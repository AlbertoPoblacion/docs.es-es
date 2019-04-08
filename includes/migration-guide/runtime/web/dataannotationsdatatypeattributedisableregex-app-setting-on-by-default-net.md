---
ms.openlocfilehash: 4daa08ce4bbcfe5a7242f19506811e422d0477b7
ms.sourcegitcommit: 0aca6c5d166d7961a1e354c248495645b97a1dc5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/01/2019
ms.locfileid: "58760756"
---
### <a name="dataannotationsdatatypeattributedisableregex-app-setting-is-on-by-default-in-net-framework-472"></a>La configuración de aplicación "dataAnnotations:dataTypeAttribute:disableRegEx" está activada de manera predeterminada en .NET Framework 4.7.2.

|   |   |
|---|---|
|Detalles|En .NET Framework 4.6.1, se incluyó una configuración de aplicación (<code>&quot;dataAnnotations:dataTypeAttribute:disableRegEx&quot;</code>) que permite a los usuarios deshabilitar el uso de expresiones regulares en atributos de tipos de datos (como <xref:System.ComponentModel.DataAnnotations.EmailAddressAttribute?displayProperty=nameWithType>, <xref:System.ComponentModel.DataAnnotations.UrlAttribute?displayProperty=nameWithType> y <xref:System.ComponentModel.DataAnnotations.PhoneAttribute?displayProperty=nameWithType>). Esto ayuda a reducir la vulnerabilidad de la seguridad, ya que se evita la posibilidad de un ataque por denegación de servicio con expresiones regulares específicas.<br/>En .NET Framework 4.6.1, esta configuración de aplicación para deshabilitar el uso de expresiones regulares se estableció en <code>false</code> de manera predeterminada. A partir de .NET Framework 4.7.2, este conmutador de configuración está establecido en <code>true</code> de manera predeterminada para reducir todavía más la vulnerabilidad de la seguridad para aplicaciones web que tengan como objetivo .NET Framework 4.7.2 y versiones superiores.|
|Sugerencia|Si las expresiones regulares de su aplicación web no funcionan después de actualizar a .NET Framework 4.7.2, puede actualizar el valor de la configuración <code>&quot;dataAnnotations:dataTypeAttribute:disableRegEx&quot;</code> a <code>false</code> para volver al comportamiento anterior.<pre><code class="lang-xml">&lt;configuration&gt;&#13;&#10;&lt;appsettings&gt;&#13;&#10;...&#13;&#10;&lt;add key=&quot;dataAnnotations:dataTypeAttribute:disableRegEx&quot; value=&quot;false&quot;/&gt;&#13;&#10;...&#13;&#10;&lt;/appsettings&gt;&#13;&#10;&lt;/configuration&gt;&#13;&#10;</code></pre>|
|Ámbito|Secundaria|
|Versión|4.7.2|
|Tipo|Tiempo de ejecución|

