---
title: Configuración del Registro en la representación de gráficos
ms.date: 03/30/2017
helpviewer_keywords:
- rendering graphics [WPF], registry settings
- rendering graphics [WPF]
- rendering graphics [WPF], troubleshooting
- troubleshooting graphics rendering [WPF]
- graphics [WPF], rendering
ms.assetid: f4b41b42-327d-407c-b398-3ed5f505df8b
ms.openlocfilehash: 616c74ccd787d9acdcb2a3bbe281c2f43bb49c2e
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61762731"
---
# <a name="graphics-rendering-registry-settings"></a>Configuración del Registro en la representación de gráficos
En este tema se ofrece información general sobre la configuración del Registro en la representación de gráficos [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] que afecta a las aplicaciones de [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  

<a name="overview"></a>   
## <a name="when-to-use-graphics-rendering-registry-settings"></a>Cuándo usar la configuración del Registro en la representación de gráficos  
 Esta configuración del Registro se proporciona a efectos de solución de problemas, depuración y soporte técnico del producto. Como los cambios al Registro afectan a todas las aplicaciones [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], la aplicación no debe nunca modificar estas claves del Registro automáticamente ni durante la instalación.  
  
<a name="xpdmandwddm"></a>   
## <a name="what-are-xpdm-and-wddm"></a>¿Qué son XPDM y WDDM?  
 Parte de la configuración del Registro en la representación de gráficos incluye distintos valores predeterminados, que varían en función de que la tarjeta de vídeo use un controlador XPDM o WDDM. XPDM se refiere a [!INCLUDE[TLA#tla_winxp](../../../../includes/tlasharptla-winxp-md.md)] Display Driver Model y WDDM, a Windows Display Driver Model. WDDM está disponible en equipos que ejecuten [!INCLUDE[TLA2#tla_winvista](../../../../includes/tla2sharptla-winvista-md.md)] y [!INCLUDE[win7](../../../../includes/win7-md.md)]. XPDM está disponible en equipos que ejecuten [!INCLUDE[TLA2#tla_winvista](../../../../includes/tla2sharptla-winvista-md.md)], [!INCLUDE[TLA#tla_winxp](../../../../includes/tlasharptla-winxp-md.md)] y [!INCLUDE[TLA#tla_winnetsvrfam](../../../../includes/tlasharptla-winnetsvrfam-md.md)]. Para más información sobre WDDM, vea [Windows Vista Display Driver Model Design Guide](https://go.microsoft.com/fwlink/?LinkId=178394) (Guía de diseño de Windows Vista Display Driver Model).  
  
<a name="registry_settings"></a>   
## <a name="registry-settings"></a>Configuración de registro  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] proporciona cuatro parámetros de configuración del Registro para controlar la representación de [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]:  
  
|Parámetro|Descripción|  
|-------------|-----------------|  
|**Opción de deshabilitación de aceleración de hardware**|Especifica si se debe habilitar la aceleración de hardware.|  
|**Valor máximo de muestreo múltiple**|Especifica el grado de muestreo múltiple para el suavizado de contorno del contenido [!INCLUDE[TLA2#tla_3d](../../../../includes/tla2sharptla-3d-md.md)].|  
|**Configuración obligatoria de fecha del controlador de vídeo**|Especifica si el sistema deshabilita la aceleración de hardware para los controladores publicados antes de noviembre de 2004.|  
|**Opción de uso del rasterizador de referencia**|Especifica si [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] debe utilizar el rasterizador de referencia.|  
  
 Es posible acceder a estos parámetros mediante una utilidad de configuración externa que pueda hacer referencia a la configuración del Registro de [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]. Estos valores de configuración también pueden crearse o modificarse mediante el acceso a los valores directamente a través del Editor del Registro de [!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)].  
  
<a name="disablehardwareacceleration"></a>   
## <a name="disable-hardware-acceleration-option"></a>Opción de deshabilitación de aceleración de hardware  
  
|Clave del Registro|Tipo de valor|  
|------------------|----------------|  
|`HKEY_CURRENT_USER\SOFTWARE\Microsoft\Avalon.Graphics\DisableHWAcceleration`|DWORD|  
  
 La **opción de deshabilitación de aceleración de hardware** le permite desactivar la aceleración de hardware a efectos de depuración y prueba. Cuando vea artefactos de representación en una aplicación, intente desactivar la aceleración de hardware. Si el artefacto desaparece, podría ser el problema con el controlador de vídeo.  
  
 La **opción de deshabilitación de aceleración de hardware** es un valor DWORD que se establece en 0 o 1. Un valor de 1 deshabilita la aceleración de hardware. Un valor de 0 habilita la aceleración de hardware, siempre que el sistema cumpla los requisitos de aceleración de hardware. Para más información, consulte [Niveles de representación de gráficos](../advanced/graphics-rendering-tiers.md).  
  
<a name="maxmultisample"></a>   
## <a name="maximum-multisample-value"></a>Valor máximo de muestreo múltiple  
  
|Clave del Registro|Tipo de valor|  
|------------------|----------------|  
|`HKEY_CURRENT_USER\SOFTWARE\Microsoft\Avalon.Graphics\MaxMultisampleType`|DWORD|  
  
 El **valor máximo de muestreo múltiple** le permite ajustar la cantidad máxima de suavizado de contorno del contenido [!INCLUDE[TLA2#tla_3d](../../../../includes/tla2sharptla-3d-md.md)]. Use este nivel para deshabilitar el suavizado de contorno de [!INCLUDE[TLA2#tla_3d](../../../../includes/tla2sharptla-3d-md.md)] en [!INCLUDE[TLA2#tla_winvista](../../../../includes/tla2sharptla-winvista-md.md)] o para habilitarlo en [!INCLUDE[TLA#tla_winxp](../../../../includes/tlasharptla-winxp-md.md)].  
  
 El **valor máximo de muestreo múltiple** es un valor DWORD comprendido entre 0 y 16. Un valor de 0 especifica que debe deshabilitarse el suavizado de contorno de muestreo múltiple del contenido 3D y un valor de 16 intentará usar un suavizado de contorno de muestreo múltiple hasta 16 veces mayor, si la tarjeta de vídeo lo admite. Tenga en cuenta que, si establece este valor de clave del Registro en equipos que usen controladores XPDM, las aplicaciones usarán una gran cantidad de memoria de vídeo adicional, disminuirá el rendimiento de representación [!INCLUDE[TLA2#tla_3d](../../../../includes/tla2sharptla-3d-md.md)] y aumentarán las posibilidades de añadir errores de representación y problemas de estabilidad.  
  
 Cuando no se establece esta clave del Registro, el valor predeterminado de [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] es 0 para los controladores XPDM y 4 para los controladores WDDM.  
  
<a name="requiredvideodriverdatesetting"></a>   
## <a name="required-video-driver-date-setting"></a>Configuración obligatoria de fecha del controlador de vídeo  
  
|Clave del Registro|Tipo de valor|  
|------------------|----------------|  
|`HKEY_CURRENT_USER\SOFTWARE\Microsoft\Avalon.Graphics\RequiredVideoDriverDate`|Cadena|  
  
 En noviembre de 2004, [!INCLUDE[TLA#tla_ms](../../../../includes/tlasharptla-ms-md.md)] publicó una nueva versión de las instrucciones de prueba de controladores; los controladores escritos después de esta fecha ofrecen una mayor estabilidad. De forma predeterminada, [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] usará la canalización de aceleración de hardware para estos controladores y recurrirá a la representación de software para los controladores XPDM publicados antes de esta fecha.  
  
 La **configuración obligatoria de fecha del controlador de vídeo** le permite especificar una fecha mínima alternativa para los controladores XPDM. Solo se debe especificar una fecha anterior a noviembre de 2004 si está seguro de que el controlador de vídeo es lo suficientemente estable como para admitir [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
 La configuración obligatoria de fecha del controlador de vídeo adopta una cadena con el formato siguiente:  
  
| |  
|-|  
|*AAAA* `/` *MM* `/` *DD*|  
  
 Donde *AAAA* son los cuatro dígitos del año, *MM* son los dos dígitos del mes y *DD* son los dos dígitos del día. Cuando este valor no se establece, [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] usa noviembre de 2004 como fecha obligatoria del controlador de vídeo.  
  
<a name="usereferencerasterizeroption"></a>   
## <a name="use-reference-rasterizer-option"></a>Opción de uso del rasterizador de referencia  
  
|Clave del Registro|Tipo de valor|  
|------------------|----------------|  
|`HKEY_CURRENT_USER\SOFTWARE\Microsoft\Avalon.Graphics\UseReferenceRasterizer`|DWORD|  
  
 La **opción de uso del rasterizador de referencia** le permite forzar [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] a un modo simulado de representación de hardware para depuración: [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] pasa al modo de hardware, pero usa el rasterizador de software de referencia [!INCLUDE[TLA#tla_d3d](../../../../includes/tlasharptla-d3d-md.md)], d3dref9.dll, en lugar de un dispositivo real de hardware.  
  
 El rasterizador de referencia es muy lento, pero omite el controlador de vídeo para evitar cualquier problema de representación causado por problemas de controladores. Por este motivo, se puede usar el rasterizador de referencia para determinar si los problemas de representación se deben al controlador de vídeo. El archivo d3dref9.dll debe estar en una ubicación en la que la aplicación pueda acceder a él, como cualquier ubicación en la ruta del sistema o el directorio local de la aplicación.  
  
 La **opción de uso del rasterizador de referencia** adopta un valor DWORD. Un valor de 0 indica que no se usa el rasterizador de referencia. Cualquier otro valor distinto de cero fuerza a [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] a usar el rasterizador de referencia.  
  
## <a name="see-also"></a>Vea también

- [Niveles de representación de gráficos](../advanced/graphics-rendering-tiers.md)
- [Información general sobre la representación de gráficos en WPF](wpf-graphics-rendering-overview.md)
