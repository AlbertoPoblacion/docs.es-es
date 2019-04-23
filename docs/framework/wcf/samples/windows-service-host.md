---
title: Host de servicio de Windows
ms.date: 03/30/2017
helpviewer_keywords:
- NT Service
- NT Service Host Sample [Windows Communication Foundation]
ms.assetid: 1b2f45c5-2bed-4979-b0ee-8f9efcfec028
ms.openlocfilehash: 85d089813a455784fde679e9200a9b29b956af8e
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59338701"
---
# <a name="windows-service-host"></a>Host de servicio de Windows
Este ejemplo muestra un servicio de Windows Communication Foundation (WCF) hospedado en un servicio de Windows administrado. Servicios de Windows se controlan mediante el applet Servicios en **Panel de Control** y pueden configurarse para iniciarse automáticamente tras un reinicio del sistema. El ejemplo está compuesto de un programa cliente y un programa de servicio de Windows. El servicio se implementa como un programa .exe y contiene su propio código de hospedaje. No es necesario que escriba el código de hospedaje en otros entornos de hospedaje, como los Servicios de activación de procesos de Windows (WAS) o Internet Information Services (IIS).

> [!NOTE]
>  El procedimiento de instalación y las instrucciones de compilación de este ejemplo se encuentran al final de este tema.

> [!IMPORTANT]
>  Puede que los ejemplos ya estén instalados en su equipo. Compruebe el siguiente directorio (predeterminado) antes de continuar.  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  Si no existe este directorio, vaya a [Windows Communication Foundation (WCF) y Windows Workflow Foundation (WF) Samples para .NET Framework 4](https://go.microsoft.com/fwlink/?LinkId=150780) para descargar todos los Windows Communication Foundation (WCF) y [!INCLUDE[wf1](../../../../includes/wf1-md.md)] ejemplos. Este ejemplo se encuentra en el siguiente directorio.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Services\Hosting\WindowsService`  
  
 Después de compilar este servicio, se debe instalar con la utilidad Installutil.exe como cualquier otro servicio de Windows. Si va a realizar cambios en el servicio, deberá desinstalarlo primero con `installutil /u`. Los archivos Setup.bat y Cleanup.bat incluidos en este ejemplo son los comandos para instalar e iniciar el servicio de Windows, y para apagar y desinstalar el servicio de Windows. El servicio de WCF solo puede responder a los clientes si se está ejecutando el servicio de Windows. Si detiene el servicio de Windows utilizando el applet Servicios en **Panel de Control** y ejecutar el cliente, un <xref:System.ServiceModel.EndpointNotFoundException> excepción se produce cuando un cliente intenta tener acceso al servicio. Si reinicia el servicio de Windows y vuelve a ejecutar el cliente, la comunicación se produce correctamente.  
  
 El código del servicio incluye una clase de instalador, una clase de implementación de servicio WCF que implementa el contrato de ICalculator y una clase de servicio de Windows que actúa como el host de tiempo de ejecución. La clase del instalador, que hereda de <xref:System.Configuration.Install.Installer>, permite instalar el programa como un servicio de NT por la herramienta Installutil.exe. La clase de implementación del servicio, `WcfCalculatorService`, es un servicio WCF que implementa un contrato de servicio básico. Este servicio WCF se hospeda dentro de una clase de servicio de Windows denominada `WindowsCalculatorService`. Para que sea calificada como un servicio de Windows, la clase hereda de <xref:System.ServiceProcess.ServiceBase> e implementa los métodos <xref:System.ServiceProcess.ServiceBase.OnStart%28System.String%5B%5D%29> y <xref:System.ServiceProcess.ServiceBase.OnStop>. En <xref:System.ServiceProcess.ServiceBase.OnStart%28System.String%5B%5D%29>, se crea un objeto <xref:System.ServiceModel.ServiceHost> para el tipo `WcfCalculatorService` y se abre. En <xref:System.ServiceProcess.ServiceBase.OnStop>, ServiceHost se cierra llamando al método <xref:System.ServiceModel.Channels.CommunicationObject.Close%28System.TimeSpan%29> del objeto <xref:System.ServiceModel.ServiceHost>. Dirección base del host se configura mediante el [ \<Agregar >](../../../../docs/framework/configure-apps/file-schema/wcf/add-of-baseaddresses.md) elemento, que es un elemento secundario de [ \<baseAddresses >](../../../../docs/framework/configure-apps/file-schema/wcf/baseaddresses.md), que es un elemento secundario de la [ \<host >](../../../../docs/framework/configure-apps/file-schema/wcf/host.md) elemento, que es un elemento secundario de la [ \<servicio >](../../../../docs/framework/configure-apps/file-schema/wcf/service.md) elemento.  
  
 El punto de conexión definida utiliza la dirección base y un [ \<wsHttpBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md). El ejemplo siguiente muestra la configuración de la dirección base así como el extremo que expone CalculatorService.  
  
```xml  
<services>  
  <service name="Microsoft.ServiceModel.Samples.WcfCalculatorService"  
           behaviorConfiguration="CalculatorServiceBehavior">  
    <host>  
      <baseAddresses>  
        <add baseAddress="http://localhost:8000/ServiceModelSamples/service"/>  
      </baseAddresses>  
    </host>  
    <!-- This endpoint is exposed at the base address provided by host: http://localhost:8000/ServiceModelSamples/service.  -->  
    <endpoint address=""  
              binding="wsHttpBinding"  
              contract="Microsoft.ServiceModel.Samples.ICalculator" />  
    ...  
  </service>  
</services>  
```  
  
 Al ejecutar el ejemplo, las solicitudes y las respuestas de operación se muestran tanto en la ventanas de la consola del cliente como del servicio. Presione Entrar en cada ventana de la consola para cerrar el servicio y el cliente.  
  
### <a name="to-set-up-build-and-run-the-sample"></a>Configurar, compilar y ejecutar el ejemplo  
  
1. Asegúrese de que ha realizado la [procedimiento de instalación de un solo uso para los ejemplos de Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2. Para compilar el código C# o Visual Basic .NET Edition de la solución, siga las instrucciones de [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3. Después de la solución se ha creado, ejecute Setup.bat desde una línea de comandos de Visual Studio 2012 con privilegios elevados para instalar el servicio de Windows mediante la herramienta Installutil.exe. El servicio debería aparecer en Servicios.  
  
4. Para ejecutar el ejemplo en una configuración de equipos única o cruzada, siga las instrucciones de [ejecutando los ejemplos de Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
## <a name="see-also"></a>Vea también

- [Ejemplos de persistencia y el hospedaje de AppFabric](https://go.microsoft.com/fwlink/?LinkId=193961)
