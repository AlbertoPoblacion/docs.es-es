---
title: Overridable (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- Overridable
- vb.Overridable
helpviewer_keywords:
- elements [Visual Basic], concrete
- properties [Visual Basic], redefining
- overriding, Overridable keyword
- elements [Visual Basic], virtual
- virtual [elements VB]
- procedures [Visual Basic], overriding
- concrete [elements VB]
- procedures [Visual Basic], redefining
- Overridable keyword [Visual Basic]
- properties [Visual Basic], overriding
ms.assetid: 612581e7-8a4c-4a5d-beff-3402fffa6f35
ms.openlocfilehash: 91a1cedc66fd66e336b6e7976ad87ad638cb43c3
ms.sourcegitcommit: bce0586f0cccaae6d6cbd625d5a7b824d1d3de4b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/02/2019
ms.locfileid: "58816891"
---
# <a name="overridable-visual-basic"></a>Overridable (Visual Basic)
Especifica que una propiedad o procedimiento puede reemplazarse por una propiedad con el mismo nombre o un procedimiento en una clase derivada.  
  
## <a name="remarks"></a>Comentarios  
 El `Overridable` modificador permite que una propiedad o método en una clase que se invalide en una clase derivada. El [NotOverridable](../../../visual-basic/language-reference/modifiers/notoverridable.md) modificador evita que una propiedad o método que se invalida en una clase derivada.  Para más información, vea [Fundamentos de la herencia](../../../visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics.md).  
  
 Si el `Overridable` o `NotOverridable` modificador no se especifica, el valor predeterminado depende de si la propiedad o método invalida un método o propiedad de clase base. Si la propiedad o método reemplaza un método o propiedad de clase base, el valor predeterminado es `Overridable`; en caso contrario, es `NotOverridable`.  
  
 Puede ocultar o reemplazar para volver a definir un elemento heredado, pero hay diferencias significativas entre los dos enfoques. Para obtener más información, consulte [sombrear en Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/shadowing.md).  
  
 Un elemento que se puede invalidar a veces se conoce como un *virtual* elemento. Si se puede invalidar, pero no tiene que ser, a veces también se denomina un *concreta* elemento.  
  
 Puede usar `Overridable` únicamente en una instrucción de declaración de procedimiento o propiedad.  
  
## <a name="combined-modifiers"></a>Modificadores combinados  
 No puede especificar `Overridable` o `NotOverridable` para un `Private` método.  
  
 No puede especificar `Overridable` junto con `MustOverride`, `NotOverridable`, o `Shared` en la misma declaración.  
  
 Dado que un elemento de reemplazo es reemplazable de forma implícita, no se puede combinar `Overridable` con `Overrides`.  
  
## <a name="usage"></a>Uso  
 El modificador `Overridable` se puede utilizar en los contextos siguientes:  
  
 [Function (instrucción)](../../../visual-basic/language-reference/statements/function-statement.md)  
  
 [Property (instrucción)](../../../visual-basic/language-reference/statements/property-statement.md)  
  
 [Sub (instrucción)](../../../visual-basic/language-reference/statements/sub-statement.md)  
  
## <a name="see-also"></a>Vea también

- [Modificadores](../../../visual-basic/language-reference/modifiers/index.md)
- [Fundamentos de la herencia](../../../visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics.md)
- [MustOverride](../../../visual-basic/language-reference/modifiers/mustoverride.md)
- [NotOverridable](../../../visual-basic/language-reference/modifiers/notoverridable.md)
- [Overrides](../../../visual-basic/language-reference/modifiers/overrides.md)
- [Palabras clave](../../../visual-basic/language-reference/keywords/index.md)
- [Sombrear en Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/shadowing.md)
