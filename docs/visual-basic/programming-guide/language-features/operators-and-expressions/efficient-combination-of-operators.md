---
title: Combinación eficaz de operadores (Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- expressions [Visual Basic], parentheses
- operators [Visual Basic], associativity
- expressions [Visual Basic], operators
- operators [Visual Basic], precedence
- Visual Basic code, operators
- Visual Basic code, expressions
- operators [Visual Basic], complex expressions
- expressions [Visual Basic], complex
- parentheses [Visual Basic], complex expressions
- numeric expressions
ms.assetid: bd22340e-b5be-458b-8772-3916c02309a4
ms.openlocfilehash: 8f5dd6c56b3e4576b9d798e0e5e10b2996f558dc
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "58841275"
---
# <a name="efficient-combination-of-operators-visual-basic"></a>Combinación eficaz de operadores (Visual Basic)
Las expresiones complejas pueden contener muchos operadores diferentes. Esto se ilustra en el siguiente ejemplo:  
  
 `x = (45 * (y + z)) ^ (2 / 85) * 5 + z`  
  
 Crear expresiones complejas, como la mostrada en el ejemplo anterior, requiere un conocimiento exhaustivo de las reglas de precedencia de operadores. Para obtener más información, consulte [prioridad de operador en Visual Basic](../../../../visual-basic/language-reference/operators/operator-precedence.md).  
  
## <a name="parenthetical-expressions"></a>Expresiones entre paréntesis  
 A menudo desean operaciones podrán continuar en un orden diferente del que determina la prioridad de operador. Considere el ejemplo siguiente.  
  
 `x = z * y + 4`  
  
 El ejemplo anterior se multiplica `z` por `y`, a continuación, agrega el resultado a `4`. Sin embargo, si desea agregar `y` y `4` antes de multiplicar el resultado por `z`, puede invalidar la prioridad de operador mediante paréntesis. Si escribe una expresión entre paréntesis, forzar esa expresión se puede evaluar en primer lugar, independientemente de la prioridad de operador. Para forzar que el ejemplo anterior para realizar la adición en primer lugar, podría reescribir como en el ejemplo siguiente.  
  
 `x = z * (y + 4)`  
  
 El ejemplo anterior se agrega `y` y `4`, a continuación, multiplica esa suma por `z`.  
  
### <a name="nested-parenthetical-expressions"></a>Expresiones entre paréntesis anidadas  
 Puede anidar expresiones en varios niveles de paréntesis para invalidar aún más la prioridad. Las expresiones más profundamente anidadas entre paréntesis se evalúan primero, seguido por el siguiente más profundamente anidado, y así sucesivamente para el nivel de anidación y, finalmente, las expresiones fuera de los paréntesis. Esto se ilustra en el siguiente ejemplo:  
  
 `x = (z * 4) ^ (y * (z + 2))`  
  
 En el ejemplo anterior, `z + 2` es evalúa primero y, a continuación, las demás expresiones entre paréntesis. Exponenciación, que generalmente tiene mayor prioridad que la suma o multiplicación, se evalúa en último lugar en este ejemplo porque se incluyen las demás expresiones entre paréntesis.  
  
## <a name="see-also"></a>Vea también

- [Operadores aritméticos en Visual Basic](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)
- [Operadores de comparación en Visual Basic](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/comparison-operators.md)
- [Operadores lógicos y bit a bit en Visual Basic](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/logical-and-bitwise-operators.md)
- [Operadores lógicos y bit a bit (Visual Basic)](../../../../visual-basic/language-reference/operators/logical-bitwise-operators.md)
- [Expresiones booleanas](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/boolean-expressions.md)
- [Comparaciones de valores](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/value-comparisons.md)
- [Cómo: Calcular valores numéricos](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/how-to-calculate-numeric-values.md)
- [Prioridad de operador en Visual Basic](../../../../visual-basic/language-reference/operators/operator-precedence.md)
