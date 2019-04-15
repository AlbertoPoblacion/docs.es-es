---
ms.openlocfilehash: 946096cb9510ca12bbd2cecd00099142308b072a
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2019
ms.locfileid: "59236154"
---
### <a name="keytips-behavior-improved-in-wpf"></a>Mejora del comportamiento de los KeyTip en WPF

|   |   |
|---|---|
|Detalles|El comportamiento de los KeyTip se ha modificado para equipararlo al de Microsoft Word y el Explorador de Windows. Mediante la comprobación de si el estado del KeyTip está habilitado o no cuando se presiona una <xref:System.Windows.Input.KeyEventArgs.SystemKey> (en concreto, <xref:System.Windows.Input.Key> o <xref:System.Windows.Input.Key.F11>), WPF administra las teclas de KeyTip de la forma adecuada. Los KeyTip ahora cierran un menú incluso cuando se abre con el mouse.|
|Sugerencia|N/D|
|Ámbito|Borde|
|Versión|4.7.2|
|Tipo|Tiempo de ejecución|
