---
title: Elemento <requestCaching> (configuración de red)
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#requestCaching
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/requestCaching
helpviewer_keywords:
- requestCaching element
- <requestCaching> element
ms.assetid: 9962a2fe-cbda-41a6-9377-571811eaea84
ms.openlocfilehash: f0979d2e0caeb0b22b90572aef0ad53235020f1d
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2019
ms.locfileid: "71697827"
---
# <a name="requestcaching-element-network-settings"></a>Elemento \<requestCaching> (configuración de red)
Controla el mecanismo de almacenamiento en caché para las solicitudes de red.  
  
[ **\<configuration>** ](../configuration-element.md)  
&nbsp;&nbsp;[ **\<System. net >** ](system-net-element-network-settings.md)  
&nbsp;&nbsp;&nbsp;&nbsp; **\<requestCaching >**  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
<requestCaching  
  isPrivateCache ="true|false"  
  disableAllCaching="true|false"  
  defaultPolicyLevel="BypassCache|Default|CacheOnly|CacheIfAvailable|Revalidate|Reload|NoCacheNoStore|Revalidate"  
  unspecifiedMaximumAge= "d.hh.mm.ss">  
    <defaultHttpCachePolicy>...</defaultHttpCachePolicy>  
    <defaultFtpCachePolicy>...</defaultFtpCachePolicy>  
</requestCaching>
```  
  
## <a name="attributes-and-elements"></a>Atributos y elementos  
 En las secciones siguientes se describen atributos, elementos secundarios y elementos primarios.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descripción|  
|---------------|-----------------|  
|`isPrivateCache`|Especifica si la memoria caché proporciona aislamiento entre la información de los distintos usuarios. El valor predeterminado es `true`. Este valor se debe `false` para las aplicaciones de nivel intermedio.|  
|`disableAllCaching`|Especifica que el almacenamiento en caché está deshabilitado para todas las respuestas web y no se puede invalidar mediante programación.|  
|`defaultPolicyLevel`|Uno de los valores de la enumeración <xref:System.Net.Cache.RequestCacheLevel>. El valor predeterminado es `BypassCache`.|  
|`unspecifiedMaximumAge`|Especifica el tiempo predeterminado después del cual el contenido se marca como expirado.|  
  
## <a name="policylevel-attribute"></a>Atributo policyLevel  
  
|Valor|Descripción|  
|-----------|-----------------|  
|`Default`|Devuelve el recurso almacenado en caché si el recurso es nuevo, la longitud del contenido es precisa y los atributos expiración, modificación y longitud del contenido están presentes.|  
|`BypassCache`|Devuelve el recurso del servidor.|  
|`CacheOnly`|Devuelve el recurso almacenado en caché si la longitud del contenido está presente y coincide con el tamaño de entrada.|  
|`CacheIfAvailable`|Devuelve el recurso almacenado en caché si se proporciona la longitud del contenido y coincide con el tamaño de entrada; de lo contrario, el recurso se descarga del servidor y se devuelve al autor de la llamada.|  
|`Revalidate`|Devuelve el recurso almacenado en caché si la marca de tiempo del recurso almacenado en caché es igual que la marca de tiempo del recurso en el servidor; de lo contrario, el recurso se descarga del servidor, se almacena en la memoria caché y se devuelve al autor de la llamada.|  
|`Reload`|Descarga el recurso del servidor, lo almacena en la memoria caché y devuelve el recurso al llamador.|  
|`NoCacheNoStore`|Si existe un recurso almacenado en caché, se elimina. El recurso se descarga del servidor y se devuelve al autor de la llamada.|  
|`Revalidate`|Satisface una solicitud mediante la copia en caché del recurso si la marca de tiempo es igual que la marca de tiempo del recurso en el servidor. de lo contrario, el recurso se descarga del servidor, se presenta al autor de la llamada y se almacena en la memoria caché.|  
  
### <a name="child-elements"></a>Elemento secundario  
  
|Elemento|Descripción|  
|-------------|-----------------|  
|[defaultHttpCachePolicy](defaulthttpcachepolicy-element-network-settings.md)|Elemento opcional.<br /><br /> Describe si el almacenamiento en caché de HTTP está activo y describe la Directiva de almacenamiento en caché predeterminada.|  
|[\<elemento > defaultFtpCachePolicy (configuración de red)](defaultftpcachepolicy-element-network-settings.md)|Elemento opcional.<br /><br /> Describe si el almacenamiento en caché de FTP está activo y describe la Directiva de almacenamiento en caché predeterminada.|  
  
### <a name="parent-elements"></a>Elemento principal  
  
|Elemento|Descripción|  
|-------------|-----------------|  
|[system.net](system-net-element-network-settings.md)|Contiene valores que especifican cómo se conecta .NET Framework a la red.|  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se muestra cómo deshabilitar todo el almacenamiento en caché.  
  
```xml  
<configuration>  
  <system.net>  
    <requestCaching  
      disableAllCaching="true"  
    />  
  </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a>Vea también

- <xref:System.Net.Cache?displayProperty=nameWithType>
- [Esquema de la configuración de red](index.md)
