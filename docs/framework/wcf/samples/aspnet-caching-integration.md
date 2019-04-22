---
title: Integración de almacenamiento en caché de ASP.NET
ms.date: 03/30/2017
ms.assetid: f581923a-8a72-42fc-bd6a-46de2aaeecc1
ms.openlocfilehash: 8ed546459479e9986d6bbecf6eaca350d2d73c98
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59770027"
---
# <a name="aspnet-caching-integration"></a>Integración de almacenamiento en caché de ASP.NET
En este ejemplo se muestra cómo utilizar la memoria caché de resultados de ASP.NET con el modelo de programación HTTP wEB de WCF. Este tema se centra en la característica de integración de la memoria caché de resultados de ASP.NET.  
  
## <a name="demonstrates"></a>Demostraciones  
 Integración con la memoria caché de resultados de ASP.NET  
  
> [!IMPORTANT]
>  Puede que los ejemplos ya estén instalados en su equipo. Compruebe el siguiente directorio (predeterminado) antes de continuar.  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  Si no existe este directorio, vaya a [Windows Communication Foundation (WCF) y Windows Workflow Foundation (WF) Samples para .NET Framework 4](https://go.microsoft.com/fwlink/?LinkId=150780) para descargar todos los Windows Communication Foundation (WCF) y [!INCLUDE[wf1](../../../../includes/wf1-md.md)] ejemplos. Este ejemplo se encuentra en el siguiente directorio.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Web\AspNetCachingIntegration`  
  
## <a name="discussion"></a>Discusión  
 El ejemplo usa el <xref:System.ServiceModel.Web.AspNetCacheProfileAttribute> utilizar ASP.NET de salida de almacenamiento en caché con el servicio de Windows Communication Foundation (WCF). <xref:System.ServiceModel.Web.AspNetCacheProfileAttribute> se aplica a las operaciones de servicio y proporciona el nombre de un perfil de la memoria caché en un archivo de configuración que se debería aplicar a las respuestas de la operación dada.  
  
 En el archivo Service.cs del proyecto de servicio de ejemplo, tanto el `GetCustomer` y `GetCustomers` operaciones se marcan con el <xref:System.ServiceModel.Web.AspNetCacheProfileAttribute>, que proporciona el nombre de perfil de caché "CacheFor60Seconds". En el archivo Web.config del proyecto de servicio, el perfil de caché "CacheFor60Seconds" se proporciona bajo el <`caching`> elemento de <`system.web`>. Para este perfil de caché, el valor de la `duration` atributo es "60", por lo que las respuestas asociadas a este perfil se almacenan en caché en la caché de resultados ASP.NET durante 60 segundos. Además, para este perfil de caché, el `varmByParam` está establecido en "format" de modo que las solicitudes con valores diferentes para el `format` consulta al parámetro de cadena tienen sus respuestas en caché por separado. Por último, el perfil de caché `varyByHeader` atributo está establecido en "Accept", por lo que las solicitudes con diferentes valores de encabezado Accept tienen sus respuestas en caché por separado.  
  
 Program.cs en el proyecto cliente muestra el modo en que se puede crear este tipo de cliente utilizando <xref:System.Net.HttpWebRequest>. Observe que se trata simplemente de una manera de tener acceso a un servicio de WCF. También es posible tener acceso al servicio utilizando otras clases de .NET Framework, como el generador de canales WCF y <xref:System.Net.WebClient>. Otros ejemplos del SDK (como el [servicio HTTP básico](../../../../docs/framework/wcf/samples/basic-http-service.md) ejemplo) muestran cómo utilizar estas clases para comunicarse con un servicio WCF.  
  
## <a name="to-run-the-sample"></a>Para ejecutar el ejemplo  
 El ejemplo consta de tres proyectos:  
  
-   **Servicio**: Un proyecto de aplicación Web que incluye un servicio HTTP WCF hospedado en ASP.NET.  
  
-   **Cliente**: Proyecto de aplicación de consola que realiza las llamadas al servicio.  
  
-   **Common**: Una biblioteca compartida que contiene el tipo de cliente utilizado por el cliente y el servicio.  
  
 Cuando se ejecuta la aplicación de consola Cliente, el cliente realiza las solicitudes al servicio y escribe la información pertinente de las respuestas en la ventana de la consola.  
  
#### <a name="to-run-the-sample"></a>Para ejecutar el ejemplo  
  
1. Abra la solución para obtener el ejemplo de integración del almacenamiento en caché de ASP.NET.  
  
2. Presione Ctrl+MAYÚS+B para compilar la solución.  
  
3. Si el **el Explorador de soluciones** ventana ya no está abierta, presione CTRL + W + S.  
  
4. Desde el **el Explorador de soluciones** ventana, haga clic derecho la **servicio** del proyecto y seleccione **Iniciar nueva instancia**. De esta forma se inicia el servidor de desarrollo de ASP.NET, que hospeda el servicio.  
  
5. Desde el **el Explorador de soluciones** ventana, haga clic derecho la **cliente** del proyecto y seleccione **Iniciar nueva instancia**.  
  
6. La ventana de la consola del cliente aparece y proporciona el URI del servicio en ejecución y el URI de la página de Ayuda HTML para este. Puede ver la página de Ayuda HTML en cualquier momento escribiendo su URI en un explorador.  
  
7. A medida que el ejemplo se ejecuta, el cliente escribe el estado de la actividad actual.  
  
8. Presione cualquier tecla para terminar la aplicación de consola del cliente.  
  
9. Presione MAYÚS+F5 para dejar de depurar el servicio.  
  
10. En el área de notificación de Windows, haga clic el icono del servidor de desarrollo de ASP.NET y seleccione **detener**.
