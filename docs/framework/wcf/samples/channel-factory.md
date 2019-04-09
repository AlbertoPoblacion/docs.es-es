---
title: Generador de canales
ms.date: 03/30/2017
ms.assetid: 09b53aa1-b13c-476c-a461-e82fcacd2a8b
ms.openlocfilehash: 8e04dd762e0abad7796d90aff5615134ba22539c
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2019
ms.locfileid: "59119735"
---
# <a name="channel-factory"></a>Generador de canales
Este ejemplo muestra cómo una aplicación cliente puede crear un canal con la clase <xref:System.ServiceModel.ChannelFactory> en lugar de un cliente generado. En este ejemplo se basa en el [Introducción](../../../../docs/framework/wcf/samples/getting-started-sample.md) que implementa un servicio de calculadora.  
  
> [!NOTE]
>  El procedimiento de instalación y las instrucciones de compilación de este ejemplo se encuentran al final de este tema.  
  
 Este ejemplo utiliza la clase <xref:System.ServiceModel.ChannelFactory%601> para crear un canal a un extremo de servicio. Normalmente, para crear un canal a un extremo de servicio genera un tipo de cliente con el [ServiceModel Metadata Utility Tool (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) y cree una instancia del tipo generado. También puede crear un canal utilizando la clase <xref:System.ServiceModel.ChannelFactory%601>, tal y como se muestra en este ejemplo. El servicio creado por el código de ejemplo siguiente es idéntico al servicio en la [Introducción](../../../../docs/framework/wcf/samples/getting-started-sample.md).  
  
```csharp  
EndpointAddress address = new EndpointAddress("http://localhost/servicemodelsamples/service.svc");  
WSHttpBinding binding = new WSHttpBinding();  
ChannelFactory<ICalculator> factory = new   
                    ChannelFactory<ICalculator>(binding, address);  
ICalculator channel = factory.CreateChannel();  
```  
  
> [!IMPORTANT]
>  Si está ejecutando este ejemplo en un escenario con varios equipos, debe reemplazar el "host local" en el código anterior con el nombre completo del equipo que está ejecutando el servicio. Este ejemplo no utiliza la configuración para establecer la dirección del punto de conexión, por lo que se debe hacer en el código.  
  
 Una vez creado el canal, se pueden invocar operaciones de servicio de la misma manera que con un cliente generado.  
  
```csharp  
// Call the Add service operation.  
double value1 = 100.00D;  
double value2 = 15.99D;  
double result = channel.Add(value1, value2);  
Console.WriteLine("Add({0},{1}) = {2}", value1, value2, result);  
```  
  
 Para cerrar el canal, se debe convertir primero a una interfaz <xref:System.ServiceModel.IClientChannel>. Esto es porque cuando se genera el canal se declara en la aplicación cliente utilizando la interfaz `ICalculator`, que cuenta con métodos como `Add` y `Subtract` pero no `Close`. El método `Close` se origina en la interfaz <xref:System.ServiceModel.ICommunicationObject>.  
  
```csharp  
// Close the channel.  
 ((IClientChannel)client).Close();  
```  
  
 Al ejecutar el ejemplo, las solicitudes y respuestas de la operación se muestran en la ventana de la consola del cliente. Presione ENTRAR en la ventana de cliente para cerrar la aplicación del cliente.  
  
```  
Add(100,15.99) = 115.99  
Subtract(145,76.54) = 68.46  
Multiply(9,81.25) = 731.25  
Divide(22,7) = 3.14285714285714  
  
Press <ENTER> to terminate client.  
```  
  
### <a name="to-set-up-build-and-run-the-sample"></a>Configurar, compilar y ejecutar el ejemplo  
  
1.  Asegúrese de que ha realizado la [procedimiento de instalación de un solo uso para los ejemplos de Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Para compilar el código C# o Visual Basic .NET Edition de la solución, siga las instrucciones de [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md). Observe que este ejemplo no permite la publicación de metadatos. Debe habilitarla primero para este ejemplo con objeto de regenerar el tipo de cliente.  
  
3.  Para ejecutar el ejemplo en una configuración de equipos única o cruzada, siga las instrucciones de [ejecutando los ejemplos de Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
### <a name="to-run-the-sample-cross-machine"></a>Para ejecutar el ejemplo en varios equipos  
  
1.  Reemplace el "host local" en el código siguiente con el nombre completo del equipo que está ejecutando el servicio.  
  
    ```csharp  
    EndpointAddress address = new EndpointAddress("http://localhost/servicemodelsamples/service.svc");  
    ```  
  
> [!IMPORTANT]
>  Puede que los ejemplos ya estén instalados en su equipo. Compruebe el siguiente directorio (predeterminado) antes de continuar.  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  Si no existe este directorio, vaya a [Windows Communication Foundation (WCF) y Windows Workflow Foundation (WF) Samples para .NET Framework 4](https://go.microsoft.com/fwlink/?LinkId=150780) para descargar todos los Windows Communication Foundation (WCF) y [!INCLUDE[wf1](../../../../includes/wf1-md.md)] ejemplos. Este ejemplo se encuentra en el siguiente directorio.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Client\ChannelFactory`  
