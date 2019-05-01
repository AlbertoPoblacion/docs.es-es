---
title: Novedades de Windows Communication Foundation 4.5
ms.date: 03/30/2017
helpviewer_keywords:
- WCF [WCF], what's new
- Windows Communication Foundation [WCF], what's new
ms.assetid: 7e93fe73-af93-46b5-9f63-32f761ee40cf
ms.openlocfilehash: eb506680f370e3571f1c38276d4e5d5890887a63
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61961712"
---
# <a name="whats-new-in-windows-communication-foundation-45"></a>Novedades de Windows Communication Foundation 4.5

En este tema se describe las características nuevas a la versión 4.5 de Windows Communication Foundation (WCF).

## <a name="wcf-simplification-features"></a>Características de simplificación de WCF

Se ha hecho un gran esfuerzo para simplificar el desarrollo y el mantenimiento de las aplicaciones de WCF 4.5. Para obtener más información, consulte [características de simplificación de WCF](../../../docs/framework/wcf/wcf-simplification-features.md).

### <a name="task-based-async-support"></a>Compatibilidad asincrónica basada en tareas

De forma predeterminada, la característica Agregar referencia de servicio genera métodos de operación de servicio asincrónicos de devolución de tarea. Se realiza tanto para los métodos sincrónicos como para los asincrónicos. De este modo, puede llamar a las operaciones de servicio asincrónicamente mediante el nuevo modelo de programación asincrónico basado en tareas. Cuando llama al método proxy generado, WCF crea un objeto de tarea para representar la operación asincrónica y devuelve dicha tarea. La tarea se completa cuando se complete la operación. Al implementar una operación asincrónica se puede implementar como una operación asincrónica basada en tareas. Para obtener más información, vea [sincrónica y operaciones asincrónicas](../../../docs/framework/wcf/synchronous-and-asynchronous-operations.md).

### <a name="simplified-generated-configuration-files"></a>Archivos de configuración generados simplificados

Al agregar una referencia de servicio en Visual Studio o al usar la herramienta SvcUtil.exe, se genera un archivo de configuración de cliente. En versiones anteriores de WCF, estos archivos de configuración contenían el valor de cada propiedad de enlace incluso si el valor era el predeterminado. En WCF 4.5, los archivos de configuración generados solo contienen las propiedades de enlace que se establecen en un valor no predeterminado.

Para obtener más información, consulte [características de simplificación de WCF](../../../docs/framework/wcf/wcf-simplification-features.md)

### <a name="contract-first-development"></a>Desarrollo de contrato primero

WCF admite ahora el desarrollo de contrato primero. Svcutil.exe tiene un modificador /serviceContract que permite generar contratos de servicio y los datos de un documento WSDL.

### <a name="add-service-reference-from-a-portable-subset-project"></a>Agregar referencia de servicio desde un proyecto de subconjuntos portátiles

Los proyectos de subconjuntos portátiles permiten a los programadores de ensamblados .NET mantener un único árbol de origen y un sistema de compilación a la vez que se admiten varias plataformas .NET (escritorio, Silverlight, Windows Phone y XBOX). Proyectos de subconjuntos portátiles solo hacen referencia a bibliotecas portátiles de .NET que son un ensamblado de .NET framework que se puede usar en cualquier plataforma. NET. La experiencia del desarrollador es igual que agregar una referencia de servicio en cualquier otra aplicación cliente de WCF. Para obtener más información, consulte [Add Service Reference en un proyecto de subconjuntos portátiles](../../../docs/framework/wcf/add-service-reference-in-a-portable-subset-project.md).

### <a name="aspnet-compatibility-mode-default-changed"></a>Valor predeterminado del modo de compatibilidad de ASP.NET cambiado

WCF proporciona el modo de compatibilidad de ASP.NET para conceder a los desarrolladores acceso total a las características en la canalización HTTP de ASP.NET al escribir servicios WCF. Para usar este modo, se debe establecer el `aspNetCompatibilityEnabled` atributo en true en el [ \<serviceHostingEnvironment >](../../../docs/framework/configure-apps/file-schema/wcf/servicehostingenvironment.md) sección del archivo web.config. Además, cualquier servicio de este appDomain debe tener la propiedad `RequirementsMode` en su <xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsAttribute> establecida en <xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsMode.Allowed> o en <xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsMode.Required>. De forma predeterminada <xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsAttribute> ahora está establecido en <xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsMode.Allowed>. Para obtener más información, consulte [What ' s New in Windows Communication Foundation](../../../docs/framework/wcf/whats-new.md) y [servicios WCF y ASP.NET](../../../docs/framework/wcf/feature-details/wcf-services-and-aspnet.md).

### <a name="new-transport-default-values"></a>Nuevos valores de transporte predeterminados

Para simplificar la configuración, han cambiado varios valores de propiedad de transporte predeterminados. Para obtener más información, consulte [características de simplificación de WCF](../../../docs/framework/wcf/wcf-simplification-features.md).

### <a name="xmldictionaryreaderquotas"></a>XmlDictionaryReaderQuotas

<xref:System.Xml.XmlDictionaryReaderQuotas> contiene valores de cuota configurables para los lectores de diccionario de XML que restringen la cantidad de memoria usada por un codificador mientras se crea un mensaje. Aunque estas cuotas son configurables, los valores predeterminados han cambiado para reducir la posibilidad de que un desarrollador tenga que establecerlas explícitamente. Para obtener más información, consulte [características de simplificación de WCF](../../../docs/framework/wcf/wcf-simplification-features.md).

### <a name="wcf-configuration-validation"></a>Validación de la configuración de WCF

Como parte del proceso de compilación en Visual Studio, los archivos de configuración de WCF se validan ahora para los atributos definidos en el proyecto. Se muestra una lista de errores de validación o advertencias en Visual Studio si se produce un error en la validación.

### <a name="xml-editor-tooltips"></a>Información sobre herramientas del editor XML

Para ayudar a los desarrolladores de servicios WCF nuevos y existentes a configurar sus servicios, el Editor XML de Visual Studio proporciona ahora información sobre herramientas para cada elemento de configuración que forma parte del archivo de configuración del servicio y sus propiedades.

## <a name="streaming-improvements"></a>Mejoras en streaming

Se agregó compatibilidad con el verdadero streaming asincrónico donde el lado de envío ahora no bloquea los subprocesos si el lado de recepción no está leyendo o lee despacio, lo que aumenta la escalabilidad. Se quitó la limitación de almacenamiento en búfer de mensaje cuando un cliente envía un mensaje transmitido por secuencias a un servicio WCF hospedado en IIS. Para obtener más información, consulte [características de simplificación de WCF](../../../docs/framework/wcf/wcf-simplification-features.md).

## <a name="simplifying-exposing-an-endpoint-over-https-with-iis"></a>Simplificar la exposición de un punto de conexión sobre HTTPS con IIS

Se ha agregado una asignación de protocolo HTTPS para simplificar la exposición de un extremo sobre HTTPS. Para habilitar un punto de conexión HTTPS, asegúrese de que el sitio web tenga un enlace HTTPS y un certificado SSL configurado y, a continuación, habilite simplemente HTTPS para el directorio virtual que hospeda el servicio. Si los metadatos están habilitados para el servicio, también se expondrán mediante HTTPS.

## <a name="generating-a-single-wsdl-document"></a>Generar un único documento WSDL

Algunas pilas de procesamiento WSDL de terceros no pueden procesar los documentos WSDL que tienen dependencias de otros documentos mediante xsd:import. WCF permite especificar ahora que toda la información del WSDL se devuelva en un único documento. Para solicitar un solo documento WSDL, anexe "? singleWSDL" al identificador URI cuando solicite metadatos del servicio.

## <a name="websocket-support"></a>Compatibilidad de WebSocket

WebSockets es una tecnología que proporciona comunicación bidireccional verdadera por los puertos 80 y 443 con características de rendimiento similares a TCP. Se han agregado dos nuevos enlaces para admitir la comunicación mediante un transporte WebSocket. <xref:System.ServiceModel.NetHttpBinding> y <xref:System.ServiceModel.NetHttpsBinding>. Para obtener más información, vea: [Los enlaces proporcionados por el sistema](../../../docs/framework/wcf/system-provided-bindings.md).

## <a name="new-transport-default-values"></a>Nuevos valores de transporte predeterminados

En la tabla siguiente se describen los valores que han cambiado y dónde encontrar información adicional.

|Propiedad|Activado|Nuevo valor predeterminado|Para obtener más información, vea|
|--------------|--------|-----------------|------------------------------|
|channelInitializationTimeout|<xref:System.ServiceModel.NetTcpBinding>|30 segundos|<xref:System.ServiceModel.Channels.ConnectionOrientedTransportBindingElement.ChannelInitializationTimeout%2A>|
|listenBacklog|<xref:System.ServiceModel.NetTcpBinding>|12 * número de procesadores|<xref:System.ServiceModel.NetTcpBinding.ListenBacklog%2A>|
|maxPendingAccepts|ConnectionOrientedTransportBindingElement<br /><br /> SMSvcHost.exe|2 * número de procesadores para transporte<br /><br /> 4 \* número de procesadores para SMSvcHost.exe|<xref:System.ServiceModel.Channels.ConnectionOrientedTransportBindingElement.MaxPendingAccepts%2A> [Configurar el servicio de uso compartido de puertos Net.TCP](../../../docs/framework/wcf/feature-details/configuring-the-net-tcp-port-sharing-service.md)|
|maxPendingConnections|ConnectionOrientedTransportBindingElement|12 * número de procesadores|<xref:System.ServiceModel.Channels.ConnectionOrientedTransportBindingElement.MaxPendingConnections%2A>|
|receiveTimeout|SMSvcHost.exe|30 segundos|[Configuración del servicio de uso compartido de puertos Net.TCP](../../../docs/framework/wcf/feature-details/configuring-the-net-tcp-port-sharing-service.md)|

## <a name="xml-editor-tooltips"></a>Información sobre herramientas del editor XML

Para ayudar a los desarrolladores de servicios WCF nuevos y existentes a configurar sus servicios, el Editor XML de Visual Studio proporciona ahora información sobre herramientas para cada elemento de configuración que forma parte del archivo de configuración del servicio y sus propiedades.

## <a name="configuring-wcf-services-in-code"></a>Configurar servicios WCF en el código

Windows Communication Foundation (WCF) permite a los desarrolladores configurar servicios mediante archivos de configuración o código. Los archivos de configuración son útiles cuando un servicio se debe configurar después de implementarse. Cuando se usan archivos de configuración, un profesional de TI solo debe actualizar el archivo de configuración; no es necesario que realice ninguna recompilación. Los archivos de configuración, sin embargo, pueden ser complejos y difíciles de mantener. No se admite la depuración de archivos de configuración y se hace referencia a los elementos de configuración por nombre, con lo que la creación de archivos de configuración resulta propensa a errores y difícil. WCF también permite configurar los servicios en el código. En versiones anteriores de servicios de configuración de WCF (4.0 y versiones anteriores) en el código era sencilla en escenarios autohospedados; la <xref:System.ServiceModel.ServiceHost> clase permite configurar los puntos de conexión y comportamientos antes de llamar a ServiceHost.Open. En escenarios hospedados en web, sin embargo, no tiene acceso a la clase <xref:System.ServiceModel.ServiceHost>. Para configurar un servicio hospedado en web era necesario crear un `System.ServiceModel.ServiceHostFactory` que creó el <xref:System.ServiceModel.Activation.ServiceHostFactory> y realizar cualquier configuración necesaria. A partir de .NET 4.5, WCF ofrece una manera más fácil de configurar ambos autohospedado y hospedado en web services en el código. Para obtener más información, consulte [configurar servicios de WCF en el código](../../../docs/framework/wcf/configuring-wcf-services-in-code.md).

## <a name="channelfactory-caching"></a>Almacenamiento en caché de ChannelFactory

Las aplicaciones cliente de WCF usan la clase <xref:System.ServiceModel.ChannelFactory%601> para crear un canal de comunicación con un servicio WCF. La crear de instancias de <xref:System.ServiceModel.ChannelFactory%601> genera sobrecarga porque implica las siguientes operaciones:

1. Construir el árbol <xref:System.ServiceModel.Description.ContractDescription>

2. Reflejar todos los tipos de CLR necesarios

3. Construir la pila del canal

4. Desechar recursos

Para ayudar a reducir esta sobrecarga, WCF puede almacenar en caché los generadores de canal cuando se usa un proxy de cliente de WCF. Para obtener más información, consulte [generador de canales y almacenamiento en caché](../../../docs/framework/wcf/feature-details/channel-factory-and-caching.md).

## <a name="compression-and-the-binary-encoder"></a>Compresión y el codificador binario

A partir de WCF 4.5, el codificador binario de WCF agrega compatibilidad con la compresión. El tipo de compresión se configura con la propiedad <xref:System.ServiceModel.Channels.BinaryMessageEncodingBindingElement.CompressionFormat%2A>. Tanto el cliente como el servicio deben configurar la propiedad <xref:System.ServiceModel.Channels.BinaryMessageEncodingBindingElement.CompressionFormat%2A>. La compresión funcionará para los protocolos HTTP, HTTPS y TCP. Si un cliente especifica usar compresión pero el servicio no la admite, se produce una excepción de protocolo que indica que no coinciden los protocolos. Para obtener más información, consulte [elegir un codificador de mensajes](../../../docs/framework/wcf/feature-details/choosing-a-message-encoder.md)

## <a name="udp"></a>UDP

Un transporte UDP que permite a los desarrolladores escribir servicios que usan "desencadenar y omitir" se ha agregado compatibilidad con mensajería. Un cliente envía un mensaje a un servicio y no espera ninguna respuesta de él.

## <a name="multiple-authentication-support"></a>Compatibilidad con autenticación múltiple

Se ha agregado compatibilidad para admitir varios modos de autenticación, como compatibles con IIS, en un solo extremo de WCF cuando se usa el transporte HTTP y la seguridad de transporte. IIS permite habilitar varios modos de autenticación en un directorio virtual; esta característica permite que un solo punto de conexión WCF admita los distintos modos de autenticación habilitados para el directorio virtual donde se hospeda el servicio WCF.

## <a name="idn-support"></a>Compatibilidad con IDN

Se ha agregado compatibilidad para permitir servicios WCF con nombres de dominio internacionalizados. Para obtener más información, consulte [WCF y nombres de dominio internacionalizados](../../../docs/framework/wcf/feature-details/wcf-and-internationalized-domain-names.md).

## <a name="httpclient"></a>HttpClient

Se ha agregado una nueva clase denominada <xref:System.Net.Http.HttpClient> para simplificar el trabajo con solicitudes HTTP. Para obtener más información, consulte [hacer que las aplicaciones sociales y conectadas a servicios HTTP](https://go.microsoft.com/fwlink/?LinkId=231886) y [ejemplo de cliente HTTP](https://code.msdn.microsoft.com/windowsapps/HttpClient-sample-55700664).

## <a name="configuration-intellisense"></a>IntelliSense de configuración

Los valores de atributo de los archivos de configuración para los atributos personalizados definidos en el proyecto ahora admiten IntelliSense para facilitar el trabajo con configuraciones de forma rápida y precisa.

## <a name="configuration-tooltips"></a>Información sobre herramientas de configuración

Atributos y elementos WCF ahora tienen información sobre herramientas en el editor XML, que más fácilmente e identifican con precisión el propósito del elemento o atributo.

## <a name="paste-data-as-classes"></a>Pegar datos como clases

En un proyecto de WCF, los tipos de datos definidos en XML (como los expuestos en un servicio) se pueden pegar directamente en una página de códigos. El tipo XML se pegará como un tipo de CLR. Consulte [generar clases de tipos de datos desde XML](../../../docs/framework/wcf/generating-data-type-classes-from-xml.md) para obtener más detalles.

## <a name="webservicehost-and-default-endpoints"></a>WebServiceHost y los puntos de conexión predeterminados

En Visual Studio 2010, WebServiceHost creaba automáticamente un extremo predeterminado sin importar si se había especificado explícitamente un extremo o no. En Visual Studio 2012 y versiones posteriores, WebServiceHost solo crea un extremo predeterminado si no se agrega explícitamente ningún punto de conexión. Si el cliente está esperando el punto de conexión predeterminado puede agregar un punto de conexión explícitamente y hacia al cliente. Como alternativa, puede pedirle a WCF que vuelva al comportamiento anterior; para ello, agregue la siguiente configuración al archivo de configuración de aplicaciones

```xml
<appSettings>
    <add key="wcf:webservicehost:enableautomaticendpointscompatability" value="true"/>
  </appSettings>
```

## <a name="ihttpcookiecontainermanager"></a>IHttpCookieContainerManager

Esta interfaz, expuesta por <xref:System.ServiceModel.Channels.IChannelFactory%601>, facilita considerablemente el trabajo con cookies en el lado cliente. Cuando AllowCookies se establece en true en el enlace, puede obtener acceso a las cookies con el siguiente código:

```csharp
IHttpCookieContainerManager cookieManager = factory.GetProperty<IHttpCookieContainerManager>();
System.Net.CookieContainer container = cookieManager.CookieContainer;
```

A continuación, puede establecer o recuperar las cookies desde <xref:System.Net.CookieContainer>. Cuando AllowCookies se establece en false, puede recuperar manualmente las cookies mediante <xref:System.ServiceModel.OperationContext> y enviarlo en otras solicitudes con otro <xref:System.ServiceModel.OperationContext> o inspector de mensaje. La interfaz de IHttpCookieContainerManager permite autenticar un usuario con un servicio y usar la cookie de autenticación devuelta por dicho servicio para autenticar con otros servicios.
