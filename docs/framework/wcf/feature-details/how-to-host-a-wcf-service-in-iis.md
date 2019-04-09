---
title: Filtrar para hospedar un servicio WCF en IIS
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: b044b1c9-c1e5-4c9f-84d8-0f02f4537f8b
ms.openlocfilehash: 8b2ebc108bf3eef60e8877e617acec782da38fa4
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2019
ms.locfileid: "59124558"
---
# <a name="how-to-host-a-wcf-service-in-iis"></a>Filtrar para hospedar un servicio WCF en IIS
En este tema se describe los pasos básicos necesarios para crear un servicio de Windows Communication Foundation (WCF) que se hospeda en Internet Information Services (IIS). Este tema da por hecho que está familiarizado con IIS y sabe cómo usar la herramienta de administración de IIS para crear y administrar aplicaciones IIS. Para obtener más información acerca de IIS, consulte [Internet Information Services](https://go.microsoft.com/fwlink/?LinkId=132449). Un servicio WCF que se ejecuta en el entorno de IIS aprovecha plenamente las características IIS, como el reciclaje de procesos, cierre por inactividad, supervisión del estado de proceso y la activación basada en mensajes. Esta opción de hospedaje requiere que se configure correctamente IIS, pero no requiere que se escriba ningún código de hospedaje como parte de la aplicación. Sólo puede utilizar el hospedaje de IIS con un transporte HTTP.  
  
 Para obtener más información acerca de cómo WCF y [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] interactuar, consulte [servicios WCF y ASP.NET](../../../../docs/framework/wcf/feature-details/wcf-services-and-aspnet.md). Para obtener más información sobre la configuración de seguridad, consulte [seguridad](../../../../docs/framework/wcf/feature-details/security.md).  
  
 Para la copia de origen de este ejemplo, vea [IIS aloja uso en línea de código](../../../../docs/framework/wcf/samples/iis-hosting-using-inline-code.md).  
  
### <a name="to-create-a-service-hosted-by-iis"></a>Para crear un servicio hospedado por IIS  
  
1.  Confirme que IIS está instalado y ejecutándose en su equipo. Para obtener más información sobre la instalación y configuración de IIS, consulte [instalación y configuración de IIS 7.0](https://go.microsoft.com/fwlink/?LinkID=132128)  
  
2.  Cree una nueva carpeta para los archivos de la aplicación denominada "IISHostedCalcService", asegúrese de que [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] tiene acceso al contenido de la carpeta, y use la herramienta de administración de IIS para crear una nueva aplicación IIS que se ubique físicamente en este directorio de la aplicación. Cuando cree un alias para el directorio de la aplicación, use "IISHostedCalc".  
  
3.  Cree un nuevo archivo denominado "service.svc" en el directorio de la aplicación. Editar este archivo agregando la siguiente @ServiceHost elemento.  
  
    ```  
    <%@ServiceHost language=c# Debug="true" Service="Microsoft.ServiceModel.Samples.CalculatorService"%>  
    ```  
  
4.  Cree un subdirectorio App_Code dentro del directorio de la aplicación.  
  
5.  Cree un archivo de código denominado Service.cs en el subdirectorio App_Code.  
  
6.  Agregue las siguientes instrucciones using a la parte superior del archivo Service.cs.  
  
    ```csharp  
    using System;  
    using System.ServiceModel;  
    ```  
  
7.  Agregue la declaración de espacio de nombres siguiente después de las instrucciones using.  
  
    ```csharp  
    namespace Microsoft.ServiceModel.Samples  
    {  
    }  
    ```  
  
8.  Defina el contrato de servicio dentro de la declaración de espacio de nombres, tal y como se muestra en el código siguiente.  
  
     [!code-csharp[c_HowTo_HostInIIS#11](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_hostiniis/cs/source.cs#11)]
     [!code-vb[c_HowTo_HostInIIS#11](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_hostiniis/vb/source.vb#11)]  
  
9. Implemente el contrato de servicio después de la definición de contrato de servicio, tal como se muestra en el código siguiente.  
  
     [!code-csharp[c_HowTo_HostInIIS#12](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_hostiniis/cs/source.cs#12)]
     [!code-vb[c_HowTo_HostInIIS#12](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_hostiniis/vb/source.vb#12)]  
  
10. Cree un archivo denominado "Web.config" en el directorio de la aplicación y agregue el código de configuración siguiente a dicho archivo. En tiempo de ejecución, la infraestructura de WCF usa la información para construir las aplicaciones cliente pueden comunicarse con un punto de conexión.  
  
     [!code-xml[c_HowTo_HostInIIS#100](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_hostiniis/common/web.config#100)]      
  
     Este ejemplo especifica puntos de conexión explícitamente en el archivo de configuración. Si no agrega ningún punto de conexión al servicio, el tiempo de ejecución agregará los puntos de conexión predeterminados. Para obtener más información acerca de los extremos, enlaces y comportamientos vea [Simplified Configuration](../../../../docs/framework/wcf/simplified-configuration.md) y [Simplified Configuration for WCF Services](../../../../docs/framework/wcf/samples/simplified-configuration-for-wcf-services.md).  
  
11. Para asegurarse de que el servicio está hospedado correctamente, abra una instancia de Internet Explorer y vaya a la URL del servicio: `http://localhost/IISHostedCalc/Service.svc`  
  
## <a name="example"></a>Ejemplo  
 A continuación, se muestra el código completo del servicio de calculadora hospedado en IIS.  
  
 [!code-csharp[C_HowTo_HostInIIS#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_hostiniis/cs/source.cs#1)] 
 [!code-vb[C_HowTo_HostInIIS#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_hostiniis/vb/source.vb#1)] 
 [!code-xml[c_HowTo_HostInIIS#100](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_hostiniis/common/web.config#100)]  
  
## <a name="see-also"></a>Vea también

- [Hospedaje en Internet Information Services](../../../../docs/framework/wcf/feature-details/hosting-in-internet-information-services.md)
- [Servicios de hospedaje](../../../../docs/framework/wcf/hosting-services.md)
- [Servicios WCF y ASP.NET](../../../../docs/framework/wcf/feature-details/wcf-services-and-aspnet.md)
- [Seguridad](../../../../docs/framework/wcf/feature-details/security.md)
- [Características de hospedaje de Windows Server AppFabric](https://go.microsoft.com/fwlink/?LinkId=201276)
