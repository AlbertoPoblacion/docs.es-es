---
title: '&lt;performanceCounter&gt; elemento (configuración de red)'
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/settings/performanceCounters
- http://schemas.microsoft.com/.NetConfiguration/v2.0#performanceCounters
helpviewer_keywords:
- performanceCounter element
- <performanceCounter> element
ms.assetid: 3afa1586-e1b8-473d-8985-c3fc90cf561b
ms.openlocfilehash: ea0eba097505741aba31bce4f23e0cc9ca1d4608
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/23/2019
ms.locfileid: "54712488"
---
# <a name="ltperformancecountergt-element-network-settings"></a>&lt;performanceCounter&gt; elemento (configuración de red)
Habilita o deshabilita los contadores de rendimiento de red.  
  
 \<configuration>  
\<system.net>  
\<settings>  
\<performanceCounters>  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
<performanceCounters  
  enabled="true|false"  
/>  
```  
  
## <a name="attributes-and-elements"></a>Atributos y elementos  
 En las siguientes secciones se describen los atributos, los elementos secundarios y los elementos primarios.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descripción|  
|---------------|-----------------|  
|`enabled`|Especifica si se habilitan los contadores de rendimiento de red. El valor predeterminado es `false`.|  
  
### <a name="child-elements"></a>Elementos secundarios  
 Ninguno.  
  
### <a name="parent-elements"></a>Elementos primarios  
  
|Elemento|Descripción|  
|-------------|-----------------|  
|[settings](../../../../../docs/framework/configure-apps/file-schema/network/settings-element-network-settings.md)|Configura opciones de red básicas para el espacio de nombres <xref:System.Net>.|  
  
## <a name="remarks"></a>Comentarios  
 Este elemento se puede usar en el archivo de configuración de la aplicación o en el archivo de configuración del equipo (Machine.config).  
  
 Los contadores de rendimiento de red deben estar habilitados en el archivo de configuración que se usará. Todos los contadores de rendimiento red se habilitan o deshabilitan con un solo valor en el archivo de configuración. Los contadores de rendimiento de red individuales no pueden habilitarse ni deshabilitarse. Para obtener más información sobre los contadores de rendimiento de red específicas, consulte [contadores de rendimiento de red](../../../../../docs/framework/debug-trace-profile/performance-counters.md#networking).  
  
 El valor predeterminado es que se deshabilitan los contadores de rendimiento en la red.  
  
 El <xref:System.Net.Configuration.PerformanceCountersElement.Enabled%2A?displayProperty=nameWithType> propiedad puede usarse para obtener el valor actual de la **habilitado** atributo desde archivos de configuración aplicables.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente muestra cómo configurar el <xref:System.Net> y espacios de nombres para habilitar los contadores de rendimiento de red relacionados.  
  
```xml  
<configuration>  
  <system.net>  
    <settings>  
      <performanceCounters  
        enabled="true"  
      />  
    </settings>  
  </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a>Vea también
- <xref:System.Net.Configuration.PerformanceCountersElement?displayProperty=nameWithType>
- <xref:System.Net.Configuration.PerformanceCountersElement.Enabled%2A?displayProperty=nameWithType>
- [Esquema de la configuración de red](../../../../../docs/framework/configure-apps/file-schema/network/index.md)
- [Contadores de rendimiento de red](../../../../../docs/framework/debug-trace-profile/performance-counters.md#networking)
