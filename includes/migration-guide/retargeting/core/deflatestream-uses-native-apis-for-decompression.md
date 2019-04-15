---
ms.openlocfilehash: 897bb0b0650c633b87a792516c62566f491ec3fd
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2019
ms.locfileid: "59234059"
---
### <a name="deflatestream-uses-native-apis-for-decompression"></a>DeflateStream usa las API nativas para la descompresión

|   |   |
|---|---|
|Detalles|A partir de .NET Framework 4.7.2, la implementación de la descompresión en la clase <code>T:System.IO.Compression.DeflateStream</code> ha cambiado para usar las API nativas de Windows de forma predeterminada. Normalmente, esto da como resultado una mejora considerable del rendimiento. En todas las aplicaciones de .NET que tienen como destino la versión 4.7.2 de .NET Framework o una versión posterior se usa la implementación nativa. Es posible que este cambio provoque algunas diferencias de comportamiento, como las siguientes:<ul><li>Los mensajes de excepción pueden ser diferentes. Pero el tipo de excepción que se inicia sigue siendo el mismo.</li><li>Algunas situaciones especiales, por ejemplo no tener memoria suficiente para completar una operación, se pueden administrar de otra manera.</li><li>Hay diferencias conocidas para el análisis del encabezado de gzip (Nota: Solo se ve afectado <code>GZipStream</code> establecido para la descompresión):</li><li>Se pueden iniciar excepciones al analizar encabezados no válidos en momentos diferentes.</li><li>La implementación nativa exige que los valores para algunas marcas reservadas dentro del encabezado de gzip (es decir, [FLG](http://www.zlib.org/rfc-gzip.html#header-trailer)) se establezcan según la especificación, lo que puede provocar que se inicie una excepción donde anteriormente se ignoraban los valores no válidos.</li></ul>|
|Sugerencia|Si la descompresión con las API nativas ha afectado negativamente el comportamiento de la aplicación, puede descartar esta característica si agrega el modificador <code>Switch.System.IO.Compression.DoNotUseNativeZipLibraryForDecompression</code> a la sección <code>runtime</code> del archivo app.config y lo establece en <code>true</code>:<pre><code class="lang-xml">&lt;?xml version=&quot;1.0&quot; encoding=&quot;utf-8&quot; ?&gt;&#13;&#10;&lt;configuration&gt;&#13;&#10;&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides&#13;&#10;value=&quot;Switch.System.IO.Compression.DoNotUseNativeZipLibraryForDecompression=true&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;&lt;/configuration&gt;&#13;&#10;</code></pre>|
|Ámbito|Secundaria|
|Versión|4.7.2|
|Tipo|Redestinación|
|API afectadas|<ul><li><xref:System.IO.Compression.DeflateStream?displayProperty=nameWithType></li><li><xref:System.IO.Compression.GZipStream?displayProperty=nameWithType></li></ul>|
