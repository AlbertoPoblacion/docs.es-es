---
title: '&lt;quitar&gt; elemento para schemeSettings (configuración de Uri)'
ms.date: 03/30/2017
ms.assetid: 4095ba51-de20-4f87-b562-018abe422c91
ms.openlocfilehash: 2a2ef83ac57c1978a0022a9c989aa03eeae8a71f
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/23/2019
ms.locfileid: "54552832"
---
# <a name="ltremovegt-element-for-schemesettings-uri-settings"></a>&lt;quitar&gt; elemento para schemeSettings (configuración de Uri)
Quita un valor de esquema para un nombre de esquema.  
  
 \<configuration>  
\<uri>  
\<schemeSettings>  
\<remove>  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
<remove
  name="http|https"
/>
```  
  
## <a name="attributes-and-elements"></a>Atributos y elementos  
 En las siguientes secciones se describen los atributos, los elementos secundarios y los elementos primarios.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descripción|  
|---------------|-----------------|  
|name|El nombre de esquema que se aplica esta configuración. Los únicos valores compatibles son el nombre = "http" y el nombre = "https".|  
  
### <a name="child-elements"></a>Elementos secundarios  
 Ninguno.  
  
### <a name="parent-elements"></a>Elementos primarios  
  
|Elemento|Descripción|  
|-------------|-----------------|  
|[Elemento \<schemeSettings> (configuración de URI)](../../../../../docs/framework/configure-apps/file-schema/network/schemesettings-element-uri-settings.md)|Especifica cómo se analizará un <xref:System.Uri> para esquemas concretos.|  
  
## <a name="remarks"></a>Comentarios  
 De forma predeterminada, el <xref:System.Uri?displayProperty=nameWithType> delimitadores de ruta de acceso de codificación de porcentaje de anular los caracteres de escape de clase antes de ejecutar la compresión de la ruta de acceso. Esto se implementó como un mecanismo de seguridad frente a ataques similar al siguiente:  
  
 `http://www.contoso.com/..%2F..%2F/Windows/System32/cmd.exe?/c+dir+c:\`  
  
 Si este URI se pasa a los módulos no se controla por ciento correctamente los caracteres codificados, podría dar como resultado el siguiente comando que se está ejecutando el servidor:  
  
 `c:\Windows\System32\cmd.exe /c dir c:\`  
  
 Por este motivo, <xref:System.Uri?displayProperty=nameWithType> delimitadores de ruta de acceso de primera anular los caracteres de escape de clase y, a continuación, aplica la compresión de la ruta de acceso. El resultado de pasar la dirección URL malintencionada anterior a <xref:System.Uri?displayProperty=nameWithType> clase constructor produce el siguiente URI:  
  
 `http://www.microsoft.com/Windows/System32/cmd.exe?/c+dir+c:\`  
  
 Este comportamiento predeterminado puede modificarse para no escape de un porcentaje de ruta de acceso codificada delimitadores de mediante la opción de configuración schemeSettings para un esquema específico.  
  
## <a name="configuration-files"></a>Archivos de configuración  
 Este elemento se puede usar en el archivo de configuración de la aplicación o en el archivo de configuración del equipo (Machine.config).  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente muestra una configuración utilizada por el <xref:System.Uri> clase que quita cualquier configuración de esquema para el esquema http.  
  
```xml  
<configuration>  
  <uri>  
    <schemeSettings>  
      <remove name="http"/>  
    </schemeSettings>  
  </uri>  
</configuration>  
```  
  
## <a name="see-also"></a>Vea también
- <xref:System.Configuration.SchemeSettingElement?displayProperty=nameWithType>
- <xref:System.Configuration.SchemeSettingElementCollection?displayProperty=nameWithType>
- <xref:System.Configuration.UriSection?displayProperty=nameWithType>
- <xref:System.Configuration.UriSection.SchemeSettings%2A?displayProperty=nameWithType>
- <xref:System.GenericUriParserOptions?displayProperty=nameWithType>
- <xref:System.Uri?displayProperty=nameWithType>
- [Esquema de la configuración de red](../../../../../docs/framework/configure-apps/file-schema/network/index.md)
