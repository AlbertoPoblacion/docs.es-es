---
ms.openlocfilehash: e4cf139d308a1c12425d966a84d59a0c3bb89712
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2019
ms.locfileid: "59236536"
---
### <a name="nullreferenceexception-in-exception-handling-code-from-imagesourceconverterconvertfrom"></a>Excepción NullReferenceException en el código de control de excepciones de ImageSourceConverter.ConvertFrom

|   |   |
|---|---|
|Detalles|Un error en el código de control de excepciones para <xref:System.Windows.Media.ImageSourceConverter.ConvertFrom(System.ComponentModel.ITypeDescriptorContext,System.Globalization.CultureInfo,System.Object)> provocaba que se iniciase una excepción <xref:System.NullReferenceException?displayProperty=name> incorrecta en lugar de la excepción prevista (como <xref:System.IO.DirectoryNotFoundException?displayProperty=name> o <xref:System.IO.FileNotFoundException?displayProperty=name>). Este cambio corrige el error para que el método produzca la excepción correcta. <p/>De forma predeterminada, todas las aplicaciones destinadas a .NET Framework 4.6.2 y versiones anteriores continuarán iniciando la excepción <xref:System.NullReferenceException?displayProperty=name> por motivos de compatibilidad. Los desarrolladores que seleccionen como destino .NET Framework 4.7 y versiones posteriores debería ver las excepciones correctas.|
|Sugerencia|Los desarrolladores que quieran volver a obtener <xref:System.NullReferenceException?displayProperty=name> cuando el destino sea .NET Framework 4.7, pueden agregar o combinar lo siguiente en el archivo App.config de la aplicación:<pre><code class="lang-xml">&lt;configuration&gt;&#13;&#10;&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Windows.Media.ImageSourceConverter.OverrideExceptionWithNullReferenceException=true&quot;/&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;&lt;/configuration&gt;&#13;&#10;</code></pre>|
|Ámbito|Borde|
|Versión|4.7|
|Tipo|Redestinación|
|API afectadas|<ul><li><xref:System.Windows.Media.ImageSourceConverter.ConvertFrom(System.ComponentModel.ITypeDescriptorContext,System.Globalization.CultureInfo,System.Object)?displayProperty=nameWithType></li></ul>|
