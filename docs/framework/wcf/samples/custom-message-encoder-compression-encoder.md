---
title: 'Codificador de mensajes personalizado: codificador de compresión'
ms.date: 03/30/2017
ms.assetid: 57450b6c-89fe-4b8a-8376-3d794857bfd7
ms.openlocfilehash: d5ec330fb4aa0a136c4a0e4c8d249d7ebb9d0692
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2019
ms.locfileid: "64650200"
---
# <a name="custom-message-encoder-compression-encoder"></a>Codificador de mensajes personalizado: codificador de compresión
Este ejemplo muestra cómo implementar un codificador personalizado mediante la plataforma de Windows Communication Foundation (WCF).  
  
> [!IMPORTANT]
>  Puede que los ejemplos ya estén instalados en su equipo. Compruebe el siguiente directorio (predeterminado) antes de continuar.  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  Si no existe este directorio, vaya a [Windows Communication Foundation (WCF) y Windows Workflow Foundation (WF) Samples para .NET Framework 4](https://go.microsoft.com/fwlink/?LinkId=150780) para descargar todos los Windows Communication Foundation (WCF) y [!INCLUDE[wf1](../../../../includes/wf1-md.md)] ejemplos. Este ejemplo se encuentra en el siguiente directorio.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\MessageEncoder\Compression`  
  
## <a name="sample-details"></a>Detalles del ejemplo  
 Este ejemplo está compuesto de un programa de consola de cliente (.exe), un programa de consola de servicio autohospedado (.exe) y una biblioteca de codificador del mensaje de compresión (.dll). El servicio implementa un contrato que define un modelo de comunicación de solicitud y respuesta. El contrato está definido por la interfaz `ISampleServer`, que expone las operaciones de eco de cadena básica (`Echo` y `BigEcho`). El cliente realiza solicitudes sincrónicas a una operación determinada y el servicio responde repitiendo el mensaje en el cliente. La actividad del cliente y el servicio está visible en las ventanas de la consola. El intento de este ejemplo es mostrar cómo escribir un codificador personalizado y mostrar el impacto de compresión de un mensaje en la conexión. Puede agregar la instrumentación al codificador del mensaje de compresión para calcular el tamaño del mensaje, el tiempo de procesamiento o ambos.  
  
> [!NOTE]
>  En .NET Framework 4, se habilitó la descompresión automática en un cliente WCF si el servidor envía una respuesta cifrada (creada con un algoritmo como GZip o Deflate). Si el servicio se hospeda en web en Internet Information Server (IIS), IIS se puede configurar para que el servicio envíe una respuesta cifrada. Se puede utilizar este ejemplo si se tiene que llevar a cabo la compresión y la descompresión tanto en el cliente como en el servicio, o si el servicio se auto-hospeda.  
  
 El ejemplo muestra cómo crear e integrar un codificador de mensajes personalizados en una aplicación de WCF. GZipEncoder.dll de la biblioteca se implementa tanto en el cliente como en el servicio. Este ejemplo también muestra el impacto de comprimir mensajes. El código en GZipEncoder.dll muestra lo siguiente:  
  
- Compilar un codificador personalizado y un generador de codificadores.  
  
- Desarrollar un elemento de enlace para un codificador personalizado.  
  
- Utilizar la configuración de enlace personalizado para integrar los elementos de enlace personalizado.  
  
- Desarrollar un controlador de configuración personalizado para permitir la configuración del archivo de un elemento de enlace personalizado.  
  
 Tal y como se ha indicado previamente, hay varios niveles que se implementan en un codificador personalizado. Para mostrar mejor la relación entre cada uno de estos niveles, hay un orden simplificado de eventos para el inicio del servicio en la lista siguiente:  
  
1. El servidor se inicia.  
  
2. Se lee la información de configuración.  
  
    1. La configuración de servicio registra el controlador de configuración personalizado.  
  
    2. El host del servicio se crea y se abre.  
  
    3. El elemento de configuración personalizado crea y devuelve el elemento de enlace personalizado.  
  
    4. El elemento de enlace personalizado crea y devuelve el generador de codificadores de mensajes.  
  
3. Se recibe un mensaje.  
  
4. El generador de codificadores de mensajes devuelve un codificador de mensaje para leer en el mensaje y escribir la respuesta.  
  
5. El nivel del codificador se implementa como un generador de clases. Sólo se debe exponer públicamente el generador de clases del codificador para el codificador personalizado. El elemento de enlace devuelve el objeto del generador cuando se crea el objeto <xref:System.ServiceModel.ServiceHost> o <xref:System.ServiceModel.ChannelFactory%601>. Los codificadores de mensaje pueden funcionar en un modo almacenado en búfer o en un modo de transmisión por secuencias. Este ejemplo muestra ambos modos.  
  
 Para cada modo hay un método `ReadMessage` y `WriteMessage` acompañante en la clase `MessageEncoder` abstracta. Una mayoría del trabajo de codificación tiene lugar en estos métodos. El ejemplo ajusta el texto existente y los codificadores de mensaje binarios. Esto permite al ejemplo delegar la lectura y escritura de la representación de la conexión de mensajes en el codificador interno y permite al codificador de compresión comprimir o descomprimir los resultados. Dado que no hay ningún conductor para la codificación de mensajes, este es el único modelo para utilizar varios codificadores en WCF. Una vez descomprimido el mensaje, el mensaje resultante se pasa a la pila para que lo gestione la pila de canales. Durante la compresión, el mensaje comprimido resultante se escribe directamente en la secuencia proporcionada.  
  
 Este ejemplo utiliza los métodos del asistente (`CompressBuffer` y `DecompressBuffer`) para realizar la conversión de los búferes a secuencias para utilizar la clase `GZipStream`.  
  
 Las clases `ReadMessage` y `WriteMessage` almacenadas en búfer hacen uso de la clase `BufferManager`. Sólo se puede acceder al codificador mediante el generador de codificadores. La clase `MessageEncoderFactory` abstracta proporciona una propiedad denominada `Encoder` para tener acceso al codificador actual y a un método denominado `CreateSessionEncoder` para crear un codificador que admite sesiones. Este tipo de codificador se puede utilizar en el escenario donde el canal admite las sesiones, se ordena y es confiable. Este escenario permite la optimización en cada sesión de los datos escritos en la conexión. Si no es esto lo que se desea, no se debería sobrecargar el método base. La propiedad `Encoder` proporciona un mecanismo para tener acceso al codificador sin sesión. La implementación predeterminada del método `CreateSessionEncoder` devuelve el valor de la propiedad. Dado que el ejemplo ajusta un codificador existente para proporcionar la compresión, la implementación `MessageEncoderFactory` acepta `MessageEncoderFactory` que representa el generador de codificadores interno.  
  
 Ahora que el codificador y el generador de codificadores se definen, se puede usar con un cliente y servicio WCF. Sin embargo, se deben agregar estos codificadores a la pila de canales. Puede derivar las clases <xref:System.ServiceModel.ServiceHost> y <xref:System.ServiceModel.ChannelFactory%601> e invalidar los métodos `OnInitialize` para agregar manualmente este generador de codificadores. También puede exponer el generador de codificadores a través de un elemento de enlace personalizado.  
  
 Para crear un nuevo elemento de enlace personalizado, derive una clase desde la clase <xref:System.ServiceModel.Channels.BindingElement>. Hay, sin embargo, varios tipos de elementos de enlace. Para garantizar que el elemento de enlace personalizado se reconozca como un elemento de enlace de la codificación de mensajes, debe implementar también <xref:System.ServiceModel.Channels.MessageEncodingBindingElement>. <xref:System.ServiceModel.Channels.MessageEncodingBindingElement> expone un método para crear un nuevo generador de codificadores de mensajes (`CreateMessageEncoderFactory`), que se implementa para devolver una instancia del generador de codificadores de mensajes correspondiente. Además, <xref:System.ServiceModel.Channels.MessageEncodingBindingElement> tiene una propiedad para indicar la versión de direccionamiento. Dado que este ejemplo ajusta los codificadores existentes, la implementación del ejemplo también ajusta los elementos de enlace del codificador existentes y lleva un elemento de enlace del codificador interno como un parámetro al constructor y lo expone mediante una propiedad. El código de ejemplo siguiente muestra la implementación de la clase `GZipMessageEncodingBindingElement`.  
  
```  
public sealed class GZipMessageEncodingBindingElement   
                        : MessageEncodingBindingElement //BindingElement  
                        , IPolicyExportExtension  
{  
  
    //We use an inner binding element to store information   
    //required for the inner encoder.  
    MessageEncodingBindingElement innerBindingElement;  
  
        //By default, use the default text encoder as the inner encoder.  
        public GZipMessageEncodingBindingElement()  
            : this(new TextMessageEncodingBindingElement()) { }  
  
    public GZipMessageEncodingBindingElement(MessageEncodingBindingElement messageEncoderBindingElement)  
    {  
        this.innerBindingElement = messageEncoderBindingElement;  
    }  
  
    public MessageEncodingBindingElement InnerMessageEncodingBindingElement  
    {  
        get { return innerBindingElement; }  
        set { innerBindingElement = value; }  
    }  
  
    //Main entry point into the encoder binding element.   
    // Called by WCF to get the factory that creates the  
    //message encoder.  
    public override MessageEncoderFactory CreateMessageEncoderFactory()  
    {  
        return new   
GZipMessageEncoderFactory(innerBindingElement.CreateMessageEncoderFactory());  
    }  
  
    public override MessageVersion MessageVersion  
    {  
        get { return innerBindingElement.MessageVersion; }  
        set { innerBindingElement.MessageVersion = value; }  
    }  
  
    public override BindingElement Clone()  
    {  
        return new   
        GZipMessageEncodingBindingElement(this.innerBindingElement);  
    }  
  
    public override T GetProperty<T>(BindingContext context)  
    {  
        if (typeof(T) == typeof(XmlDictionaryReaderQuotas))  
        {  
            return innerBindingElement.GetProperty<T>(context);  
        }  
        else   
        {  
            return base.GetProperty<T>(context);  
        }  
    }  
  
    public override IChannelFactory<TChannel> BuildChannelFactory<TChannel>(BindingContext context)  
    {  
        if (context == null)  
            throw new ArgumentNullException("context");  
  
        context.BindingParameters.Add(this);  
        return context.BuildInnerChannelFactory<TChannel>();  
    }  
  
    public override IChannelListener<TChannel> BuildChannelListener<TChannel>(BindingContext context)  
    {  
        if (context == null)  
            throw new ArgumentNullException("context");  
  
        context.BindingParameters.Add(this);  
        return context.BuildInnerChannelListener<TChannel>();  
    }  
  
    public override bool CanBuildChannelListener<TChannel>(BindingContext context)  
    {  
        if (context == null)  
            throw new ArgumentNullException("context");  
  
        context.BindingParameters.Add(this);  
        return context.CanBuildInnerChannelListener<TChannel>();  
    }  
  
    void IPolicyExportExtension.ExportPolicy(MetadataExporter exporter, PolicyConversionContext policyContext)  
    {  
        if (policyContext == null)  
        {  
            throw new ArgumentNullException("policyContext");  
        }  
       XmlDocument document = new XmlDocument();  
       policyContext.GetBindingAssertions().Add(document.CreateElement(  
            GZipMessageEncodingPolicyConstants.GZipEncodingPrefix,  
            GZipMessageEncodingPolicyConstants.GZipEncodingName,  
            GZipMessageEncodingPolicyConstants.GZipEncodingNamespace));  
    }  
}  
```  
  
 Observe que la clase `GZipMessageEncodingBindingElement` implementa la interfaz `IPolicyExportExtension`, para que este elemento de enlace se pueda exportar como una directiva en metadatos, tal y como se muestra en el ejemplo siguiente.  
  
```xml  
<wsp:Policy wsu:Id="BufferedHttpSampleServer_ISampleServer_policy">  
    <wsp:ExactlyOne>  
      <wsp:All>  
        <gzip:text xmlns:gzip=  
        "http://schemas.microsoft.com/ws/06/2004/mspolicy/netgzip1" />   
       <wsaw:UsingAddressing />   
     </wsp:All>  
   </wsp:ExactlyOne>  
</wsp:Policy>  
```  
  
 La clase `GZipMessageEncodingBindingElementImporter` implementa la interfaz `IPolicyImportExtension` Esta clase importa la directiva para `GZipMessageEncodingBindingElement`. La herramienta Svcutil.exe se puede utilizar para importar las directivas al archivo de configuración. Para administrar `GZipMessageEncodingBindingElement`, se debería agregar lo siguiente a Svcutil.exe.config.  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <extensions>  
      <bindingElementExtensions>  
        <add name="gzipMessageEncoding"   
          type=  
            "Microsoft.ServiceModel.Samples.GZipMessageEncodingElement, GZipEncoder, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />  
      </bindingElementExtensions>  
    </extensions>  
    <client>  
      <metadata>  
        <policyImporters>  
          <remove type=  
"System.ServiceModel.Channels.MessageEncodingBindingElementImporter, System.ServiceModel, Version=3.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />  
          <extension type=  
"Microsoft.ServiceModel.Samples.GZipMessageEncodingBindingElementImporter, GZipEncoder, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />  
        </policyImporters>  
      </metadata>  
    </client>  
  </system.serviceModel>  
</configuration>  
```  
  
 Ahora que hay un elemento de enlace correspondiente para el codificador de compresión, se puede enlazar mediante programación con el servicio o cliente construyendo un nuevo objeto de enlace personalizado y agregando el elemento de enlace personalizado a él, tal y como se muestra en el código de ejemplo siguiente.  
  
```  
ICollection<BindingElement> bindingElements = new List<BindingElement>();  
HttpTransportBindingElement httpBindingElement = new HttpTransportBindingElement();  
GZipMessageEncodingBindingElement compBindingElement = new GZipMessageEncodingBindingElement ();  
bindingElements.Add(compBindingElement);  
bindingElements.Add(httpBindingElement);  
CustomBinding binding = new CustomBinding(bindingElements);  
binding.Name = "SampleBinding";  
binding.Namespace = "http://tempuri.org/bindings";  
```  
  
 Aunque esto puede ser suficiente para la mayoría de escenarios de usuario, ser compatible con una configuración de archivo es fundamental si se hospeda en web un servicio. Para admitir el escenario hospedado en web, debe desarrollar un controlador de configuración personalizado para permitir que se configure un elemento de enlace personalizado en un archivo.  
  
 Puede crear un controlador de configuración para el elemento de enlace encima del sistema de configuración que proporciona [!INCLUDE[dnprdnlong](../../../../includes/dnprdnlong-md.md)]. El controlador de configuración para el elemento de enlace debe derivar de la clase <xref:System.ServiceModel.Configuration.BindingElementExtensionElement>. Se usa la propiedad `BindingElementType` para informar al sistema de configuración del tipo de elemento de enlace que se va a crear para esta sección. Todos los aspectos de `BindingElement` que se pueden establecer se deberían exponer como propiedades en la clase derivada <xref:System.ServiceModel.Configuration.BindingElementExtensionElement>. <xref:System.Configuration.ConfigurationPropertyAttribute> se utiliza para ayudar a asignar los atributos de elemento de configuración a las propiedades y a definir valores predeterminados si faltan los atributos. Después de cargar y aplicar los valores de configuración a las propiedades, se llama al método <xref:System.ServiceModel.Configuration.BindingElementExtensionElement.CreateBindingElement%2A>, que convierte las propiedades en una instancia concreta de un elemento de enlace. El método <xref:System.ServiceModel.Configuration.BindingElementExtensionElement.ApplyConfiguration%2A> se usa para convertir las propiedades de la clase derivada <xref:System.ServiceModel.Configuration.BindingElementExtensionElement> en los valores que se van a definir en el elemento de enlace creado recientemente.  
  
 En el siguiente código de ejemplo muestra la implementación de `GZipMessageEncodingElement`.  
  
```  
public class GZipMessageEncodingElement : BindingElementExtensionElement  
{  
    public GZipMessageEncodingElement()  
    {  
    }  
  
//Called by the WCF to discover the type of binding element this   
//config section enables  
    public override Type BindingElementType  
    {  
        get { return typeof(GZipMessageEncodingBindingElement); }  
    }  
  
    //The only property we need to configure for our binding element is   
    //the type of inner encoder to use. Here, we support text and  
    //binary.  
    [ConfigurationProperty("innerMessageEncoding",   
                         DefaultValue = "textMessageEncoding")]  
    public string InnerMessageEncoding  
    {  
        get { return (string)base["innerMessageEncoding"]; }  
        set { base["innerMessageEncoding"] = value; }  
    }  
  
    //Called by the WCF to apply the configuration settings (the   
    //property above) to the binding element  
    public override void ApplyConfiguration(BindingElement bindingElement)  
    {  
        GZipMessageEncodingBindingElement binding =   
                (GZipMessageEncodingBindingElement)bindingElement;  
        PropertyInformationCollection propertyInfo =   
                    this.ElementInformation.Properties;  
        if (propertyInfo["innerMessageEncoding"].ValueOrigin !=   
                                     PropertyValueOrigin.Default)  
        {  
            switch (this.InnerMessageEncoding)  
            {  
                case "textMessageEncoding":  
                    binding.InnerMessageEncodingBindingElement =   
                      new TextMessageEncodingBindingElement();  
                    break;  
                case "binaryMessageEncoding":  
                    binding.InnerMessageEncodingBindingElement =   
                         new BinaryMessageEncodingBindingElement();  
                    break;  
            }  
        }  
    }  
  
    //Called by the WCF to create the binding element  
    protected override BindingElement CreateBindingElement()  
    {  
        GZipMessageEncodingBindingElement bindingElement =   
                new GZipMessageEncodingBindingElement();  
        this.ApplyConfiguration(bindingElement);  
        return bindingElement;  
    }  
}   
```  
  
 Este controlador de configuración asigna a la representación siguiente en App.config o Web.config para el servicio o cliente.  
  
```xml  
<gzipMessageEncoding innerMessageEncoding="textMessageEncoding" />  
```  
  
 Para utilizar este controlador de configuración, debe registrarse en el [ \<system.serviceModel >](../../../../docs/framework/configure-apps/file-schema/wcf/system-servicemodel.md) elemento, como se muestra en el siguiente ejemplo de configuración.  
  
```xml  
<extensions>  
    <bindingElementExtensions>  
       <add   
           name="gzipMessageEncoding"   
           type=  
           "Microsoft.ServiceModel.Samples.GZipMessageEncodingElement,  
           GZipEncoder, Version=1.0.0.0, Culture=neutral,   
           PublicKeyToken=null" />  
      </bindingElementExtensions>  
</extensions>  
```  
  
 Al ejecutar el servidor, las solicitudes y respuestas de la operación se muestran en la ventana de la consola. Presione ENTRAR en la ventana para cerrar el servidor.  
  
```  
Press Enter key to Exit.  
  
        Server Echo(string input) called:  
        Client message: Simple hello  
  
        Server BigEcho(string[] input) called:  
        64 client messages  
```  
  
 Al ejecutar el cliente, las solicitudes y respuestas de la operación se muestran en la ventana de la consola. Presione ENTRAR en la ventana de cliente para cerrar el cliente.  
  
```  
Calling Echo(string):  
Server responds: Simple hello Simple hello  
  
Calling BigEcho(string[]):  
Server responds: Hello 0  
  
Press <ENTER> to terminate client.  
```  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>Configurar, compilar y ejecutar el ejemplo  
  
1. Instale [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 4.0 mediante el siguiente comando:  
  
    ```  
    %windir%\Microsoft.NET\Framework\v4.0.XXXXX\aspnet_regiis.exe /i /enable  
    ```  
  
2. Asegúrese de que ha realizado la [procedimiento de instalación de un solo uso para los ejemplos de Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
3. Para compilar la solución, siga las instrucciones de [compilar los ejemplos de Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
4. Para ejecutar el ejemplo en una configuración de equipos única o cruzada, siga las instrucciones de [ejecutando los ejemplos de Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
> [!IMPORTANT]
>  Puede que los ejemplos ya estén instalados en su equipo. Compruebe el siguiente directorio (predeterminado) antes de continuar.  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  Si no existe este directorio, vaya a [Windows Communication Foundation (WCF) y Windows Workflow Foundation (WF) Samples para .NET Framework 4](https://go.microsoft.com/fwlink/?LinkId=150780) para descargar todos los Windows Communication Foundation (WCF) y [!INCLUDE[wf1](../../../../includes/wf1-md.md)] ejemplos. Este ejemplo se encuentra en el siguiente directorio.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\MessageEncoder\Compression`  
