---
title: <defaultProxy> Elemento (configuración de red)
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#defaultProxy
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/defaultProxy
helpviewer_keywords:
- defaultProxy element
- <defaultProxy> element
ms.assetid: 9d663c4b-07b4-4f6f-9b12-efbd3630354f
ms.openlocfilehash: ce08dadb0fb7b986c0573b1514f9ecbbe2961c3a
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2019
ms.locfileid: "59228352"
---
# <a name="defaultproxy-element-network-settings"></a>\<defaultProxy > elemento (configuración de red)
Configura el servidor proxy de Protocolo de transferencia de hipertexto (HTTP).  
  
 \<configuration>  
\<system.net>  
\<defaultProxy>  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
<defaultProxy  
  enabled="true|false"  
  useDefaultCredentials="true|false">  
    <bypasslist>...</bypasslist>  
    <proxy>...</proxy>  
    <module>...</module>  
</defaultProxy>
```  
  
## <a name="attributes-and-elements"></a>Atributos y elementos  
 En las siguientes secciones se describen los atributos, los elementos secundarios y los elementos primarios.  
  
### <a name="attributes"></a>Atributos  
  
|**Elemento**|**Descripción**|  
|-----------------|---------------------|  
|`enabled`|Especifica si se usa un proxy web. El valor predeterminado es `true`.|  
|`useDefaultCredentials`|Especifica si se usan las credenciales predeterminadas de este host para tener acceso al proxy web. El valor predeterminado es `false`.|  
  
### <a name="child-elements"></a>Elementos secundarios  
  
|**Elemento**|**Descripción**|  
|-----------------|---------------------|  
|[bypasslist](../../../../../docs/framework/configure-apps/file-schema/network/bypasslist-element-network-settings.md)|Proporciona un conjunto de expresiones regulares que describen direcciones que no usan el proxy.|  
|[module](../../../../../docs/framework/configure-apps/file-schema/network/module-element-network-settings.md)|Agrega un nuevo módulo proxy a la aplicación.|  
|[proxy](../../../../../docs/framework/configure-apps/file-schema/network/proxy-element-network-settings.md)|Define un servidor proxy.|  
  
### <a name="parent-elements"></a>Elementos primarios  
  
|**Elemento**|**Descripción**|  
|-----------------|---------------------|  
|[system.net](../../../../../docs/framework/configure-apps/file-schema/network/system-net-element-network-settings.md)|Contiene valores que especifican cómo se conecta .NET Framework a la red.|  
  
## <a name="remarks"></a>Comentarios  
 Si el elemento defaultProxy está vacío, se usará la configuración de proxy de Internet Explorer. Este comportamiento es diferente de la versión 1.1 de .NET Framework.  
  
 Se produce una excepción si el [módulo](../../../../../docs/framework/configure-apps/file-schema/network/module-element-network-settings.md) elemento especifica un tipo no público, el tipo no deriva de la <xref:System.Net.IWebProxy> (clase), se produjo una excepción en el constructor predeterminado de este objeto, o se produjo una excepción mientras Recuperando al proxy predeterminado especificado por el sistema. La propiedad <xref:System.Exception.InnerException%2A> en la excepción debería tener más información acerca de la causa principal del error.  
  
## <a name="configuration-files"></a>Archivos de configuración  
 Este elemento se puede usar en el archivo de configuración de la aplicación o en el archivo de configuración del equipo (Machine.config).  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente utiliza los valores predeterminados desde el proxy de Internet Explorer, especifica la dirección del proxy y omite al proxy para el acceso local y contoso.com.  
  
```xml  
<configuration>  
  <system.net>  
    <defaultProxy>  
      <proxy  
        usesystemdefault="true"  
        proxyaddress="http://192.168.1.10:3128"  
        bypassonlocal="true"  
      />  
      <bypasslist>  
        <add address="[a-z]+\.contoso\.com$" />  
      </bypasslist>  
    </defaultProxy>  
  </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a>Vea también

- <xref:System.Net.WebProxy?displayProperty=nameWithType>
- [Esquema de la configuración de red](../../../../../docs/framework/configure-apps/file-schema/network/index.md)
