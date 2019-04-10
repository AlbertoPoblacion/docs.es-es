---
title: Acceso a los servicios mediante un cliente WCF
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- clients [WCF], consuming services
ms.assetid: d780af9f-73c5-42db-9e52-077a5e4de7fe
ms.openlocfilehash: 6bf683cdd0a03a5d1dbc452c28e7b33911464f09
ms.sourcegitcommit: 558d78d2a68acd4c95ef23231c8b4e4c7bac3902
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/09/2019
ms.locfileid: "59297257"
---
# <a name="accessing-services-using-a-wcf-client"></a>Acceso a los servicios mediante un cliente WCF

Después de crear un servicio, el siguiente paso es crear a un proxy de cliente WCF. Una aplicación cliente usa al proxy de cliente WCF para comunicarse con el servicio. Las aplicaciones cliente suelen importación los metadatos del servicio para generar código de cliente WCF que se puede usar para invocar el servicio.

 Los pasos básicos para crear a un cliente de WCF incluyen lo siguiente:

1. Compilar el código del servicio.

2. Generar al proxy de cliente WCF.

3. Cree una instancia del proxy de cliente de WCF.

El proxy de cliente WCF puede generarse manualmente mediante el uso de Service Model Metadata Utility Tool (SvcUtil.exe) para obtener más información, vea [ServiceModel Metadata Utility Tool (Svcutil.exe)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md). También se puede generar el proxy de cliente WCF dentro de Visual Studio mediante el **Add Service Reference** característica. Para generar el proxy de cliente de WCF usando cualquier método, el servicio debe estar en ejecución. Si el servicio se autohospeda, debe ejecutar el host. Si el servicio se hospeda en IIS/WAS no necesita hacer nada más.

## <a name="servicemodel-metadata-utility-tool"></a>Herramienta de utilidad de metadatos ServiceModel
 El [ServiceModel Metadata Utility Tool (Svcutil.exe)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) es una herramienta de línea de comandos para generar código a partir de los metadatos. A continuación se muestra un ejemplo del uso de un comando básico Svcutil.exe.

```
Svcutil.exe <service's Metadata Exchange (MEX) address or HTTP GET address>
```

 Como alternativa, puede usar Svcutil.exe con archivos de Lenguaje de descripción de servicios Web (WSDL) y de lenguaje de definición de esquemas XML (XSD) en el sistema de archivos.

```
Svcutil.exe <list of WSDL and XSD files on file system>
```

 El resultado es un archivo de código que contiene el código de cliente WCF que la aplicación cliente puede utilizar para invocar el servicio.

 También puede usar la herramienta para generar archivos de configuración.

```
Svcutil.exe <file1 [,file2]>
```

 Si se proporciona solo uno nombre de archivo, ése será el nombre del archivo de salida. Si se proporcionan dos nombres de archivo, entonces el primer archivo es un archivo de configuración de entrada cuyo contenido está combinado con la configuración generada y que se escribe en el segundo archivo. Para obtener más información acerca de la configuración, consulte [configurar enlaces para los servicios](../../../docs/framework/wcf/configuring-bindings-for-wcf-services.md).

> [!IMPORTANT]
> Las solicitudes de metadatos no seguras plantean ciertos riesgos en la misma forma que cualquier solicitud de red no segura: Si no está seguro de que se comunican con el punto de conexión es quien dice ser, la información que recupere posible los metadatos de un servicio malintencionado.

## <a name="add-service-reference-in-visual-studio"></a>Agregar referencia de servicio en Visual Studio

 Con el servicio en ejecución, a la derecha, haga clic en el proyecto que contendrá el proxy de cliente WCF y seleccione **agregar** > **referencia de servicio**. En el **Agregar cuadro de diálogo de referencia de servicio**, escriba la dirección URL para el servicio que desea llamar y haga clic en el **vaya** botón. El cuadro de diálogo mostrará una lista de servicios disponibles en la dirección especificada. Haga doble clic en el servicio para ver los contratos y operaciones disponibles, especifique un espacio de nombres para el código generado y haga clic en el **Aceptar** botón.

## <a name="example"></a>Ejemplo
 El ejemplo de código siguiente muestra un contrato de servicio creado para un servicio.

```csharp
// Define a service contract.
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples")]
public interface ICalculator
{
    [OperationContract]
    double Add(double n1, double n2);
    // Other methods are not shown here.
}
```

```vb
' Define a service contract.
<ServiceContract(Namespace:="http://Microsoft.ServiceModel.Samples")> _
Public Interface ICalculator
    <OperationContract()>  _
    Function Add(ByVal n1 As Double, ByVal n2 As Double) As Double
    ' Other methods are not shown here.
End Interface
```

 La herramienta de utilidad Metadata de ServiceModel y **Add Service Reference** en Visual Studio genera la siguiente clase de cliente WCF. La clase adquiere de la clase <xref:System.ServiceModel.ClientBase%601> genérica e implementa la interfaz `ICalculator`. La herramienta también genera la interfaz (no se muestra aquí) `ICalculator`.

```csharp
public partial class CalculatorClient : System.ServiceModel.ClientBase<ICalculator>, ICalculator
{
    public CalculatorClient()
    {}

    public CalculatorClient(string endpointConfigurationName) :
            base(endpointConfigurationName)
    {}

    public CalculatorClient(string endpointConfigurationName, string remoteAddress) :
            base(endpointConfigurationName, remoteAddress)
    {}

    public CalculatorClient(string endpointConfigurationName,
        System.ServiceModel.EndpointAddress remoteAddress) :
            base(endpointConfigurationName, remoteAddress)
    {}

    public CalculatorClient(System.ServiceModel.Channels.Binding binding,
        System.ServiceModel.EndpointAddress remoteAddress) :
            base(binding, remoteAddress)
    {}

    public double Add(double n1, double n2)
    {
        return base.Channel.Add(n1, n2);
    }
}
```

```vb
Partial Public Class CalculatorClient
    Inherits System.ServiceModel.ClientBase(Of ICalculator)
    Implements ICalculator

    Public Sub New()
        MyBase.New
    End Sub

    Public Sub New(ByVal endpointConfigurationName As String)
        MyBase.New(endpointConfigurationName)
    End Sub

    Public Sub New(ByVal endpointConfigurationName As String, ByVal remoteAddress As String)
        MyBase.New(endpointConfigurationName, remoteAddress)
    End Sub

    Public Sub New(ByVal endpointConfigurationName As String,
        ByVal remoteAddress As System.ServiceModel.EndpointAddress)
        MyBase.New(endpointConfigurationName, remoteAddress)
    End Sub

    Public Sub New(ByVal binding As System.ServiceModel.Channels.Binding,
        ByVal remoteAddress As System.ServiceModel.EndpointAddress)
        MyBase.New(binding, remoteAddress)
    End Sub

    Public Function Add(ByVal n1 As Double, ByVal n2 As Double) As Double
        Implements ICalculator.Add
        Return MyBase.Channel.Add(n1, n2)
    End Function
End Class
```

## <a name="using-the-wcf-client"></a>Uso del cliente WCF
 Para usar al cliente de WCF, cree una instancia del cliente WCF y, a continuación, llamar a sus métodos, como se muestra en el código siguiente.

```csharp
// Create a client object with the given client endpoint configuration.
CalculatorClient calcClient = new CalculatorClient("CalculatorEndpoint"));
// Call the Add service operation.
double value1 = 100.00D;
double value2 = 15.99D;
double result = calcClient.Add(value1, value2);
Console.WriteLine("Add({0},{1}) = {2}", value1, value2, result);
```

```vb
' Create a client object with the given client endpoint configuration.
Dim calcClient As CalculatorClient = _
New CalculatorClient("CalculatorEndpoint")

' Call the Add service operation.
Dim value1 As Double = 100.00D
Dim value2 As Double = 15.99D
Dim result As Double = calcClient.Add(value1, value2)
Console.WriteLine("Add({0},{1}) = {2}", value1, value2, result)
```

## <a name="debugging-exceptions-thrown-by-a-client"></a>Depuración de las excepciones iniciadas por un cliente

Muchas de las excepciones iniciadas por un cliente WCF están provocados por una excepción en el servicio. Estos son algunos ejemplos:

-   <xref:System.Net.Sockets.SocketException>: El host remoto cerró fuerza una conexión existente.

-   <xref:System.ServiceModel.CommunicationException>: La conexión subyacente se cerró inesperadamente.

-   <xref:System.ServiceModel.CommunicationObjectAbortedException>: Se anuló la conexión de socket. La causa puede ser un error en el procesamiento del mensaje, que se superó el tiempo de espera de recepción en el host remoto, o bien un problema de recursos de red subyacente.

Cuando se producen estos tipos de excepciones, la mejor manera de resolver el problema es activar el seguimiento en el lado del servicio y determinar qué excepción se produjo allí. Para obtener más información acerca del seguimiento, vea [seguimiento](../../../docs/framework/wcf/diagnostics/tracing/index.md) y [utilizando seguimiento de la solución de problemas de la aplicación](../../../docs/framework/wcf/diagnostics/tracing/using-tracing-to-troubleshoot-your-application.md).

## <a name="see-also"></a>Vea también

- [Filtrar Crear un cliente](../../../docs/framework/wcf/how-to-create-a-wcf-client.md)
- [Filtrar para obtener acceso a los servicios con un contrato dúplex](../../../docs/framework/wcf/feature-details/how-to-access-services-with-a-duplex-contract.md)
- [Filtrar para llamar a operaciones de servicio de forma asincrónica](../../../docs/framework/wcf/feature-details/how-to-call-wcf-service-operations-asynchronously.md)
- [Filtrar para obtener acceso a los servicios con contratos unidireccionales y de solicitud-respuesta](../../../docs/framework/wcf/feature-details/how-to-access-wcf-services-with-one-way-and-request-reply-contracts.md)
- [Filtrar para obtener acceso a un servicio WSE 3.0](../../../docs/framework/wcf/feature-details/how-to-access-a-wse-3-0-service-with-a-wcf-client.md)
- [Comprender códigos de cliente generado](../../../docs/framework/wcf/feature-details/understanding-generated-client-code.md)
- [Filtrar para mejorar el tiempo de inicio de las aplicaciones cliente WCF mediante XmlSerializer](../../../docs/framework/wcf/feature-details/startup-time-of-wcf-client-applications-using-the-xmlserializer.md)
- [Especificación del comportamiento de tiempo de ejecución del cliente](../../../docs/framework/wcf/specifying-client-run-time-behavior.md)
- [Configuración de los comportamientos del cliente](../../../docs/framework/wcf/configuring-client-behaviors.md)
