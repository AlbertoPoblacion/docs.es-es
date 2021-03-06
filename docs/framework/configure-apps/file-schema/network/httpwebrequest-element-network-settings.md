---
title: '&lt;httpWebRequest&gt; elemento (configuración de red)'
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/settings/httpWebRequest
- http://schemas.microsoft.com/.NetConfiguration/v2.0#httpWebRequest
helpviewer_keywords:
- <httpWebRequest> element
- httpWebRequest element
ms.assetid: 52acd9d2-5bdc-4dc4-9c2a-f0a476ccbb31
ms.openlocfilehash: 1a883b2e57d0f055237d68e4f69651ef496795ab
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/23/2019
ms.locfileid: "54590040"
---
# <a name="lthttpwebrequestgt-element-network-settings"></a>&lt;httpWebRequest&gt; elemento (configuración de red)
Personaliza los parámetros de solicitud Web.  
  
 \<configuration>  
\<system.net>  
\<settings>  
\<httpWebRequest>  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
<httpWebRequest  
  maximumResponseHeadersLength="size"  
  maximumErrorResponseLength="size"  
  maximumUnauthorizedUploadLength="size"  
  useUnsafeHeaderParsing="true|false"  
/>  
```  
  
## <a name="attributes-and-elements"></a>Atributos y elementos  
 En las siguientes secciones se describen los atributos, los elementos secundarios y los elementos primarios.  
  
### <a name="attributes"></a>Atributos  
  
|**Attribute**|**Descripción**|  
|-------------------|---------------------|  
|`maximumResponseHeadersLength`|Especifica la longitud máxima de un encabezado de respuesta, en kilobytes. El valor predeterminado es 64. El valor -1 indica que no se impondrá ningún límite de tamaño en los encabezados de respuesta.|  
|`maximumErrorResponseLength`|Especifica la longitud máxima de una respuesta de error, en kilobytes. El valor predeterminado es 64. El valor -1 indica que no hay límite de tamaño se impondrá en la respuesta de error.|  
|`maximumUnauthorizedUploadLength`|Especifica la longitud máxima de una carga en respuesta a un código de error no autorizado, en bytes. El valor predeterminado es -1. El valor -1 indica que no hay límite de tamaño se impondrá en la carga.|  
|`useUnsafeHeaderParsing`|Especifica si está habilitado el análisis de encabezado no segura. El valor predeterminado es `false`.|  
  
### <a name="child-elements"></a>Elementos secundarios  
 Ninguno.  
  
### <a name="parent-elements"></a>Elementos primarios  
  
|**Element**|**Descripción**|  
|-----------------|---------------------|  
|[settings](../../../../../docs/framework/configure-apps/file-schema/network/settings-element-network-settings.md)|Configura opciones de red básicas para el espacio de nombres <xref:System.Net>.|  
  
## <a name="remarks"></a>Comentarios  
 De forma predeterminada, .NET Framework aplica estrictamente RFC 2616 para analizar URI. Algunas respuestas del servidor pueden incluir caracteres de control en campos prohibidos, lo que hará que el <xref:System.Net.HttpWebRequest.GetResponse?displayProperty=nameWithType> método inicie una <xref:System.Net.WebException>. Si **useUnsafeHeaderParsing** está establecido en **true**, <xref:System.Net.HttpWebRequest.GetResponse?displayProperty=nameWithType> no iniciará ninguna en este caso; sin embargo, la aplicación será vulnerable a varias formas de ataques de análisis de URI. La mejor solución es cambiar el servidor de modo que la respuesta no incluya caracteres de control.  
  
## <a name="configuration-files"></a>Archivos de configuración  
 Este elemento se puede usar en el archivo de configuración de la aplicación o en el archivo de configuración del equipo (Machine.config).  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente muestra cómo especificar una mayor que la longitud máxima de encabezado normal.  
  
```xml  
<configuration>  
  <system.net>  
    <settings>  
      <httpWebRequest  
        maximumResponseHeadersLength="128"  
      />  
    </settings>  
  </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a>Vea también
- <xref:System.Net.HttpWebRequest.MaximumResponseHeadersLength%2A>
- [Esquema de la configuración de red](../../../../../docs/framework/configure-apps/file-schema/network/index.md)
