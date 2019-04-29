---
title: Materialización de objetos (Servicios de datos de WCF)
ms.date: 03/30/2017
helpviewer_keywords:
- WCF Data Services, client library
- WCF Data Services, querying
ms.assetid: f0dbf7b0-0292-4e31-9ae4-b98288336dc1
ms.openlocfilehash: bf75e126c2a44b6b9d151269046d2cb8110815cc
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61774691"
---
# <a name="object-materialization-wcf-data-services"></a>Materialización de objetos (Servicios de datos de WCF)
Cuando se usa el **Add Service Reference** cuadro de diálogo para consumir un [!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)] la fuente en una aplicación cliente basada en .NET Framework, se generan clases equivalentes para cada tipo de entidad en el modelo de datos expuesto por la fuente. Para obtener más información, consulte [generar la biblioteca de cliente de servicio de datos](../../../../docs/framework/data/wcf/generating-the-data-service-client-library-wcf-data-services.md). Los datos de entidad devueltos por una consulta se materializan en una instancia de una de estas clases de servicio de datos de cliente generadas. Para obtener información acerca de las opciones de combinación y resolución de identidades para objetos con seguimiento, vea [administrar el contexto de servicio de datos](../../../../docs/framework/data/wcf/managing-the-data-service-context-wcf-data-services.md).  
  
 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] también le permite definir sus propias clases de servicio de datos de cliente en lugar de usar las clases de datos generadas por herramientas. De esta forma, puede usar sus propias clases de datos, que también se conocen como clases de datos "tipos de objetos CLR antiguos sin formato" (POCO). Al usar estos tipos de clases de datos personalizadas, debe atribuir la clase de datos con cualquiera <xref:System.Data.Services.Common.DataServiceKeyAttribute> o <xref:System.Data.Services.Common.DataServiceEntityAttribute> y asegúrese de que los nombres de tipos en los nombres de tipo de coincidencia de cliente en el modelo de datos del servicio de datos.  
  
 Después de la biblioteca recibe el mensaje de respuesta de consulta, materializa los datos devueltos desde el [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] las clases de servicio son del tipo de la consulta se envían a las instancias de datos de cliente. El proceso general para materializar estos objetos es el siguiente:  
  
1. La biblioteca de cliente lee el tipo serializado desde el elemento `entry` en la fuente del mensaje de respuesta e intenta crear una nueva instancia del tipo correcto de una de estas formas:  
  
    - Cuando el tipo declarado en la fuente tenga el mismo nombre que el tipo de la clase <xref:System.Data.Services.Client.DataServiceQuery%601>, se crea una nueva instancia de este tipo mediante el constructor vacío.  
  
    - Cuando el tipo declarado en la fuente tenga el mismo tipo que se deriva del tipo de la clase <xref:System.Data.Services.Client.DataServiceQuery%601>, se crea una nueva instancia de este tipo derivado mediante el constructor vacío.  
  
    - Cuando el tipo declarado en la fuente no se pueda hacer coincidir con el tipo de la clase <xref:System.Data.Services.Client.DataServiceQuery%601> ni con ningún tipo derivado, se crea una nueva instancia del tipo consultado mediante el constructor vacío.  
  
    - Cuando se establezca la propiedad <xref:System.Data.Services.Client.DataServiceContext.ResolveType%2A>, se llama al delegado proporcionado para invalidar la asignación de tipos basada en nombre predeterminada y, en su lugar, se crea una nueva instancia del tipo devuelto por el delgado <xref:System.Func%602>. Si este delegado devuelve un valor NULL, en su lugar se crea una nueva instancia del tipo consultado. Quizá sea necesario invalidar la asignación de nombre basada en tipo predeterminada para admitir escenarios de herencia.  
  
2. La biblioteca de cliente lee el valor de URI desde el elemento `id` de `entry`, que es el valor de identidad de la entidad. A menos que se use un valor de la propiedad <xref:System.Data.Services.Client.DataServiceContext.MergeOption%2A> de la enumeración <xref:System.Data.Services.Client.MergeOption.NoTracking>, se usa el valor de identidad para realizar el seguimiento del objeto en la clase <xref:System.Data.Services.Client.DataServiceContext>. El valor de identidad también se usa para garantizar que solo se cree una única instancia de identidad, aunque se devuelva varias veces una entidad en la respuesta de la consulta.  
  
3. La biblioteca de cliente lee propiedades desde la entrada de la fuente y establece las propiedades correspondientes en el objeto recién creado. Cuando un objeto con el mismo valor de identidad se produce en la clase <xref:System.Data.Services.Client.DataServiceContext>, las propiedades se establecen basándose en la configuración de <xref:System.Data.Services.Client.MergeOption> de la clase <xref:System.Data.Services.Client.DataServiceContext>. Puede que la respuesta contenga valores de propiedad para los que no se produzca ninguna propiedad correspondiente en el tipo de cliente. En este caso, la acción depende del valor de la propiedad <xref:System.Data.Services.Client.DataServiceContext.IgnoreMissingProperties%2A> de la clase <xref:System.Data.Services.Client.DataServiceContext>. Cuando esta propiedad se establece en `true`, se ignora la propiedad que falta. En caso contrario, se produce un error. Las propiedades se establecen de la siguiente forma:  
  
    - Las propiedades escalares se establecen en el valor correspondiente de la entrada del mensaje de respuesta.  
  
    - Las propiedades complejas se establecen en una nueva instancia de tipo complejo, que se establecen con las propiedades del tipo complejo de la respuesta.  
  
    - Las propiedades de navegación que devuelven una colección de entidades relacionadas se establecen en una instancia nueva o en una instancia existente de la interfaz <xref:System.Collections.Generic.ICollection%601>, donde `T` es el tipo de entidad relacionada. Esta colección está vacía a menos que se hayan cargado los objetos relacionados en la clase <xref:System.Data.Services.Client.DataServiceContext>. Para obtener más información, consulte [cargar contenido diferido](../../../../docs/framework/data/wcf/loading-deferred-content-wcf-data-services.md).  
  
        > [!NOTE]
        >  Cuando las clases de datos del cliente generadas admitan el enlace de datos, las propiedades de navegación devuelven instancias de la clase <xref:System.Data.Services.Client.DataServiceCollection%601> en su lugar. Para obtener más información, consulte [enlazar datos a controles](../../../../docs/framework/data/wcf/binding-data-to-controls-wcf-data-services.md).  
  
4. Se genera el evento <xref:System.Data.Services.Client.DataServiceContext.ReadingEntity>.  
  
5. La biblioteca de clientes adjunta el objeto a la clase <xref:System.Data.Services.Client.DataServiceContext>. El objeto no se adjunta cuando la clase <xref:System.Data.Services.Client.MergeOption> es la enumeración <xref:System.Data.Services.Client.MergeOption.NoTracking>.  
  
## <a name="see-also"></a>Vea también

- [Consultar el servicio de datos](../../../../docs/framework/data/wcf/querying-the-data-service-wcf-data-services.md)
- [Proyecciones de consultas](../../../../docs/framework/data/wcf/query-projections-wcf-data-services.md)
