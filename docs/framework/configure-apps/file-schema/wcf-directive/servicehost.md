---
title: '@ServiceHost'
ms.date: 03/30/2017
ms.assetid: 96ba6967-00f2-422f-9aa7-15de4d33ebf3
ms.openlocfilehash: dd3dd026749ccc299cd922b79dcae8ccbcc722d8
ms.sourcegitcommit: f348c84443380a1959294cdf12babcb804cfa987
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/12/2019
ms.locfileid: "73968826"
---
# <a name="servicehost"></a>\@ServiceHost
Asocia el generador usado para crear el host del servicio con el servicio que se va a hospedar y otros aspectos de programación necesarios para tener acceso o compilar el código de hospedaje proporcionado en el archivo .svc.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
<% @ServiceHost
Service = "Service, ServiceNamespace"
Factory = "Factory, FactoryNamespace"
Debug = "Debug"
Language = "Language"
CodeBehind = "CodeBehind"
%>
```  
  
## <a name="attributes"></a>Atributos  
  
#### <a name="service"></a>web de Office  
 El nombre del tipo de CLR del servicio hospedado. Esto debería ser un nombre completo de un tipo que implementa uno o varios contactos del servicio.  
  
#### <a name="factory"></a>Factory  
 El nombre de tipo de CLR del generador de host de servicio usado para crear instancias del host del servicio. Este atributo es opcional. Si no se especifica, se usa el valor predeterminado <xref:System.ServiceModel.Activation.ServiceHostFactory> que devuelve una instancia de <xref:System.ServiceModel.ServiceHost>.  
  
#### <a name="debug"></a>Depuración  
 Indica si el servicio Windows Communication Foundation (WCF) se debe compilar con símbolos de depuración. `true` si el servicio WCF se debe compilar con símbolos de depuración; de lo contrario, `false`.  
  
#### <a name="language"></a>Lenguaje  
 Especifica el lenguaje usado al compilar todo el código en línea del archivo (.svc). Los valores pueden representar cualquier lenguaje compatible con .NET, incluyendo C#, VB y JS, que hacen referencia a C#, Visual Basic .NET y JScript .NET, respectivamente. Este atributo es opcional.  
  
#### <a name="codebehind"></a>CodeBehind  
 Especifica el archivo de código fuente que implementa el servicio Web XML, cuando la clase que implementa dicho servicio no reside en el mismo archivo, y no se ha compilado en un ensamblado ni se ha colocado en el directorio \Bin.  
  
## <a name="remarks"></a>Comentarios  
 El <xref:System.ServiceModel.ServiceHost> que se usa para hospedar el servicio es un punto de extensibilidad dentro del modelo de programación de Windows Communication Foundation (WCF). Se usa un patrón del generador para crear <xref:System.ServiceModel.ServiceHost> porque es, potencialmente, un tipo polimórfico del que el entorno de hospedaje no debería crear instancias directamente.  
  
 las implementaciones predeterminadas usan <xref:System.ServiceModel.Activation.ServiceHostFactory> para crear una instancia de <xref:System.ServiceModel.ServiceHost>. Sin embargo, puede proporcionar su propio generador (uno que devuelve el host derivado) especificando el nombre de tipo de CLR de la implementación del generador en la directiva [\@ServiceHost](servicehost.md) .  
  
 Para usar su propio generador de host de servicio personalizado en lugar del generador predeterminado, simplemente proporcione el nombre de tipo en la directiva [@ServiceHost](servicehost.md) como se indica a continuación:  
  
```xml  
<% @ServiceHost Factory="DerivedFactory" Service="MyService" %>  
```  
  
 Mantenga las implementaciones del generador tan ligeras como sea posible. Si tiene mucha lógica personalizada, su código es más reutilizable si coloca esa lógica dentro de su host en lugar de dentro del generador.  
  
 Por ejemplo, para habilitar un punto de conexión habilitado para AJAX para `MyService`, especifique el <xref:System.ServiceModel.Activation.WebScriptServiceHostFactory> para el valor del atributo `Factory`, en lugar del <xref:System.ServiceModel.Activation.ServiceHostFactory>predeterminado, en la directiva [@ServiceHost](servicehost.md) , tal como se muestra en el ejemplo siguiente.  
  
## <a name="example"></a>Ejemplo  
  
```xml  
<% @ServiceHost
Service="MyService"  
Language="C#"  
Debug="true"  
Factory="WebScriptServiceHostFactory"  
%>  
```  
  
## <a name="see-also"></a>Vea también

- [Host de servicio personalizado](../../../wcf/samples/custom-service-host.md)
