---
title: Instrucción If...Then...Else (Visual Basic)
ms.date: 04/16/2018
f1_keywords:
- vb.ElseIf
- vb.Then
- vb.If
- vb.EndIf
helpviewer_keywords:
- ElseIf statement [Visual Basic], If...Then...Else
- Then statement [Visual Basic], If...Then...Else
- control flow [Visual Basic], branching
- execution [Visual Basic], conditional
- TypeOf...Is expression, and If...Then...Else statements
- If...Then...Else statements
- If statement [Visual Basic], If...Then...Else
- If statement [Visual Basic]
- Is operator [Visual Basic], in If...Then...Else statements
- If Operator [Visual Basic]
- branching [Visual Basic], conditional
- If function [Visual Basic], and If...Then...Else statements
- Else statement [Visual Basic]
ms.assetid: 790068a2-1307-4e28-8a72-be5ebda099e9
ms.openlocfilehash: d91a913d515f36a6b974850bc30079b000a919b4
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61637761"
---
# <a name="ifthenelse-statement-visual-basic"></a>Instrucción If...Then...Else (Visual Basic)
Ejecuta condicionalmente un grupo de instrucciones en función del valor de una expresión.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
' Multiline syntax:  
If condition [ Then ]  
    [ statements ]  
[ ElseIf elseifcondition [ Then ]  
    [ elseifstatements ] ]  
[ Else  
    [ elsestatements ] ]  
End If  
  
' Single-line syntax:  
If condition Then [ statements ] [ Else [ elsestatements ] ]  
```  

## <a name="quick-links-to-example-code"></a>Vínculos rápidos a código de ejemplo

En este artículo incluye varios ejemplos que ilustran los usos de la `If`... `Then`... `Else` instrucción:

* [Ejemplo de sintaxis de varias líneas](#multi-line)
* [Ejemplo de sintaxis anidados](#nested)
* [Ejemplo de sintaxis de línea](#single-line)

## <a name="parts"></a>Elementos  
 `condition`  
 Obligatorio. expresión. Se debe evaluar como `True` o `False`, o a un tipo de datos que es implícitamente convertible a `Boolean`.  
  
 Si la expresión es un [Nullable](../../../visual-basic/programming-guide/language-features/data-types/nullable-value-types.md) `Boolean` variable que se evalúa como [nada](../../../visual-basic/language-reference/nothing.md), la condición se trata como si la expresión es `False` y `Else` bloque se ejecuta.  
  
 `Then`  
 Necesario en la sintaxis de línea; opcional en la sintaxis de varias líneas.  
  
 `statements`  
 Opcional. Uno o más instrucciones que siguen `If`... `Then` que se ejecutan si `condition` se evalúa como `True`.  
  
 `elseifcondition`  
 Es necesario si `ElseIf` está presente. expresión. Se debe evaluar como `True` o `False`, o a un tipo de datos que es implícitamente convertible a `Boolean`.  
  
 `elseifstatements`  
 Opcional. Uno o más instrucciones que siguen `ElseIf`... `Then` que se ejecutan si `elseifcondition` se evalúa como `True`.  
  
 `elsestatements`  
 Opcional. Una o varias instrucciones que se ejecutan si anterior no `condition` o `elseifcondition` expresión se evalúa como `True`.  
  
 `End If`  
 Finaliza la versión multilínea del `If`... `Then`... `Else` bloque.  
  
## <a name="remarks"></a>Comentarios  
  
### <a name="multiline-syntax"></a>Sintaxis de varias líneas  
 Cuando un `If`... `Then`... `Else` se encuentra la instrucción, `condition` está probando. Si `condition` es `True`, las instrucciones que siguen `Then` se ejecutan. Si `condition` es `False`, cada `ElseIf` instrucción (si hay alguno) se evalúa en orden. Cuando un `True` `elseifcondition` se encuentra, las instrucciones que siguen inmediatamente asociado `ElseIf` se ejecutan. Si no hay ningún `elseifcondition` se evalúa como `True`, o si no hay ningún `ElseIf` instrucciones, las instrucciones que siguen `Else` se ejecutan. Después de ejecutar las instrucciones que siguen `Then`, `ElseIf`, o `Else`, la ejecución continúa con la instrucción que sigue `End If`.  
  
 El `ElseIf` y `Else` cláusulas son opcionales. Puede tener tantos `ElseIf` cláusulas como desean en un `If`... `Then`... `Else` instrucción, pero no `ElseIf` puede aparecer una cláusula después de un `Else` cláusula. `If`... `Then`... `Else` instrucciones pueden anidarse dentro de otros.  
  
 En la sintaxis de varias líneas, el `If` instrucción debe ser la única instrucción en la primera línea. El `ElseIf`, `Else`, y `End If` instrucciones pueden ir precedidas solamente por una etiqueta de línea. El `If`... `Then`... `Else` bloque debe terminar con un `End If` instrucción.  
  
> [!TIP]
>  El [seleccione... Instrucción de caso](../../../visual-basic/language-reference/statements/select-case-statement.md) podría ser más útil al evaluar una expresión única que tiene varios valores posibles.  
  
### <a name="single-line-syntax"></a>Sintaxis de línea  
 Puede usar la sintaxis de línea para una única condición con el código que se ejecutarán si es true. Sin embargo, la sintaxis de varias líneas proporciona más estructura y la flexibilidad y es más fácil de leer, mantener y depurar.  
  
 A continuación se la `Then` palabra clave se examina para determinar si la instrucción es una sola línea `If`. Si algo distinto de un comentario aparece después `Then` en la misma línea, la instrucción se trata como una sola línea `If` instrucción. Si `Then` no está presente, debe ser el inicio de varias líneas `If`... `Then`... `Else`.  
  
 En la sintaxis de línea única, puede tener varias instrucciones ejecutadas como resultado de un `If`... `Then` decisión. Todas las instrucciones deben estar en la misma línea y estar separadas por signos de dos puntos.  

## <a name="multiline-syntax-example"></a>Ejemplo de sintaxis de varias líneas

<a name="multi-line"></a>
 
 El ejemplo siguiente muestra el uso de la sintaxis de varias líneas de la `If`... `Then`... `Else` instrucción.  
  
 [!code-vb[VbVbalrStatements#101](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class6.vb#101)]

## <a name="nested-syntax-example"></a>Ejemplo de sintaxis anidados

<a name="nested"></a>

 El ejemplo siguiente contiene anidada `If`... `Then`... `Else` instrucciones.  
  
 [!code-vb[VbVbalrStatements#102](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class6.vb#102)]

## <a name="single-line-syntax-example"></a>Ejemplo de sintaxis de línea
  
<a name="single-line"></a> El ejemplo siguiente muestra el uso de la sintaxis de línea.  
  
 [!code-vb[VbVbalrStatements#103](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class6.vb#103)]
  
## <a name="see-also"></a>Vea también

- <xref:Microsoft.VisualBasic.Interaction.Choose%2A>
- <xref:Microsoft.VisualBasic.Interaction.Switch%2A>
- [#If...Then...#Else (directivas)](../../../visual-basic/language-reference/directives/if-then-else-directives.md)
- [Select...Case (instrucción)](../../../visual-basic/language-reference/statements/select-case-statement.md)
- [Estructuras de control anidadas](../../../visual-basic/programming-guide/language-features/control-flow/nested-control-structures.md)
- [Estructuras de decisión](../../../visual-basic/programming-guide/language-features/control-flow/decision-structures.md)
- [Operadores lógicos y bit a bit en Visual Basic](../../../visual-basic/programming-guide/language-features/operators-and-expressions/logical-and-bitwise-operators.md)
- [If (operador)](../../../visual-basic/language-reference/operators/if-operator.md)
