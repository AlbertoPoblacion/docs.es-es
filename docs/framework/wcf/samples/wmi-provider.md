---
title: Proveedor WMI
ms.date: 03/30/2017
ms.assetid: 462f0db3-f4a4-4a4b-ac26-41fc25c670a4
ms.openlocfilehash: 519f63f8dfc558a83a98ca44f74e926beb81c190
ms.sourcegitcommit: 558d78d2a68acd4c95ef23231c8b4e4c7bac3902
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/09/2019
ms.locfileid: "59327235"
---
# <a name="wmi-provider"></a>Proveedor WMI
Este ejemplo muestra cómo recopilar datos de servicios de Windows Communication Foundation (WCF) en tiempo de ejecución mediante el proveedor de Instrumental de administración de Windows (WMI) que está integrado en WCF. Asimismo, este ejemplo muestra cómo agregar un objeto WMI definido por el usuario a un servicio. El ejemplo activa el proveedor WMI para la [Introducción](../../../../docs/framework/wcf/samples/getting-started-sample.md) y muestra cómo recopilar datos de la `ICalculator` servicio en tiempo de ejecución.  
  
 WMI es la implementación de Microsoft del estándar Web-Based Enterprise Management (WBEM). Para obtener más información sobre el SDK de WMI, consulte [Instrumental de administración de Windows](/windows/desktop/WmiSdk/wmi-start-page). WBEM es un estándar de la industria para saber cómo exponen las aplicaciones la instrumentación de administración a las herramientas de administración externas.  
  
 WCF implementa un proveedor WMI, un componente que expone la instrumentación en tiempo de ejecución a través de una interfaz compatible con WBEM. Las herramientas de administración pueden conectarse a los servicios a través de la interfaz en tiempo de ejecución. WCF expone atributos de servicios como direcciones, enlaces, comportamientos y agentes de escucha.  
  
 El proveedor de WMI integrado se activa en el archivo de configuración de la aplicación. Esto se realiza mediante el `wmiProviderEnabled` atributo de la [ \<diagnósticos >](../../../../docs/framework/configure-apps/file-schema/wcf/diagnostics.md) en el [ \<system.serviceModel >](../../../../docs/framework/configure-apps/file-schema/wcf/system-servicemodel.md) sección, como se muestra en el ejemplo siguiente configuración:  
  
```xml  
<system.serviceModel>  
    ...  
    <diagnostics wmiProviderEnabled="true" />  
    ...  
</system.serviceModel>  
```  
  
 Esta entrada de configuración expone una interfaz WMI. Ahora, las aplicaciones de administración pueden establecer la conexión a través de esta interfaz y obtener acceso a la instrumentación de administración de la aplicación.  
  
## <a name="custom-wmi-object"></a>Objeto WMI personalizado  
 Agregar objetos WMI a un servicio permite revelar la información definida por el usuario junto con la información de proveedor WMI integrada. Esto se logra publicando el esquema del servicio en WMI mediante la aplicación Installutil.exe. Las instrucciones para conseguirlo, además de más información, se pueden encontrar en las instrucciones de configuración al final del tema.  
  
## <a name="accessing-wmi-information"></a>Acceso a la información de WMI  
 Se puede tener acceso a los datos de WMI de maneras muy distintas. Microsoft proporciona las API de WMI para scripts, aplicaciones de Visual Basic, las aplicaciones de C++ y el [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] (https://docs.microsoft.com/windows/desktop/wmisdk/using-wmi).  
  
 Este ejemplo utiliza dos scripts Java: uno para enumerar los servicios que se ejecutan en el equipo junto con algunas de sus propiedades y otro para ver los datos de WMI definidos por el usuario. El script abre una conexión con el proveedor WMI, analiza los datos y muestra los datos recopilados.  
  
 Iniciar el ejemplo para crear una instancia en ejecución de un servicio WCF. Mientras el servicio se está ejecutando, ejecute cada script de Java usando el comando siguiente en el símbolo del sistema:  
  
```  
cscript EnumerateServices.js  
```  
  
 El script obtiene acceso al instrumental contenido en el servicio y genera la salida siguiente:  
  
```  
Microsoft (R) Windows Script Host Version 5.6  
Copyright © Microsoft Corporation 1996-2001. All rights reserved.  
  
1 service(s) found.  
|-PID:           5776  
|-DistinguishedName:  CalculatorService@http://localhost/ServiceModelSamples/service.svc  
|-Endpoints:     1 endpoints  
  |-CalculatorService.ICalculator@http://localhost/ServiceModelSamples/service.svc  
    |-Address:                        http://localhost/ServiceModelSamples/service.svc  
    |-CounterInstanceName:  
    |-AddressHeaders:                 0  
    |-ContractType:                   Contract.Name='ICalculator'  
    |-BindingElements:                4 bindings  
      |-BindingElements[0]  
        |-Type:                       TransactionFlowBindingElement  
      |-BindingElements[1]  
        |-Type:                       SymmetricSecurityBindingElement  
      |-BindingElements[2]  
        |-Type:                       TextMessageEncodingBindingElement  
        |-MaxReadPoolSize:            64  
        |-MaxWritePoolSize:           16  
      |-BindingElements[3]  
        |-Type:                       HttpTransportBindingElement  
        |-ManualAddressing:           false  
        |-MaxBufferSize:              65536  
        |-AllowCookies:               false  
        |-AuthenticationScheme:       Anonymous  
        |-BypassProxyOnLocal:         false  
        |-HostNameComparisonMode:     StrongWildcard  
        |-ProxyAddress:               null  
        |-ProxyAuthenticationScheme:  Anonymous  
        |-Realm:  
        |-TransferMode:               Buffered  
        |-UseDefaultWebProxy:         true  
|-Behaviors:     5 behaviors  
      |-Behavior[0]  
      |-Type:                       ServiceBehaviorAttribute  
        |-AddressFilterMode:               Exact  
        |-AutomaticSessionShutdown:        true  
        |-ConcurrencyMode:                 Single  
        |-IncludeExceptionDetailInFaults:  false  
        |-InstanceContextMode:             PerSession  
        |-TransactionIsolationLevel:       Unspecified  
        |-TransactionTimeout:              null  
        |-ValidateMustUnderstand:          true  
      |-Behavior[1]  
      |-Type:                       AspNetCompatibilityRequirementsAttribute  
      |-Behavior[2]  
      |-Type:                       ServiceDebugBehavior  
      |-Behavior[3]  
      |-Type:                       ServiceAuthorizationBehavior  
      |-Behavior[4]  
      |-Type:                       Behavior  
```  
  
 Después, ejecute el segundo script de Java para mostrar los datos de WMI definidos por el usuario:  
  
```  
cscript EnumerateCustomObjects.js  
```  
  
 El script tiene acceso al instrumental definido por el usuario contenido en los servicios y genera el resultado siguiente:  
  
```  
1 WMIObject(s) found.  
|-PID:           30285bfd-9d66-4c4e-9be2-310499c5cef5  
|-InstanceId:    3839  
|-WMIInfo:       User Defined WMI Information.  
```  
  
 El resultado muestra que hay un único servicio que se ejecuta en el equipo. El servicio expone un extremo que implementa el contrato `ICalculator`. Los valores del comportamiento y el enlace que el punto de conexión implementa se muestran como la suma de elementos individuales de la pila de mensajería.  
  
 WMI no se limita a exponer el Instrumental de administración de la infraestructura de WCF. La aplicación puede exponer sus propios elementos de datos específicos del dominio a través del mismo mecanismo. WMI es un mecanismo unificado para la inspección y control de un servicio Web.  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>Configurar, compilar y ejecutar el ejemplo  
  
1. Asegúrese de que ha realizado la [procedimiento de instalación de un solo uso para los ejemplos de Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2. Para compilar el código C# o Visual Basic .NET Edition de la solución, siga las instrucciones de [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3. Publique el esquema de los servicios en WMI ejecutando InstallUtil.exe (las ubicaciones predeterminadas para Installutil.exe son "%WINDIR%\Microsoft.NET\Framework\v4.0.30319") en el archivo service.dll del directorio de hospedaje. Este paso solo debe ejecutarse cuando se hayan realizado cambios en el archivo service.dll.
  
4. Para ejecutar el ejemplo en una configuración de equipos única o cruzada, siga las instrucciones de [ejecutando los ejemplos de Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
    > [!NOTE]
    >  Si ha instalado WCF después de instalar ASP.NET, es posible que deba ejecutar "%WINDIR%\ Microsoft.Net\Framework\v3.0\Windows Communication Foundation\servicemodelreg.exe "- r - x para proporcionar a la cuenta de ASPNET permiso para publicar objetos WMI.  
  
5. Vea los datos del ejemplo que aparece mediante WMI con los comandos: `cscript EnumerateServices.js` o `cscript EnumerateCustomObjects.js`.  
  
> [!IMPORTANT]
>  Puede que los ejemplos ya estén instalados en su equipo. Compruebe el siguiente directorio (predeterminado) antes de continuar.  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  Si no existe este directorio, vaya a [Windows Communication Foundation (WCF) y Windows Workflow Foundation (WF) Samples para .NET Framework 4](https://go.microsoft.com/fwlink/?LinkId=150780) para descargar todos los Windows Communication Foundation (WCF) y [!INCLUDE[wf1](../../../../includes/wf1-md.md)] ejemplos. Este ejemplo se encuentra en el siguiente directorio.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Management\WMIProvider`  
  
## <a name="see-also"></a>Vea también

- [Ejemplos de supervisión de AppFabric](https://go.microsoft.com/fwlink/?LinkId=193959)
