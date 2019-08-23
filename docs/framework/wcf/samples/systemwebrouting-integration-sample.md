---
title: Ejemplo de integración de SystemWebRouting
ms.date: 03/30/2017
ms.assetid: f1c94802-95c4-49e4-b1e2-ee9dd126ff93
ms.openlocfilehash: 032be700beaa38ed6c08ed1940aab558b2106591
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/22/2019
ms.locfileid: "69964483"
---
# <a name="systemwebrouting-integration-sample"></a>Ejemplo de integración de SystemWebRouting
Este ejemplo muestra la integración de nivel de hospedaje con las clases en el espacio de nombres <xref:System.Web.Routing>. Las clases en el espacio de nombres <xref:System.Web.Routing> permiten a una aplicación utilizar direcciones URL que no se corresponden directamente con un recurso físico. El uso del enrutamiento web permite al desarrollador crear direcciones virtuales para HTTP que se asignan a los servicios WCF reales. Esto es útil cuando un servicio WCF se debe hospedar sin requerir un archivo físico ni un recurso, o cuando se debe tener acceso a los servicios con direcciones URL que no contienen archivos como .html o .aspx. En este ejemplo se muestra cómo utilizar la clase <xref:System.Web.Routing.RouteTable> para crear URI virtuales que se asignan a servicios en ejecución definidos en global.asax. 

> [!NOTE]
> Las clases en el espacio de nombres <xref:System.Web.Routing> solo funcionan para los servicios hospedados sobre HTTP.  
  
En este ejemplo se usa WCF para crear dos fuentes RSS `movies` : una fuente `channels` y una fuente. Las direcciones URL para activar los servicios no contienen una extensión y se registran en `Application_Start` el método de `Global` la clase derivada de <xref:System.Web.HttpApplication> la clase.  
  
> [!NOTE]
> Este ejemplo solo funciona en Internet Information Services (IIS) 7,0 y versiones posteriores, ya que IIS 6,0 usa un método diferente para admitir direcciones URL sin extensión.  

#### <a name="to-download-this-sample"></a>Para descargar este ejemplo
  
Es posible que este ejemplo ya esté instalado en el equipo. Compruebe el siguiente directorio (predeterminado) antes de continuar.  
   
`<InstallDrive>:\WF_WCF_Samples`  
   
 Si este directorio no existe, vaya a [ejemplos de Windows Communication Foundation (WCF) y Windows Workflow Foundation (WF) para .NET Framework 4](https://go.microsoft.com/fwlink/?LinkId=150780) para descargar todos los Windows Communication Foundation (WCF) [!INCLUDE[wf1](../../../../includes/wf1-md.md)] y ejemplos. Este ejemplo se encuentra en el siguiente directorio.  
   
`<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Services\Hosting\WebRoutingIntegration`  
  
#### <a name="to-use-this-sample"></a>Para utilizar este ejemplo  
  
1. Con Visual Studio, abra el archivo WebRoutingIntegration. sln.  
  
2. Para ejecutar la solución e iniciar el servidor de desarrollo web, presione F5.  
  
     Aparece una lista de directorios para el ejemplo. Observe que no hay ningún archivo con la extensión de archivo .svc.  
  
3. En la barra de direcciones, `movies` agregue a la dirección URL para que lea `http://localhost:[port]/movies` y presione Entrar.  
  
     Las fuentes de películas aparecen en el explorador.  
  
4. En la barra de direcciones, `channels` agregue a la dirección URL, de modo `http://localhost:[port]/channels` que sea lectura y presione Entrar.  
  
     La fuente de canales aparece en el explorador.  
  
5. Presione ALT+F4 para cerrar el explorador web.  
  
     Si el servidor de desarrollo no se ha cerrado, haga clic con el botón secundario en el icono del área de notificación y seleccione **detener**.  
  
#### <a name="to-use-this-sample-when-hosted-in-iis"></a>Para utilizar este ejemplo cuando se hospeda en IIS  
  
1. Con Visual Studio, abra el archivo WebRoutingIntegration. sln.  
  
2. Compile el proyecto presionando CTRL+MAYÚS+B.  
  
3. Cree una aplicación web en el Administrador de Internet Information Services (IIS).  
  
    1. En el administrador de IIS, haga clic con el botón secundario en el **sitio web predeterminado** y seleccione **Agregar una aplicación**.  
  
    2. Para el **alias**, escriba `WebRoutingIntegration`.  
  
    3. Para la **ruta de acceso física**, seleccione la carpeta de servicio dentro del proyecto.  
  
    4. Haga clic en **Aceptar**.  
  
4. Inicie la aplicación, haciendo clic con el botón secundario en la aplicación web y seleccionando **administrar aplicación** y, a continuación, **examinar**.  
  
5. En la barra de direcciones, `movies` agregue a la dirección URL, de modo `http://localhost:[port]/movies` que sea lectura y presione Entrar.  
  
     Las fuentes de películas aparecen en el explorador.  
  
6. En la barra de direcciones, `channels` agregue a la dirección URL, de modo `http://localhost:[port]/channels` que sea lectura y presione Entrar.  
  
     La fuente de canales aparece en el explorador.  
  
7. Presione ALT+F4 para cerrar el explorador web.  
  
 En este ejemplo se muestra que el nivel de hospedaje es capaz de crear las clases en el espacio de nombres <xref:System.Web.Routing> para enrutar las solicitudes de servicios hospedados a través de HTTP.  
  
> [!NOTE]
> Debe actualizar la versión predeterminada del grupo de aplicaciones [!INCLUDE[netfx40_long](../../../../includes/netfx40-long-md.md)] a si está establecida en la versión 2.  
  
## <a name="see-also"></a>Vea también

- [Ejemplos de hospedaje y persistencia de AppFabric](https://go.microsoft.com/fwlink/?LinkId=193961)
