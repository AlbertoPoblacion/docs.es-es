---
title: <add> Elemento para webRequestModules (configuración de red)
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/webRequestModules/add
- http://schemas.microsoft.com/.NetConfiguration/v2.0#add
helpviewer_keywords:
- <webRequestModules>, add element
- webRequestModules, add element
- add element, webRequestModules
- <add> element, webRequestModules
ms.assetid: 47ec4adc-f39f-4bcd-8680-1ec21fd26890
ms.openlocfilehash: 4c1116c088c12ad3859714c8d75704d0156c12f7
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2019
ms.locfileid: "59188258"
---
# <a name="add-element-for-webrequestmodules-network-settings"></a>\<Agregar > elemento para webRequestModules (configuración de red)
Agrega un módulo de solicitud Web personalizado a la aplicación.  
  
 \<configuration>  
\<system.net>  
\<webRequestModules>  
\<add>  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
<add   
  prefix="URI prefix"   
  type="type_fullname, assembly_fullname"   
/>  
```  
  
## <a name="attributes-and-elements"></a>Atributos y elementos  
 En las siguientes secciones se describen los atributos, los elementos secundarios y los elementos primarios.  
  
### <a name="attributes"></a>Atributos  
  
|**Atributo**|**Descripción**|  
|-------------------|---------------------|  
|`prefix`|El prefijo URI para las solicitudes administradas por este módulo de solicitud Web.|  
|`type`|El nombre de tipo completo (indicado por el <xref:System.Type.FullName%2A> propiedad) y el nombre del ensamblado (indicado por el <xref:System.Reflection.Assembly.FullName%2A> propiedad), separados por punto y coma, que implementa este módulo de solicitud Web.|  
  
### <a name="child-elements"></a>Elementos secundarios  
 Ninguno.  
  
### <a name="parent-elements"></a>Elementos primarios  
  
|**Elemento**|**Descripción**|  
|-----------------|---------------------|  
|[webRequestModules](../../../../../docs/framework/configure-apps/file-schema/network/webrequestmodules-element-network-settings.md)|Especifica los módulos que se utilizan para solicitar información de hosts de la red.|  
  
## <a name="remarks"></a>Comentarios  
 El `prefix` atributo define el prefijo URI que utiliza el módulo de solicitud Web especificado. Módulos de solicitud Web se registran normalmente para controlar un protocolo específico, como HTTP o FTP, pero se pueden registrar para controlar una solicitud a un servidor específico o una ruta de acceso en un servidor.  
  
 El módulo de solicitud Web se crea cuando se pasa a la <xref:System.Net.WebRequest.Create%2A?displayProperty=nameWithType> método.  
  
 El valor de la `prefix` atributo debe ser los primeros caracteres de un URI válido. Por ejemplo: `http` o `http://www.contoso.com`.
  
 El valor de la `type` atributo debe ser un nombre de tipo válido y el nombre de ensamblado correspondiente, separados por comas.
  
## <a name="configuration-files"></a>Archivos de configuración  
 Este elemento se puede usar en el archivo de configuración de la aplicación o en el archivo de configuración del equipo (Machine.config).  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente registra un módulo de solicitud Web personalizado para HTTP. Debe reemplazar los valores de versión y PublicKeyToken con los valores correctos para el módulo especificado.  
  
```xml  
<configuration>  
  <system.net>  
    <webRequestModules>  
      <add prefix="http"  
           type="System.Net.HttpRequestCreator, System, Version=2.0.3600.0,  
           Culture=neutral, PublicKeyToken=b77a5c561934e089"  
      />  
    </webRequestModules>  
  </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a>Vea también

- <xref:System.Net.WebRequest>
- [Esquema de la configuración de red](../../../../../docs/framework/configure-apps/file-schema/network/index.md)
