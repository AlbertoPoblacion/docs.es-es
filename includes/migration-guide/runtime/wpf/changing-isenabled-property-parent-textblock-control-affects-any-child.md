---
ms.openlocfilehash: 735278848cb7399e414a128afc650a0a1f882337
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2019
ms.locfileid: "59236069"
---
### <a name="changing-the-isenabled-property-of-the-parent-of-a-textblock-control-affects-any-child-controls"></a>El cambio de la propiedad IsEnabled del elemento primario de un control TextBlock afecta a todos los controles secundarios

|   |   |
|---|---|
|Detalles|A partir de .NET Framework 4.6.2, el cambio de la propiedad <xref:System.Windows.UIElement.IsEnabled?displayProperty=name> del elemento primario de un control <xref:System.Windows.Controls.TextBlock?displayProperty=name> afecta a todos los controles secundarios (como los hipervínculos y los botones) del control <xref:System.Windows.Controls.TextBlock?displayProperty=name>. En .NET Framework 4.6.1 y versiones anteriores, los controles dentro de un <xref:System.Windows.Controls.TextBlock?displayProperty=name> no siempre reflejaban el estado de la propiedad <xref:System.Windows.UIElement.IsEnabled?displayProperty=name> del elemento <xref:System.Windows.Controls.TextBlock?displayProperty=name> primario.|
|Sugerencia|Ninguno. Este cambio se ajusta al comportamiento esperado de los controles dentro de un control <xref:System.Windows.Controls.TextBlock?displayProperty=name>.|
|Ámbito|Secundaria|
|Versión|4.6.2|
|Tipo|Tiempo de ejecución|
|API afectadas|<ul><li><xref:System.Windows.UIElement.IsEnabled?displayProperty=nameWithType></li></ul>|
