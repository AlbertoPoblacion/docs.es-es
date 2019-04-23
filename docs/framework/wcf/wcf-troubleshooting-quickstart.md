---
title: Inicio rápido de solución de problemas de WCF
ms.date: 03/30/2017
helpviewer_keywords:
- WCF [WCF], troubleshooting
- Windows Communication Foundation [WCF], troubleshooting
ms.assetid: a9ea7a53-f31a-46eb-806e-898e465a4992
ms.openlocfilehash: 4327e8bb07cb03a91f7384f7fe82bc2e47f6fcb9
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59320007"
---
# <a name="wcf-troubleshooting-quickstart"></a>Inicio rápido de solución de problemas de WCF
En este tema se enumeran muchos problemas conocidos que los clientes han detectado al desarrollar clientes y servicios de WCF. Si el problema que tiene no aparece en esta lista, se recomienda que configure la traza del servicio. De esta forma, se genera un archivo de seguimiento que puede ver con el visor de archivos de seguimiento y obtiene información detallada sobre las excepciones que se pueden producir en el servicio. Para obtener más información sobre la configuración de seguimiento, vea: [Configuración del seguimiento](../../../docs/framework/wcf/diagnostics/tracing/configuring-tracing.md). Para obtener más información sobre el Visor del archivo de seguimiento, vea: [Herramienta de Visor de seguimiento (SvcTraceViewer.exe) del servicio](../../../docs/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe.md).  
  
1. [Después de instalar Windows 7 e IIS, cuando intente explorar un servicio WCF puede obtener el mensaje de error siguiente: Error HTTP 404.3 – no encontrado](../../../docs/framework/wcf/wcf-troubleshooting-quickstart.md#bkmk_0)  
  
     Error HTTP 404.3 – No encontrada. La página que solicita no puede presentarse debido a la configuración de la extensión. Si la página es un script, agregue un controlador. Si se descarga el archivo, agregue un mapa MIME. Error detallado InformationModule StaticFileModule.  
  
2. [A veces recibo una excepción MessageSecurityException en la segunda solicitud si mi cliente está inactivo durante algún tiempo después de la primera solicitud. ¿Qué sucede?](../../../docs/framework/wcf/wcf-troubleshooting-quickstart.md#BKMK_q1)  
  
3. [Mi servicio empieza a rechazar nuevos clientes cuando interactúa con unos 10 clientes. ¿Qué sucede?](../../../docs/framework/wcf/wcf-troubleshooting-quickstart.md#BKMK_q2)  
  
4. [¿Puedo cargar mi configuración de servicio desde otra parte que no sea el archivo de configuración de la aplicación WCF?](../../../docs/framework/wcf/wcf-troubleshooting-quickstart.md#BKMK_q3)  
  
5. [Mi servicio y cliente funcionan muy bien, pero no puedo conseguir que funcionen cuando el cliente está en otro equipo. ¿Qué sucede?](../../../docs/framework/wcf/wcf-troubleshooting-quickstart.md#BKMK_q4)  
  
6. [Cuando produzco una FaultException\<excepción > donde el tipo es una excepción, siempre recibo un tipo FaultException general en el cliente y no el tipo genérico. ¿Qué sucede?](../../../docs/framework/wcf/wcf-troubleshooting-quickstart.md#BKMK_q5)  
  
7. [Parece que las operaciones unidireccionales y las operaciones solicitud-respuesta se devuelven aproximadamente a la misma velocidad cuando la respuesta no contiene datos. ¿Qué sucede?](../../../docs/framework/wcf/wcf-troubleshooting-quickstart.md#BKMK_q6)  
  
8. [Estoy usando un certificado X.509 con mi servicio y obtengo una excepción System.Security.Cryptography.CryptographicException. ¿Qué sucede?](../../../docs/framework/wcf/wcf-troubleshooting-quickstart.md#BKMK_q77)  
  
9. [He cambiado el primer parámetro de una operación de mayúsculas a minúsculas; ahora mi cliente produce una excepción. ¿Qué sucede?](../../../docs/framework/wcf/wcf-troubleshooting-quickstart.md#BKMK_q88)  
  
10. [Estoy utilizando una de mis herramientas de traza y obtengo la excepción EndpointNotFoundException. ¿Qué sucede?](../../../docs/framework/wcf/wcf-troubleshooting-quickstart.md#BKMK_q99)  
  
11. [Al llamar a una aplicación Web HTTP de WCF desde una aplicación SOAP de WCF el servicio devuelve el error siguiente: 405 método no permitido](../../../docs/framework/wcf/wcf-troubleshooting-quickstart.md#BK_MK99)  
  
 [¿Cuál es la dirección base? ¿Cómo se relaciona con una dirección de extremo?](../../../docs/framework/wcf/wcf-troubleshooting-quickstart.md#BKMK_q10)  
  
<a name="bkmk_0"></a>   
## <a name="after-installing-windows-7-and-iis-when-i-attempt-to-browse-to-a-wcf-service-i-get-the-following-error-message-http-error-4043--not-found"></a>Después de instalar Windows 7 e IIS, cuando intente explorar un servicio WCF puede obtener el mensaje de error siguiente: Error HTTP 404.3 – no encontrado  
 El mensaje de error completo es:  
  
 Error HTTP 404.3 – No encontrada. La página que solicita no puede presentarse debido a la configuración de la extensión. Si la página es un script, agregue un controlador. Si se descarga el archivo, agregue un mapa MIME. Error detallado InformationModule StaticFileModule.  
  
 Este mensaje de error se produce cuando "Activación HTTP de Windows Communication Foundation" no se establece explícitamente en el Panel de Control. Para establecer esto vaya al Panel de control, programas de la esquina inferior izquierda de la ventana. Haga clic en Activar o desactivar las características de Windows. Expanda el elemento con la etiqueta Microsoft .NET Framework 3.5.1, seleccione Activación HTTP de Windows Communication Foundation .  
  
<a name="BKMK_q1"></a>   
## <a name="sometimes-i-receive-a-messagesecurityexception-on-the-second-request-if-my-client-is-idle-for-a-while-after-the-first-request-what-is-happening"></a>A veces recibo una excepción MessageSecurityException en la segunda solicitud si mi cliente está inactivo durante algún tiempo después de la primera solicitud. ¿Qué sucede?  
 Puede producir un error en la segunda solicitud principalmente por dos motivos: (1) la sesión ha expirado o (2) el servidor Web que hospeda el servicio se recicla. En el primer caso, la sesión es válida hasta que se agota el tiempo de espera del servicio. Cuando el servicio no recibe una solicitud del cliente dentro del período de tiempo especificado en el enlace del servicio (<xref:System.ServiceModel.Channels.Binding.ReceiveTimeout%2A>), el servicio finaliza la sesión de seguridad. Los siguientes mensajes del cliente producen <xref:System.ServiceModel.Security.MessageSecurityException>. El cliente debe restablecer una sesión segura con el servicio para enviar los futuros mensajes o utilizar un token de contexto de seguridad con estado. Los tokens de contexto de seguridad con estado también permiten que una sesión segura sobreviva a un servidor web que se recicla. Para obtener más información sobre el uso de tokens de contexto de seguridad en una sesión segura, consulte [Cómo: Crear un contexto de seguridad para una sesión segura Token](../../../docs/framework/wcf/feature-details/how-to-create-a-security-context-token-for-a-secure-session.md). También puede deshabilitar las sesiones seguras. Cuando se usa el [ \<wsHttpBinding >](../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md) enlace, puede establecer el `establishSecurityContext` propiedad `false` para deshabilitar las sesiones seguras. Para deshabilitar las sesiones seguras para otros enlaces, debe crear un enlace personalizado. Para obtener más información acerca de cómo crear un enlace personalizado, vea [Cómo: Crear un enlace personalizado mediante SecurityBindingElement](../../../docs/framework/wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md). Antes de aplicar cualquiera de estas opciones, debe entender los requisitos de seguridad de su aplicación.  
  
<a name="BKMK_q2"></a>   
## <a name="my-service-starts-to-reject-new-clients-after-about-10-clients-are-interacting-with-it-what-is-happening"></a>Mi servicio empieza a rechazar nuevos clientes cuando interactúa con unos 10 clientes. ¿Qué sucede?  
 De forma predeterminada, los servicios pueden tener solo 10 sesiones simultáneas. Por tanto, si los enlaces del servicio utilizan sesiones, el servicio acepta nuevas conexiones de cliente hasta que alcance ese numero, después del cual rechaza nuevas conexiones de cliente hasta que finaliza una de las sesiones actuales. Puede admitir más clientes de varias maneras. Si su servicio no requiere sesiones, no utilice un enlace con sesión. (Para obtener más información, consulte [mediante sesiones](../../../docs/framework/wcf/using-sessions.md).) Otra opción es aumentar el límite de sesiones cambiando el valor de propiedad <xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentSessions%2A> al número apropiado a su circunstancia.  
  
<a name="BKMK_q3"></a>   
## <a name="can-i-load-my-service-configuration-from-somewhere-other-than-the-wcf-applications-configuration-file"></a>¿Puedo cargar mi configuración de servicio desde otra parte que no sea el archivo de configuración de la aplicación WCF?  
 Sí, sin embargo, tiene que crear una clase <xref:System.ServiceModel.ServiceHost> personalizada que invalide el método <xref:System.ServiceModel.ServiceHostBase.ApplyConfiguration%2A> . Dentro de ese método, puede llamar a la base para cargar primero la configuración (si desea también cargar la información de configuración estándar), pero también puede reemplazar completamente el sistema de carga de configuración. Tenga en cuenta que si desea cargar la configuración desde un archivo de configuración que es diferente del archivo de configuración de la aplicación, debe analizar usted mismo el archivo de configuración y cargar la configuración.  
  
 El siguiente ejemplo de código muestra cómo invalidar el método <xref:System.ServiceModel.ServiceHostBase.ApplyConfiguration%2A> y configurar directamente un extremo.  
  
```csharp
public class MyServiceHost : ServiceHost  
{  
    public MyServiceHost(Type serviceType, params Uri[] baseAddresses)    
      : base(serviceType, baseAddresses)  
    {
        Console.WriteLine("MyServiceHost Constructor");
    }  
  
    protected override void ApplyConfiguration()  
    {  
        string straddress = GetAddress();  
        Uri address = new Uri(straddress);  
        Binding binding = GetBinding();  
        base.AddServiceEndpoint(typeof(IData), binding, address);  
    }  
  
    string GetAddress()  
    {
        return "http://MyMachine:7777/MyEndpointAddress/";
    }  
  
    Binding GetBinding()  
    {  
        WSHttpBinding binding = new WSHttpBinding();  
        binding.Security.Mode = SecurityMode.None;  
        return binding;  
    }  
}  
```  
  
<a name="BKMK_q4"></a>   
## <a name="my-service-and-client-work-great-but-i-cant-get-them-to-work-when-the-client-is-on-another-computer-whats-happening"></a>Mi servicio y cliente funcionan muy bien, pero no puedo conseguir que funcionen cuando el cliente está en otro equipo. ¿Qué sucede?  
 Dependiendo de la excepción, puede haber varios problemas:  
  
-   Puede que necesite cambiar las direcciones de extremo del cliente al nombre de host y no el "localhost".  
  
-   Puede que necesite abrir el puerto a la aplicación. Para obtener más información, consulte [Firewall Instructions](../../../docs/framework/wcf/samples/firewall-instructions.md) en los ejemplos de SDK.  
  
-   Para otros posibles problemas, vea el tema de los ejemplos [ejecutando los ejemplos de Windows Communication Foundation](./samples/running-the-samples.md).  
  
-   Si su cliente está utilizando las credenciales de Windows y la excepción es <xref:System.ServiceModel.Security.SecurityNegotiationException>, configure Kerberos tal y como se muestra a continuación.  
  
    1.  Agregue las credenciales de identidad al elemento de extremo en el archivo del cliente App.config:  
  
        ```xml
        <endpoint   
          address="http://MyServer:8000/MyService/"   
          binding="wsHttpBinding"   
          bindingConfiguration="WSHttpBinding_IServiceExample"   
          contract="IServiceExample"   
          behaviorConfiguration="ClientCredBehavior"   
          name="WSHttpBinding_IServiceExample">  
          <identity>  
            <userPrincipalName value="name@corp.contoso.com"/>  
          </identity>  
        </endpoint>  
        ```  
  
    2.  Ejecute el servicio autohospedado con la cuenta System o NetworkService. Puede ejecutar este comando para crear una ventana de comandos bajo la cuenta del sistema:  
  
        ```console
        at 12:36 /interactive "cmd.exe"  
        ```  
  
    3.  Hospede el servicio bajo IIS (Servicios de Internet Information Services) (IIS) que, de forma predeterminada, utiliza la cuenta del nombre de entidad de seguridad de servicio (SPN).  
  
    4.  Registre un nuevo SPN con el dominio utilizando SetSPN. Tenga en cuenta que, para ello, necesitará ser un administrador de dominio.  
  
 Para obtener más información acerca del protocolo Kerberos, consulte [Security Concepts Used in WCF](../../../docs/framework/wcf/feature-details/security-concepts-used-in-wcf.md) y:  
  
-   [Depuración de errores de autenticación de Windows](../../../docs/framework/wcf/feature-details/debugging-windows-authentication-errors.md)  
  
-   [Registrar nombres principales de servicio de Kerberos mediante Http.sys](https://go.microsoft.com/fwlink/?LinkId=86943)  
  
-   [Kerberos Explained (Kerberos en detalle)](https://go.microsoft.com/fwlink/?LinkId=86946)  
  
<a name="BKMK_q5"></a>   
## <a name="when-i-throw-a-faultexceptionexception-where-the-type-is-an-exception-i-always-receive-a-general-faultexception-type-on-the-client-and-not-the-generic-type-whats-happening"></a>Cuando produzco una FaultException\<excepción > donde el tipo es una excepción, siempre recibo un tipo FaultException general en el cliente y no el tipo genérico. ¿Qué sucede?  
 Es muy recomendable que cree su propio tipo de datos de error personalizado y lo declare como tipo detallado en el contrato de error. La razón es que utilizando los tipos de excepción proporcionados por el sistema:  
  
-   Crea una dependencia de tipo que quita uno de los puntos fuertes más grandes de las aplicaciones orientadas al servicio.  
  
-   No se puede esperar que las excepciones se serialicen de una manera estándar. Puede que algunas, como <xref:System.Security.SecurityException>no se puedan serializar en absoluto.  
  
-   Expone los detalles internos de la implementación a los clientes. Para obtener más información, consulte [especificar y controlar errores en contratos y servicios](../../../docs/framework/wcf/specifying-and-handling-faults-in-contracts-and-services.md).  
  
 Si está depurando una aplicación, sin embargo, puede serializar información de excepción y devolverla al cliente utilizando la clase <xref:System.ServiceModel.Description.ServiceDebugBehavior> .  
  
<a name="BKMK_q6"></a>   
## <a name="it-seems-like-one-way-and-request-reply-operations-return-at-roughly-the-same-speed-when-the-reply-contains-no-data-whats-happening"></a>Parece que las operaciones unidireccionales y las operaciones solicitud-respuesta se devuelven aproximadamente a la misma velocidad cuando la respuesta no contiene datos. ¿Qué sucede?  
 Especificando que una operación es unidireccional solo significa que el contrato de operación acepta un mensaje de entrada y no devuelve un mensaje de salida. En WCF, todas las invocaciones de cliente devuelven cuando los datos salientes se ha escrito en la conexión o se produce una excepción. Las operaciones unidireccionales funcionan de la misma manera y se pueden iniciar si el servicio no se puede localizar o se pueden bloquear si el servicio no está preparado para aceptar los datos de la red. Normalmente en WCF, esto da como resultado llamadas unidireccionales que vuelven al cliente más rápidamente que la solicitud-respuesta; pero las condiciones que ralentizan el envío de los datos salientes a través de la red ralentizan las operaciones unidireccionales, así como las operaciones de solicitud-respuesta. Para obtener más información, consulte [servicios unidireccional](../../../docs/framework/wcf/feature-details/one-way-services.md) y [servicios de acceso mediante un cliente WCF](../../../docs/framework/wcf/feature-details/accessing-services-using-a-client.md).  
  
<a name="BKMK_q77"></a>   
## <a name="im-using-an-x509-certificate-with-my-service-and-i-get-a-systemsecuritycryptographycryptographicexception-whats-happening"></a>Estoy usando un certificado X.509 con mi servicio y obtengo una excepción System.Security.Cryptography.CryptographicException. ¿Qué sucede?  
 Esto se produce normalmente después de cambiar la cuenta de usuario bajo la cual se ejecuta el proceso de trabajo de IIS. Por ejemplo, en [!INCLUDE[wxp](../../../includes/wxp-md.md)], si cambia la cuenta de usuario predeterminada que Aspnet_wp.exe ejecuta desde ASPNET a una cuenta de usuario personalizada, puede ver este error. Si utiliza una clave privada, el proceso que utiliza necesitará tener los permisos para tener acceso al archivo que almacena esa clave.  
  
 Si éste es el caso, debe dar los privilegios de acceso de lectura a la cuenta del proceso para el archivo que contiene la clave privada. Por ejemplo, si el proceso de trabajo de IIS se está ejecutando bajo la cuenta Bob, entonces, necesitará proporcionar a Bob el acceso de lectura al archivo que contiene la clave privada.  
  
 Para obtener más información acerca de cómo proporcionar a la cuenta de usuario correcta acceso al archivo que contiene la clave privada para un certificado X.509 concreto, vea [Cómo: Hacer que los certificados X.509 accesibles para WCF](../../../docs/framework/wcf/feature-details/how-to-make-x-509-certificates-accessible-to-wcf.md).  
  
<a name="BKMK_q88"></a>   
## <a name="i-changed-the-first-parameter-of-an-operation-from-uppercase-to-lowercase-now-my-client-throws-an-exception-whats-happening"></a>He cambiado el primer parámetro de una operación de mayúsculas a minúsculas; ahora mi cliente produce una excepción. ¿Qué sucede?  
 El valor de los nombres de parámetro en la firma de la operación forma parte del contrato y distingue entre mayúsculas y minúsculas. Utilice el atributo <xref:System.ServiceModel.MessageParameterAttribute?displayProperty=nameWithType> cuando necesite distinguir entre el nombre de parámetro local y los metadatos que describen la operación para las aplicaciones cliente.  
  
<a name="BKMK_q99"></a>   
## <a name="im-using-one-of-my-tracing-tools-and-i-get-an-endpointnotfoundexception-whats-happening"></a>Estoy utilizando una de mis herramientas de traza y obtengo la excepción EndpointNotFoundException. ¿Qué sucede?  
 Si está utilizando una herramienta de seguimiento que no es el mecanismo de seguimiento de WCF proporcionados por el sistema y recibe un <xref:System.ServiceModel.EndpointNotFoundException> que indica que se ha producido un error de coincidencia de filtro de dirección, deberá usar el <xref:System.ServiceModel.Description.ClientViaBehavior> clase para dirigir los mensajes a la utilidad de seguimiento y tiene la utilidad redirija esos mensajes a la dirección del servicio. La clase <xref:System.ServiceModel.Description.ClientViaBehavior> modifica `Via` que dirige el encabezado para especificar la siguiente dirección de red de forma independiente con respecto al receptor último, indicado por `To` que dirige el encabezado. Cuando haga esto, sin embargo, no cambie la dirección del extremo, la cual se utiliza para establecer el valor `To` .  
  
 El ejemplo de código siguiente muestra un ejemplo de archivo de configuración de cliente.  
  
```xml
<endpoint   
  address="http://localhost:8000/MyServer/"  
  binding="wsHttpBinding"  
  bindingConfiguration="WSHttpBinding_IMyContract"  
  behaviorConfiguration="MyClient"   
  contract="IMyContract"   
  name="WSHttpBinding_IMyContract">  
</endpoint>  
<behaviors>  
  <endpointBehaviors>  
    <behavior name="MyClient">  
      <clientVia viaUri="http://localhost:8001/MyServer/"/>  
    </behavior>  
  </endpointBehaviors>  
</behaviors>  
```  
  
<a name="BKMK_q10"></a>   
## <a name="what-is-the-base-address-how-does-it-relate-to-an-endpoint-address"></a>¿Cuál es la dirección base? ¿Cómo se relaciona con una dirección de extremo?  
 Una dirección base es la dirección de raíz para una clase <xref:System.ServiceModel.ServiceHost> . De forma predeterminada, si agrega una clase <xref:System.ServiceModel.Description.ServiceMetadataBehavior> en su configuración de servicio, el lenguaje de descripción de servicios Web (WSDL) para todos los extremos que publica el host se recupera de la dirección base de HTTP, más cualquier dirección relativa proporcionada al comportamiento de los metadatos, más "? wsdl". Si está familiarizado con [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] e IIS, la dirección base es equivalente al directorio virtual.  
  
## <a name="sharing-a-port-between-a-service-endpoint-and-a-mex-endpoint-using-the-nettcpbinding"></a>Compartir un puerto entre un extremo de servicio y un extremo mex mediante NetTcpBinding  
 Si especifica la dirección base para un servicio como net.tcp://MyServer:8080/MyService y agrega los siguientes extremos:  
  
```xml  
<services>  
  <service name="Microsoft.Samples.NetTcp.CalculatorService">  
    <endpoint address="calcsvc" binding ="netTcpBinding" contract="Microsoft.Samples.NetTcp.ICalculator"/>  
    <endpoint address="mex" binding="mexTcpBinding" contract="IMetadataExchange" />  
  </service>  
</services>  
```  
  
 Y si modifica uno de los valores de NetTcpBinding como se muestra en el siguiente fragmento de código de configuración:  
  
```xml  
<bindings>  
  <netTcpBinding>  
    <binding closeTimeout="00:01:00" openTimeout="00:01:00" receiveTimeout="00:10:00" sendTimeout="00:01:00" transactionFlow="false" transferMode="Buffered" transactionProtocol="OleTransactions" hostNameComparisonMode="StrongWildcard" listenBacklog="10" maxBufferPoolSize="524288" maxBufferSize="65536" maxConnections="11" maxReceivedMessageSize="65536">  
      <readerQuotas maxDepth="32" maxStringContentLength="8192" maxArrayLength="16384" maxBytesPerRead="4096" maxNameTableCharCount="16384"/>  
      <reliableSession ordered="true" inactivityTimeout="00:10:00" enabled="false"/>  
      <security mode="Transport">  
        <transport clientCredentialType="Windows" protectionLevel="EncryptAndSign"/>  
      </security>  
    </binding>  
  </netTcpBinding>  
</bindings>  
```  
  
 Verá un error similar al siguiente: Excepción no controlada: System.ServiceModel.AddressAlreadyInUseException: Ya hay un agente de escucha en 0.0.0.0:9000 de punto de conexión IP que puede evitar este error especificando una dirección URL completa con un puerto diferente para el extremo MEX, como se muestra en el siguiente fragmento de código de configuración:  
  
```xml
<services>  
  <service name="Microsoft.Samples.NetTcp.CalculatorService">  
    <endpoint address="calcsvc" binding ="netTcpBinding" contract="Microsoft.Samples.NetTcp.ICalculator"/>  
    <endpoint address="net.tcp://localhost:9001/servicemodelsamples/mex" binding="mexTcpBinding" contract="IMetadataExchange" />  
  </service>  
</services>  
```  
  
<a name="BK_MK99"></a>   
## <a name="when-calling-a-wcf-web-http-application-from-a-wcf-soap-application-the-service-returns-the-following-error-405-method-not-allowed"></a>Al llamar a una aplicación Web HTTP de WCF desde una aplicación SOAP de WCF el servicio devuelve el error siguiente: 405 método no permitido  
 Llamar a una aplicación Web HTTP de WCF (un servicio que utiliza el <xref:System.ServiceModel.WebHttpBinding> y <xref:System.ServiceModel.Description.WebHttpBehavior>) desde un WCF service puede generar la excepción siguiente: `Unhandled Exception: System.ServiceModel.FaultException`1[System.ServiceModel.ExceptionDetail]: El servidor remoto devolvió una respuesta inesperada: (405) método no permitido.' esta excepción se produce porque WCF sobrescribe el saliente <xref:System.ServiceModel.OperationContext> con entrante <xref:System.ServiceModel.OperationContext>. Para resolver este problema cree un <xref:System.ServiceModel.OperationContextScope> dentro de la operación del servicio web HTTP de WCF. Por ejemplo:  
  
```csharp
public string Echo(string input)  
{  
    using (new OperationContextScope(this.InnerChannel))  
    {  
        return base.Channel.Echo(input);  
    }  
}  
```  
  
## <a name="see-also"></a>Vea también

- [Depuración de errores de autenticación de Windows](../../../docs/framework/wcf/feature-details/debugging-windows-authentication-errors.md)
