---
title: Tipos de datos constantes y literales (Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- declaring constants [Visual Basic], literal data types
- data types [Visual Basic], declaring
- constants [Visual Basic], declaring
- explicit declarations
- literals [Visual Basic], coercing data type
- declarations [Visual Basic], data types
ms.assetid: 057206d2-3a5b-40b9-b3af-57446f9b52fa
ms.openlocfilehash: 50e36aa13439bafcca27a7153a8c5d6043f03975
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61906976"
---
# <a name="constant-and-literal-data-types-visual-basic"></a>Tipos de datos constantes y literales (Visual Basic)
Un literal es un valor que se expresa por sí misma, en lugar de como valor de una variable o el resultado de una expresión, como el número 3 o la cadena "Hello". Una constante es un nombre descriptivo que ocupa el lugar de un literal y conserva este mismo valor en todo el programa, en lugar de una variable, cuyo valor puede cambiar.  
  
 Cuando [Option Infer](../../../../visual-basic/language-reference/statements/option-infer-statement.md) es `Off` y [Option Strict](../../../../visual-basic/language-reference/statements/option-strict-statement.md) es `On`, debe declarar explícitamente todas las constantes con un tipo de datos. En el ejemplo siguiente, el tipo de datos de `MyByte` se declara explícitamente como tipo de datos `Byte`:  
  
 [!code-vb[VbVbalrConstants#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrConstants/VB/Class1.vb#1)]  
  
 Cuando `Option Infer` es `On` o `Option Strict` es `Off`, puede declarar una constante sin especificar un tipo de datos con un `As` cláusula. El compilador determina el tipo de la constante del tipo de la expresión. Un literal de entero numérico se convierte de forma predeterminada para el `Integer` tipo de datos. Tipo de datos predeterminado para números de punto flotante es `Double`y las palabras clave `True` y `False` especificar un `Boolean` constante.  
  
## <a name="literals-and-type-coercion"></a>Literales y conversión de tipos  
 En algunos casos, es posible que desee forzar que un literal a un tipo de datos determinado; Por ejemplo, al asignar un valor literal integral especialmente grande a una variable de tipo `Decimal`. En el ejemplo siguiente, se produce un error:  
  
```  
Dim myDecimal as Decimal  
myDecimal = 100000000000000000000   ' This causes a compiler error.  
```  
  
 Los resultados de error de la representación del literal. El `Decimal` tipo de datos puede contener un valor de este tamaño, pero el literal implícitamente se representa como un `Long`, cuáles no.  
  
 Se puede convertir un literal a un tipo de datos determinado de dos maneras: mediante la anexión de un carácter de tipo a él o colocando entre caracteres de inclusión. Un carácter de tipo o caracteres de cierre deben preceder inmediatamente o siga del literal, sin ningún espacio intermedio o cualquier tipo de carácter.  
  
 Para que funcione el ejemplo anterior, puede anexar el `D` escribir carácter en el literal, lo que hace que se puede representar como un `Decimal`:  
  
 [!code-vb[VbVbalrConstants#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrConstants/VB/Class1.vb#2)]  
  
 El ejemplo siguiente muestra el uso correcto de caracteres de tipo y de inclusión:  
  
 [!code-vb[VbVbalrConstants#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrConstants/VB/Class1.vb#3)]  
  
 La siguiente tabla muestra los caracteres de inclusión y caracteres de tipo disponibles en Visual Basic.  
  
|Tipo de datos|Carácter de inclusión|Carácter de tipo anexado|  
|---|---|---|  
|`Boolean`|(ninguno)|(ninguno)|  
|`Byte`|(ninguno)|(ninguno)|  
|`Char`|"|C|  
|`Date`|#|(ninguno)|  
|`Decimal`|(ninguno)|D. o @|  
|`Double`|(ninguno)|R o #|  
|`Integer`|(ninguno)|O %|  
|`Long`|(ninguno)|L o &|  
|`Short`|(ninguno)|S|  
|`Single`|(ninguno)|F o!|  
|`String`|"|(ninguno)|  
  
## <a name="see-also"></a>Vea también

- [Constantes definidas por el usuario](../../../../visual-basic/programming-guide/language-features/constants-enums/user-defined-constants.md)
- [Cómo: Declarar una constante](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-declare-a-constant.md)
- [Información general sobre las constantes](../../../../visual-basic/programming-guide/language-features/constants-enums/constants-overview.md)
- [Option Strict (instrucción)](../../../../visual-basic/language-reference/statements/option-strict-statement.md)
- [Option Explicit (instrucción)](../../../../visual-basic/language-reference/statements/option-explicit-statement.md)
- [Información general sobre las enumeraciones](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-overview.md)
- [Cómo: Declarar una enumeración](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-declare-enumerations.md)
- [Enumeraciones y calificación de nombres](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-and-name-qualification.md)
- [Tipos de datos](../../../../visual-basic/language-reference/data-types/index.md)
- [Constantes y enumeraciones](../../../../visual-basic/language-reference/constants-and-enumerations.md)
