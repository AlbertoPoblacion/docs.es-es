---
ms.openlocfilehash: 5a45d616001be5a2a2bdf2c654c10526125d7d86
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2019
ms.locfileid: "67802683"
---
### <a name="svctraceviewer-combobox-high-contrast-change"></a>Cambio de contraste alto de ComboBox svcTraceViewer

|   |   |
|---|---|
|Detalles|En la [herramienta Service Trace Viewer de Microsoft](~/docs/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe.md), los controles ComboBox no se mostraban en el color correcto en ciertos temas de contraste alto. El problema se ha corregido en .NET Framework 4.7.2. Sin embargo, debido a los requisitos de compatibilidad con versiones anteriores del SDK de .NET Framework, la corrección no era visible para los clientes de forma predeterminada. .NET 4.8 manifiesta este cambio agregando los siguientes [modificadores de configuración AppContext](~/docs/framework/configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) al archivo svcTraceViewer.exe.config:<pre><code class="lang-xml">&lt;AppContextSwitchOverrides value=&quot;Switch.UseLegacyAccessibilityFeatures=false;Switch.UseLegacyAccessibilityFeatures.2=false&quot; /&gt;&#13;&#10;</code></pre>|
|Sugerencia|<ul><li>Cómo no participar en el cambio: si no desea que se produzca el cambio de comportamiento de contraste alto, puede deshabilitarlo mediante la eliminación de la siguiente sección del archivo svcTraceViewer.exe.config:</li></ul><pre><code class="lang-xml">&lt;AppContextSwitchOverrides value=&quot;Switch.UseLegacyAccessibilityFeatures=false;Switch.UseLegacyAccessibilityFeatures.2=false&quot; /&gt;&#13;&#10;</code></pre>|
|Ámbito|Borde|
|Versión|4.8|
|Tipo|Tiempo de ejecución|

