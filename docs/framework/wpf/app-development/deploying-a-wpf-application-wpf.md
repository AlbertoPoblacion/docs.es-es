---
title: Implementar una aplicación de WPF
ms.date: 03/30/2017
helpviewer_keywords:
- WPF applications [WPF], deployment
- deployment [WPF], applications
ms.assetid: 12cadca0-b32c-4064-9a56-e6a306dcc76d
ms.openlocfilehash: cfb617fde514c93596d52b0ca70da39c6e5be301
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/22/2019
ms.locfileid: "69958647"
---
# <a name="deploying-a-wpf-application-wpf"></a>Implementar una aplicación de WPF
Después de compilar las aplicaciones de Windows Presentation Foundation (WPF), deben implementarse. Windows y el .NET Framework incluyen varias tecnologías de implementación. La tecnología de implementación que se usa para implementar una aplicación de [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] depende del tipo de esta. En este tema se proporciona alguna información general sobre cada tecnología de implementación y su uso, además de los requisitos de implementación de cada tipo de aplicación de [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)].  

<a name="Deployment_Technologies"></a>   
## <a name="deployment-technologies"></a>Tecnologías de implementación  
 Windows y el .NET Framework incluyen varias tecnologías de implementación, entre las que se incluyen:  
  
- Implementación de XCopy.  
  
- Implementación de [!INCLUDE[TLA2#tla_wininstall](../../../../includes/tla2sharptla-wininstall-md.md)].  
  
- Implementación ClickOnce  
  
<a name="XCopy_Deployment"></a>   
### <a name="xcopy-deployment"></a>Implementación de XCopy  
 La implementación de XCopy se refiere al uso del programa de línea de comandos XCopy para copiar los archivos de una ubicación a otra. La implementación de XCopy es adecuada en las circunstancias siguientes:  
  
- La aplicación es autónoma. No necesita actualizar el cliente para ejecutarse.  
  
- Los archivos de la aplicación se deben mover de una ubicación a otra; por ejemplo, de la ubicación de compilación (disco local, recurso compartido de archivos [!INCLUDE[TLA2#tla_unc](../../../../includes/tla2sharptla-unc-md.md)], etc.) a la ubicación de publicación (sitio web, recurso compartido de archivos [!INCLUDE[TLA2#tla_unc](../../../../includes/tla2sharptla-unc-md.md)], etc.).  
  
- La aplicación no necesita la integración en el Shell (acceso directo del menú de Inicio, icono de escritorio, etc.).  
  
 Aunque XCopy es adecuado para escenarios de implementación simples, presenta limitaciones cuando se requieren funciones de implementación más complejas. En particular, al usar Xcopy se provoca una sobrecarga al crear, ejecutar y mantener los scripts necesarios para administrar la implementación de una manera robusta. Además, XCopy no admite el control de versiones, la desinstalación ni la reversión.  
  
<a name="Windows_Installer"></a>   
### <a name="windows-installer"></a>Windows Installer  
 [!INCLUDE[TLA2#tla_wininstall](../../../../includes/tla2sharptla-wininstall-md.md)] permite empaquetar las aplicaciones como aplicaciones ejecutables autónomas que se pueden distribuir con facilidad a los clientes y ejecutar. Además, [!INCLUDE[TLA2#tla_wininstall](../../../../includes/tla2sharptla-wininstall-md.md)] se instala con Windows y permite la integración con el escritorio, el menú Inicio y el panel de control programas.  
  
 [!INCLUDE[TLA2#tla_wininstall](../../../../includes/tla2sharptla-wininstall-md.md)] simplifica la instalación y desinstalación de aplicaciones, pero no proporciona los medios para asegurarse de que las aplicaciones instaladas se mantengan actualizadas desde el punto de vista de su versión.  
  
 Para obtener más información acerca de Windows Installer, vea [implementación de Windows Installer](/visualstudio/deployment/deploying-applications-services-and-components#create-an-installer-package-windows-desktop).
  
<a name="ClickOnce_Deployment"></a>   
### <a name="clickonce-deployment"></a>implementación de ClickOnce  
 ClickOnce habilita la implementación de aplicaciones de estilo Web para aplicaciones que no son de Web. Las aplicaciones se publican e implementan para Web o para servidores de archivos. Aunque ClickOnce no admite toda la gama de características de cliente que [!INCLUDE[TLA2#tla_wininstall](../../../../includes/tla2sharptla-wininstall-md.md)]realizan las aplicaciones instaladas, admite un subconjunto que incluye lo siguiente:  
  
- Integración con el menú Inicio y el panel de control de Programas.  
  
- Control de versiones, reversión y desinstalación.  
  
- Modo de instalación en línea, que siempre inicia una aplicación desde la ubicación de implementación.  
  
- Actualización automática cuando se publican nuevas versiones.  
  
- Registro de extensiones de archivo.  
  
 Para obtener más información sobre ClickOnce, consulte [seguridad e implementación de ClickOnce](/visualstudio/deployment/clickonce-security-and-deployment).  
  
<a name="Deploying_WPF_Applications"></a>   
## <a name="deploying-wpf-applications"></a>Implementar aplicaciones de WPF  
 Las opciones de implementación para una aplicación de [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] dependen del tipo de aplicación. Desde una perspectiva de implementación, [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] tiene tres tipos de aplicación significativos:  
  
- Aplicaciones independientes.  
  
- Aplicaciones [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] solo de marcado.  
  
- [!INCLUDE[TLA#tla_xbap#plural](../../../../includes/tlasharptla-xbapsharpplural-md.md)]  
  
<a name="Deploying_Standalone_Applications"></a>   
### <a name="deploying-standalone-applications"></a>Implementar aplicaciones independientes  
 Las aplicaciones independientes se implementan mediante ClickOnce [!INCLUDE[TLA2#tla_wininstall](../../../../includes/tla2sharptla-wininstall-md.md)]o. De cualquier modo, las aplicaciones independientes requieren plena confianza para ejecutarse. La plena confianza se concede automáticamente a las aplicaciones independientes que se implementan mediante [!INCLUDE[TLA2#tla_wininstall](../../../../includes/tla2sharptla-wininstall-md.md)]. Las aplicaciones independientes que se implementan mediante ClickOnce no reciben automáticamente plena confianza. En su lugar, ClickOnce muestra un cuadro de diálogo de advertencia de seguridad que los usuarios deben aceptar antes de instalar una aplicación independiente. Si el usuario acepta, se instala la aplicación independiente y se le otorgan permisos de plena confianza. En caso contrario, no se instala la aplicación independiente.  
  
<a name="Deploying_Markup_Only_XAML_Applications"></a>   
### <a name="deploying-markup-only-xaml-applications"></a>Implementar aplicaciones XAML solo de marcado  
 Las páginas solo [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] de marcado normalmente se publican en servidores Web, como páginas HTML, y se pueden ver con Internet Explorer. Las páginas [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] solo de marcado se ejecutan dentro de un recinto de seguridad de confianza parcial con restricciones definidas por el conjunto de permisos de zona de Internet. Esto proporciona un espacio aislado de seguridad equivalente a las aplicaciones web basadas en HTML.  
  
 Para obtener más información sobre los cambios en materia de seguridad que se han realizado en las aplicaciones [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)], vea [Seguridad (WPF)](../security-wpf.md).  
  
 Las páginas [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] solo de marcado se pueden instalar en el sistema de archivos local usando XCopy o [!INCLUDE[TLA2#tla_wininstall](../../../../includes/tla2sharptla-wininstall-md.md)]. Estas páginas se pueden ver con Internet Explorer o el explorador de Windows.  
  
 Para obtener más información sobre XAML, vea [Información general sobre XAML (WPF)](../advanced/xaml-overview-wpf.md).  
  
<a name="Deploying_XAML_Browser_Applications"></a>   
### <a name="deploying-xaml-browser-applications"></a>Implementar aplicaciones de explorador XAML  
 [!INCLUDE[TLA2#tla_xbap#plural](../../../../includes/tla2sharptla-xbapsharpplural-md.md)] son aplicaciones compiladas que necesitan los tres archivos siguientes para implementarse:  
  
- *ApplicationName*.exe: El archivo de aplicación del ensamblado ejecutable.  
  
- *ApplicationName*.xbap: El manifiesto de implementación.  
  
- *ApplicationName*.exe.manifest: Manifiesto de aplicación  
  
> [!NOTE]
> Para obtener más información sobre los manifiestos de implementación y de aplicación, vea [Compilar una aplicación de WPF (WPF)](building-a-wpf-application-wpf.md).  
  
 Estos archivos se crean al compilar una [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)]. Para obtener más información, vea [Cómo: Cree un nuevo proyecto](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/bb628663(v=vs.100))de aplicación de explorador de WPF. Al igual que las [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] páginas de [!INCLUDE[TLA2#tla_xbap#plural](../../../../includes/tla2sharptla-xbapsharpplural-md.md)] solo marcado, normalmente se publican en un servidor Web y se ven con Internet Explorer.  
  
 [!INCLUDE[TLA2#tla_xbap#plural](../../../../includes/tla2sharptla-xbapsharpplural-md.md)] se puede implementar en los clientes usando cualquiera de las técnicas de implementación. Sin embargo, se recomienda ClickOnce, ya que ofrece las siguientes capacidades:  
  
1. Actualizaciones automáticas cuando se publica una nueva versión.  
  
2. Privilegios aumentados para [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] que se ejecuta con plena confianza.  
  
 De manera predeterminada, ClickOnce publica los archivos de aplicación con la extensión .deploy. Esto puede ser problemático, pero también puede deshabilitarse. Para obtener más información, vea [Problemas de configuración de servidor y cliente en implementaciones de ClickOnce](/visualstudio/deployment/server-and-client-configuration-issues-in-clickonce-deployments).  
  
 Para obtener más información sobre la manera de implementar [!INCLUDE[TLA#tla_xbap#plural](../../../../includes/tlasharptla-xbapsharpplural-md.md)], vea [Información general sobre las aplicaciones de explorador XAML de WPF](wpf-xaml-browser-applications-overview.md).  
  
<a name="Installing__NET_Framework_3_0"></a>   
## <a name="installing-the-net-framework"></a>Instalar .NET Framework  
 Para ejecutar una [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] aplicación, el marco de trabajo de Microsoft .net debe estar instalado en el cliente. Internet Explorer detecta automáticamente si los clientes se instalan con .NET Framework [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] cuando se ven las aplicaciones hospedadas en el explorador. Si el .NET Framework no está instalado, Internet Explorer solicita a los usuarios que lo instalen.  
  
 Para detectar si el .NET Framework está instalado, Internet Explorer incluye una aplicación de programa previo que se registra como el controlador de las extensiones multipropósito de correo Internet (MIME) de reserva para los archivos de contenido con las siguientes extensiones:. XAML,. XPS,. XBAP y. Application. Si navega a estos tipos de archivo y el .NET Framework no está instalado en el cliente, la aplicación de arranque solicita permiso para instalarlo. Si no se proporciona el permiso, no se instalará ni el .NET Framework ni la aplicación.  
  
 Si se concede el permiso, Internet Explorer descarga e instala el .NET Framework mediante el Servicio de transferencia inteligente en segundo plano de Microsoft (BITS). Después de instalar correctamente el .NET Framework, el archivo solicitado originalmente se abre en una nueva ventana del explorador.  
  
 Para obtener más información, vea [Implementar .NET Framework y aplicaciones](../../deployment/index.md).  
  
## <a name="see-also"></a>Vea también

- [Compilar una aplicación de WPF](building-a-wpf-application-wpf.md)
- [Seguridad](../security-wpf.md)
