---
title: Evento &#39; &lt;eventname1&gt; &#39; no se puede implementar el evento &#39; &lt;eventname2&gt; &#39; en interfaz &#39; &lt;interfaz&gt; &#39; porque sus tipos delegados &#39; &lt;delegate1&gt; &#39; y &#39; &lt;delegate2&gt; &#39; no coinciden
ms.date: 07/20/2015
f1_keywords:
- vbc31423
- bc31423
helpviewer_keywords:
- BC31423
ms.assetid: 2e754b66-5836-48ff-9697-b9c0d7085f18
ms.openlocfilehash: 024e260f12d3497d64f26e59521f016ad439ebb6
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/23/2019
ms.locfileid: "54638219"
---
# <a name="event-39lteventname1gt39-cannot-implement-event-39lteventname2gt39-on-interface-39ltinterfacegt39-because-their-delegate-types-39ltdelegate1gt39-and-39ltdelegate2gt39-do-not-match"></a>Evento &#39; &lt;eventname1&gt; &#39; no se puede implementar el evento &#39; &lt;eventname2&gt; &#39; en interfaz &#39; &lt;interfaz&gt; &#39; porque sus tipos delegados &#39; &lt;delegate1&gt; &#39; y &#39; &lt;delegate2&gt; &#39; no coinciden
Visual Basic no puede implementar un evento porque el tipo de delegado del evento no coincide con el tipo de delegado del evento en la interfaz. Este error puede producirse cuando define varios eventos en una interfaz e intenta implementarlos juntos con el mismo evento. Un evento puede implementar dos o más eventos solo si todos los eventos implementados se declaran con la sintaxis `As` y si se especifica el mismo tipo delegado.  
  
 **Identificador de error:** BC31423  
  
## <a name="to-correct-this-error"></a>Para corregir este error  
  
-   Implemente los eventos por separado.  
  
     -O bien-  
  
-   Definir los eventos en la interfaz usando el `As` sintaxis y especifique el mismo tipo de delegado.  
  
## <a name="see-also"></a>Vea también
- [Event (instrucción)](../../../visual-basic/language-reference/statements/event-statement.md)
- [Delegate (instrucción)](../../../visual-basic/language-reference/statements/delegate-statement.md)
- [Eventos](../../../visual-basic/programming-guide/language-features/events/index.md)
