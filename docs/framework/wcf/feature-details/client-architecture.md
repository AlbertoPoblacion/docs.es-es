---
title: Arquitectura de cliente
ms.date: 03/30/2017
ms.assetid: 02624403-0d77-41cb-9a86-ab55e98c7966
ms.openlocfilehash: 4ced24f370e2ab54528c6adb2b3617d3d849e745
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61781529"
---
# <a name="client-architecture"></a>Arquitectura de cliente
Las aplicaciones usar objetos de cliente de Windows Communication Foundation (WCF) para invocar operaciones de servicio. Este tema describen los objetos de cliente WCF, canales de cliente WCF y sus relaciones con la arquitectura de canal subyacente. Para obtener una introducción básica de los objetos de cliente WCF, vea [WCF Client Overview](../../../../docs/framework/wcf/wcf-client-overview.md). Para obtener más información acerca de la capa del canal, consulte [extensión de la capa de canal](../../../../docs/framework/wcf/extending/extending-the-channel-layer.md).  
  
## <a name="overview"></a>Información general  
 El tiempo de ejecución del modelo de servicio crea a clientes WCF, que se componen de las siguientes acciones:  
  
- Una implementación del cliente generada automáticamente de un contrato de servicios, que convierte el código de aplicación de las llamadas en mensajes salientes y convierte los mensajes de respuesta en parámetros de salida y devuelve valores que su aplicación puede recuperar.  
  
- Una implementación de una interfaz de control (<xref:System.ServiceModel.IClientChannel?displayProperty=nameWithType>) que agrupa varias interfaces y proporciona el acceso para controlar la funcionalidad, sobre todo la capacidad de cerrar la sesión del cliente y eliminar el canal.  
  
- Un canal de cliente que se crea basado en los valores de configuración especificados por el enlace utilizado.  
  
 Las aplicaciones pueden crear tales clientes a petición, ya sea a través de un <xref:System.ServiceModel.ChannelFactory?displayProperty=nameWithType> o mediante la creación de una instancia de un <xref:System.ServiceModel.ClientBase%601> clase derivada que se generan mediante la [ServiceModel Metadata Utility Tool (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md). Estas clases de cliente ya creadas se encapsulan y delegan en una implementación de canal de cliente que se construye de manera dinámica por un <xref:System.ServiceModel.ChannelFactory>. Por consiguiente, el canal de cliente y el generador de canales que los genera son el punto de interés focal para este debate.  
  
## <a name="client-objects-and-client-channels"></a>Objetos cliente y canales de cliente  
 La interfaz base de clientes WCF es la <xref:System.ServiceModel.IClientChannel?displayProperty=nameWithType> interfaz, que expone la funcionalidad del cliente principal así como la funcionalidad del objeto de comunicación básica de <xref:System.ServiceModel.ICommunicationObject?displayProperty=nameWithType>, la funcionalidad del contexto de <xref:System.ServiceModel.IContextChannel?displayProperty=nameWithType>y el comportamiento de extensible <xref:System.ServiceModel.IExtensibleObject%601?displayProperty=nameWithType>.  
  
 La interfaz <xref:System.ServiceModel.IClientChannel>, sin embargo, no define ningún contrato de servicios. Los declara la interfaz de contrato de servicio (suele generar a partir de los metadatos del servicio mediante una herramienta como el [ServiceModel Metadata Utility Tool (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)). Tipos de cliente WCF extienden <xref:System.ServiceModel.IClientChannel> y la interfaz de contrato de servicio de destino para habilitar aplicaciones llamar a operaciones directamente y también tienen acceso a la funcionalidad de tiempo de ejecución del lado cliente. Creación de un cliente WCF proporciona WCF<xref:System.ServiceModel.ChannelFactory?displayProperty=nameWithType> objetos con la información necesaria para crear un tiempo de ejecución que pueden conectarse e interactuar con el punto de conexión de servicio configurada.  
  
 Como se mencionó anteriormente, los dos tipos de cliente WCF deben configurarse antes de usarlos. Los tipos de cliente WCF más simple son objetos que derivan de <xref:System.ServiceModel.ClientBase%601> (o <xref:System.ServiceModel.DuplexClientBase%601> si el contrato de servicio es un contrato dúplex). Puede crear estos tipos utilizando un constructor, configurado mediante programación, o mediante un archivo de configuración. Después se llama directamente para invocar las operaciones de servicio. Para una introducción básica a <xref:System.ServiceModel.ClientBase%601> objetos, vea [WCF Client Overview](../../../../docs/framework/wcf/wcf-client-overview.md).  
  
 El segundo tipo se genera en el tiempo de ejecución desde una llamada al método <xref:System.ServiceModel.ChannelFactory%601.CreateChannel%2A>. Las aplicaciones relacionadas con un control estricto de los detalles de comunicación suelen usan este tipo de cliente, denominado un *objeto de canal de cliente*, porque permite una interacción más directa que el tiempo de ejecución de cliente subyacente y el canal sistema.  
  
## <a name="channel-factories"></a>Generadores de canales  
 La clase que es responsable de la creación del tiempo de ejecución subyacente que admite las invocaciones del cliente es la clase <xref:System.ServiceModel.ChannelFactory%601?displayProperty=nameWithType>. Uso de objetos de canal de objetos de cliente WCF y de cliente de WCF un <xref:System.ServiceModel.ChannelFactory%601> objeto para crear instancias; el <xref:System.ServiceModel.ClientBase%601> objeto de cliente derivado encapsula el control del generador de canales, pero en una serie de escenarios es absolutamente razonable utilizar el Generador de canales directamente. El escenario común para esto es si desea crear repetidamente nuevos canales de cliente a partir de un generador existente. Si usa un objeto de cliente, puede obtener el generador de canales subyacente de un objeto de cliente WCF mediante una llamada a la <xref:System.ServiceModel.ClientBase%601.ChannelFactory%2A?displayProperty=nameWithType> propiedad.  
  
 Lo importante que debe recordar sobre los generadores de canales es que crean nuevas instancias de canales de cliente para la configuración proporcionada para ellos antes de llamar a <xref:System.ServiceModel.ChannelFactory%601.CreateChannel%2A?displayProperty=nameWithType>. Una vez que llamamos <xref:System.ServiceModel.ChannelFactory%601.CreateChannel%2A> (o <xref:System.ServiceModel.ClientBase%601.Open%2A?displayProperty=nameWithType>, <xref:System.ServiceModel.ClientBase%601.CreateChannel%2A?displayProperty=nameWithType>, o cualquier operación en un objeto de cliente WCF), no se puede modificar el generador de canales y esperar obtener canales en distintas instancias de servicio, incluso si está cambiando solamente la dirección del punto de conexión de destino. Si desea crear un objeto de cliente o un canal de cliente con una configuración diferente, debe crear primero un nuevo generador de canales.  
  
 Para obtener más información acerca de varios problemas utilizando objetos de cliente WCF y los canales de cliente WCF, vea [servicios de acceso mediante un cliente WCF](../../../../docs/framework/wcf/feature-details/accessing-services-using-a-client.md).  
  
 Las dos secciones siguientes describen la creación y uso de los objetos de canal de cliente WCF.  
  
#### <a name="creating-a-new-wcf-client-channel-object"></a>Creación de un nuevo objeto de canal de cliente WCF  
 Para mostrar el uso de un canal de cliente, suponga que se ha generado el siguiente contrato de servicios.  
  
 [!code-csharp[C_GeneratedCodeFiles#12](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_generatedcodefiles/cs/proxycode.cs#12)]  
  
 Para conectar a un servicio `ISampleService`, utilice directamente la interfaz de contrato generada con un generador de canales (<xref:System.ServiceModel.ChannelFactory%601>). Cuando crea y configura un generador de canales para un contrato determinado, puede llamar al método <xref:System.ServiceModel.ChannelFactory%601.CreateChannel%2A> para devolver objetos de canal de cliente que puede utilizar para comunicar con un servicio `ISampleService`.  
  
 Al utilizar la clase <xref:System.ServiceModel.ChannelFactory%601> con una interfaz del contrato de servicios, debe convertirse a la interfaz <xref:System.ServiceModel.IClientChannel> para abrir, cerrar, o anular el canal explícitamente. Para facilitar su funcionamiento, la herramienta Svcutil.exe también genera una interfaz del asistente que implementa la interfaz del contrato de servicio y <xref:System.ServiceModel.IClientChannel> para permitir que usted interactúe con la infraestructura del canal de cliente sin tener que convertirse. El código siguiente muestra la definición de un canal de cliente del asistente que implementa el contrato de servicios anterior.  
  
 [!code-csharp[C_GeneratedCodeFiles#13](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_generatedcodefiles/cs/proxycode.cs#13)]  
  
#### <a name="creating-a-new-wcf-client-channel-object"></a>Creación de un nuevo objeto de canal de cliente WCF  
 Para utilizar un canal de cliente para conectar con un servicio `ISampleService`, utilice directamente la interfaz de contrato generada (o la versión del asistente) con un generador de canales, pasando el tipo de la interfaz de contrato como el parámetro de tipo. Una vez que se haya creado y configurado un generador de canales para un contrato determinado, puede llamar al método <xref:System.ServiceModel.ChannelFactory%601.CreateChannel%2A?displayProperty=nameWithType> para devolver los objetos de canal de cliente que puede utilizar para comunicar con un servicio `ISampleService`.  
  
 Cuando se crea, los objetos de canal de cliente implementan <xref:System.ServiceModel.IClientChannel> y la interfaz de contrato. Por consiguiente, puede utilizarlos directamente para llamar a las operaciones que interactúan con un servicio que admite ese contrato.  
  
 La diferencia entre utilizar los objetos de cliente y los objetos de canal de cliente es básicamente una de control y facilidad de uso para los desarrolladores. Muchos desarrolladores que estén acostumbrados a trabajar con clases y objetos preferirán utilizar el objeto de cliente WCF en lugar de canal de cliente de WCF.  
  
 Como ejemplo, vea [Cómo: Uso de ChannelFactory](../../../../docs/framework/wcf/feature-details/how-to-use-the-channelfactory.md).
