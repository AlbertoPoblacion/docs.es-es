---
ms.openlocfilehash: 2bb40294685c987de84138ee889e6b88f7184bb0
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2019
ms.locfileid: "67857208"
---
### <a name="chained-popups-with-staysopenfalse"></a>Menús emergentes encadenados con StaysOpen=False

|   |   |
|---|---|
|Detalles|Se supone que un menú emergente con StaysOpen=False se cierra al hacer clic fuera de la ventana emergente. Cuando se encadenaban dos o más de estos elementos Popup (es decir, uno contiene al otro), se producían muchos problemas, incluidos los siguientes:<ul><li>Se abren dos niveles, se hace clic fuera de P2 pero dentro de P1.  No sucede nada.</li><li>Se abren dos niveles, se hace clic fuera de P1.  Los dos menús emergentes se cierran.</li><li>Se abren y se cierran dos niveles.  Después, se intenta volver a abrir P2.  No sucede nada.</li><li>Se intenta abrir tres niveles.  No se puede.  (No sucede nada o se cierra el primero de los dos niveles, en función de dónde se hizo clic). Estos casos (y otras variantes) ahora funcionan según lo esperado.</li></ul>|
|Ámbito|Borde|
|Versión|4.7.1|
|Tipo|Tiempo de ejecución|
|API afectadas|<ul><li><xref:System.Windows.Controls.Primitives.Popup.StaysOpen?displayProperty=nameWithType></li></ul>|

