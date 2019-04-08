---
ms.openlocfilehash: 38c50244b1cee41bd95c232ac5d1691c59c55488
ms.sourcegitcommit: 0aca6c5d166d7961a1e354c248495645b97a1dc5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/01/2019
ms.locfileid: "58760935"
---
### <a name="wpf-focusvisual-for-radiobutton-and-checkbox-now-displays-correctly-when-the-controls-have-no-content"></a>Ahora FocusVisual de WPF para los controles RadioButton y CheckBox se muestra correctamente cuando los controles no tienen contenido

|   |   |
|---|---|
|Detalles|En .NET Framework 4.7.1 y versiones anteriores, los controles <xref:System.Windows.Controls.CheckBox?displayProperty=nameWIthType> y <xref:System.Windows.Controls.RadioButton?displayProperty=nameWIthType> de WPF tenían objetos visuales de foco incoherentes y, en los temas Clásico y Contraste alto, eran incorrectos.  Estos problemas se producen en casos en los que no se ha definido ningún contenido para los controles.  Esto puede hacer que la transición entre los temas sea confusa y el objeto visual de foco difícil de ver. En .NET Framework 4.7.2, estos objetos visuales son ahora más coherentes entre los temas y se ven más fácilmente en los temas Clásico y Contraste alto.|
|Sugerencia|Un desarrollador que seleccione como destino .NET Framework 4.7.2 y que quiera revertir al comportamiento de .NET 4.7.1 tendrá que establecer la marca de AppContext siguiente.<pre><code class="lang-xml">&lt;configuration&gt;&#13;&#10;&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.UseLegacyAccessibilityFeatures.2=true;&quot;/&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;&lt;/configuration&gt;&#13;&#10;</code></pre>Un desarrollador que quiera usar este cambio mientras selecciona como destino una versión de .NET Framework inferior a 4.7.2 debe establecer las marcas de AppContext siguientes. Tenga en cuenta que todas las marcas se deben establecer correctamente y que la versión instalada de .NET Framework debe ser 4.7.2 o posterior. Es necesario que las aplicaciones de WPF participen en todas las mejoras de accesibilidad anteriores para obtener las mejoras más recientes. Para ello, asegúrese de que los modificadores "Switch.UseLegacyAccessibilityFeatures" y "Switch.UseLegacyAccessibilityFeatures.2" de AppContext se establezcan en false.<pre><code class="lang-xml">&lt;configuration&gt;&#13;&#10;&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.UseLegacyAccessibilityFeatures=false;Switch.UseLegacyAccessibilityFeatures.2=false;&quot;/&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;&lt;/configuration&gt;&#13;&#10;</code></pre>|
|Ámbito|Borde|
|Versión|4.7.2|
|Tipo|Redestinación|

