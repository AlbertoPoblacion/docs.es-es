---
title: Compatibilidad de ASP.NET
ms.date: 03/30/2017
ms.assetid: c8b51f1e-c096-4c42-ad99-0519887bbbc5
ms.openlocfilehash: a718b3f3bcbfd4bc2b74a14ba8f20cd8c335877f
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/22/2019
ms.locfileid: "69925278"
---
# <a name="aspnet-compatibility"></a>Compatibilidad de ASP.NET
Este ejemplo muestra cómo habilitar el modo de compatibilidad de ASP.NET en Windows Communication Foundation (WCF). Los servicios que se ejecutan en modo de compatibilidad ASP.net participan completamente en la canalización de la aplicación ASP.net y pueden usar características de ASP.net como la autorización de archivo <xref:System.Web.HttpContext> /URL, el estado de sesión y la clase. La <xref:System.Web.HttpContext> clase permite el acceso a las cookies, las sesiones y otras características de ASP.net. Este modo requiere que los enlaces utilicen el transporte HTTP y el propio servicio se debe hospedar en IIS.  
  
 En este ejemplo, el cliente es una aplicación de consola (un ejecutable) e Internet Information Servers (IIS) hospeda el servicio.  
  
> [!NOTE]
> El procedimiento de instalación y las instrucciones de compilación de este ejemplo se encuentran al final de este tema.  
  
En este ejemplo se requiere un grupo de aplicaciones de [!INCLUDE[netfx40_long](../../../../includes/netfx40-long-md.md)] para ejecutarse. Para crear un nuevo grupo de aplicaciones o modificar el grupo de aplicaciones predeterminado, siga estos pasos.  

1. Abra el **Panel de control**.  Abra el applet **herramientas administrativas** en el encabezado **sistema y seguridad** . Abra el applet **Administrador de Internet Information Services (IIS)** .  

2. Expanda la vista de árbol en el panel **conexiones** . Seleccione el nodo **grupos de aplicaciones** .  

3. Para establecer el grupo de aplicaciones predeterminado que [!INCLUDE[netfx40_long](../../../../includes/netfx40-long-md.md)] se va a usar (lo que puede provocar problemas de incompatibilidad con los sitios existentes), haga clic con el botón secundario en el elemento de lista **DefaultAppPool** y seleccione **configuración básica.** ... Establezca la desactivación de la **versión de .NET Framework** en **.NET Framework v 4.0.30128** (o posterior).  

4. Para crear un nuevo grupo de aplicaciones que [!INCLUDE[netfx40_long](../../../../includes/netfx40-long-md.md)] use (para conservar la compatibilidad con otras aplicaciones), haga clic con el botón secundario en el nodo **grupos de aplicaciones** y seleccione **Agregar grupo de aplicaciones**.... Asigne un nombre al nuevo grupo de aplicaciones y establezca la desactivación de la **versión de .NET Framework** en **.NET Framework v 4.0.30128** (o posterior). Después de ejecutar los pasos de configuración siguientes, haga clic con el botón derecho en la aplicación **ServiceModelSamples** y seleccione **administrar aplicación**, **Configuración avanzada.** ... Establezca el **grupo de aplicaciones** en el nuevo grupo de aplicaciones.  
  
> [!IMPORTANT]
>  Puede que los ejemplos ya estén instalados en su equipo. Compruebe el siguiente directorio (predeterminado) antes de continuar.  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  Si este directorio no existe, vaya a [ejemplos de Windows Communication Foundation (WCF) y Windows Workflow Foundation (WF) para .NET Framework 4](https://go.microsoft.com/fwlink/?LinkId=150780) para descargar todos los Windows Communication Foundation (WCF) [!INCLUDE[wf1](../../../../includes/wf1-md.md)] y ejemplos. Este ejemplo se encuentra en el siguiente directorio.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Services\Hosting\WebHost\ASPNetCompatibility`  
  
 Este ejemplo se basa en el [Introducción](../../../../docs/framework/wcf/samples/getting-started-sample.md), que implementa un servicio de calculadora. El contrato `ICalculator` se ha modificado como contrato`ICalculatorSession` para permitir realizar un conjunto de operaciones, manteniendo un resultado en ejecución.  
  
```csharp  
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples")]  
public interface ICalculatorSession  
{  
    [OperationContract]  
    void Clear();  
    [OperationContract]  
    void AddTo(double n);  
    [OperationContract]  
    void SubtractFrom(double n);  
    [OperationContract]  
    void MultiplyBy(double n);  
    [OperationContract]  
    void DivideBy(double n);  
    [OperationContract]  
    double Result();  
}  
```  
  
 El servicio mantiene el estado, utilizando la característica, para cada cliente ya que se llama a varias operaciones de servicio para realizar un cálculo. El cliente puede recuperar el resultado actual llamando a `Result` y borrar el resultado para ponerlo a cero llamando a `Clear`.  
  
 El servicio utiliza la sesión ASP.NET para almacenar el resultado de cada sesión de cliente. Esto permite al servicio mantener el resultado en ejecución para cada cliente por varias llamadas al servicio.  
  
> [!NOTE]
> El estado de sesión de ASP.NET y las sesiones de WCF son cosas muy diferentes. Vea la [sesión](../../../../docs/framework/wcf/samples/session.md) para obtener más información sobre las sesiones de WCF.
  
 El servicio tiene una dependencia íntima en el estado de sesión ASP.NET y requiere que el modo de compatibilidad ASP.NET funcione correctamente. Estos requisitos se expresan mediante declaración aplicando el atributo `AspNetCompatibilityRequirements`.  
  
```csharp  
[AspNetCompatibilityRequirements(RequirementsMode =  
                       AspNetCompatibilityRequirementsMode.Required)]  
public class CalculatorService : ICalculatorSession  
{  
    double Result  
    {  // store result in AspNet Session  
       get {  
          if (HttpContext.Current.Session["Result"] != null)  
             return (double)HttpContext.Current.Session["Result"];  
          return 0.0D;  
       }  
       set  
       {  
          HttpContext.Current.Session["Result"] = value;  
       }  
    }  
    public void Clear()  
    {  
        Result = 0.0D;  
    }  
    public void AddTo(double n)  
    {  
        Result += n;  
    }  
    public void SubtractFrom(double n)  
    {  
        Result -= n;  
    }  
    public void MultiplyBy(double n)  
    {  
        Result *= n;  
    }  
    public void DivideBy(double n)  
    {  
        Result /= n;  
    }  
    public double Result()  
    {  
        return Result;  
    }  
}  
```
  
 Al ejecutar el ejemplo, las solicitudes y respuestas de la operación se muestran en la ventana de la consola del cliente. Presione ENTRAR en la ventana de cliente para cerrar el cliente.  
  
```console
0, + 100, - 50, * 17.65, / 2 = 441.25  
Press <ENTER> to terminate client.  
```  
  
### <a name="to-set-up-build-and-run-the-sample"></a>Configurar, compilar y ejecutar el ejemplo  
  
1. Asegúrese de que ha realizado el [procedimiento de instalación única para los ejemplos de Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2. Para compilar el código C# o Visual Basic .NET Edition de la solución, siga las instrucciones de [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3. Una vez compilada la solución, ejecute setup. bat para configurar la aplicación ServiceModelSamples en IIS 7,0. El directorio ServiceModelSamples debería aparecer ahora como una aplicación de IIS 7,0.  
  
4. Para ejecutar el ejemplo en una configuración de equipos única o cruzada, siga las instrucciones de [ejecución de los ejemplos de Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
## <a name="see-also"></a>Vea también

- [Ejemplos de hospedaje y persistencia de AppFabric](https://go.microsoft.com/fwlink/?LinkId=193961)
