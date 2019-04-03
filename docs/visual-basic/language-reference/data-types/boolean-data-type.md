---
title: Boolean (Tipo de datos, Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.FALSE
- vb.TRUE
- vb.Boolean
helpviewer_keywords:
- Boolean data type
- Boolean values [Visual Basic], False keyword
- False keyword [Visual Basic]
- True keyword [Visual Basic]
- Boolean values [Visual Basic], True keyword
ms.assetid: 4858e630-4813-4216-a55e-f4d0feb884e4
ms.openlocfilehash: 7b64302d801a08f976de0ec969983c821f7a8471
ms.sourcegitcommit: bce0586f0cccaae6d6cbd625d5a7b824d1d3de4b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/02/2019
ms.locfileid: "58841229"
---
# <a name="boolean-data-type-visual-basic"></a>Boolean (Tipo de datos, Visual Basic)
Contiene valores que solo pueden ser `True` o `False`. Las palabras clave `True` y `False` corresponden a los dos Estados de `Boolean` variables.  
  
## <a name="remarks"></a>Comentarios  
 Use la [(Visual Basic) de tipo de datos Boolean](../../../visual-basic/language-reference/data-types/boolean-data-type.md) para contener valores de dos estados como verdadero/falso, sí/no o activado/desactivado.  
  
 El valor predeterminado de `Boolean` es `False`.  
  
 `Boolean` los valores no se almacenan como números y los valores almacenados no pretende ser equivalente a números. Nunca debería escribir código que se basa en valores numéricos equivalentes para `True` y `False`. Siempre que sea posible, debe restringir el uso de `Boolean` variables a los valores lógicos para que se han diseñado.  
  
## <a name="type-conversions"></a>Conversiones de tipos  
 Cuando Visual Basic convierte los valores de tipo de datos numéricos para `Boolean`, se convierte en 0 `False` y todos los demás valores se convierten en `True`. Cuando Visual Basic convierte `Boolean` valores a tipos numéricos, `False` se convierte en 0 y `True` se convierte en -1.  
  
 Al convertir entre `Boolean` valores y tipos de datos numéricos, tenga en cuenta que los métodos de conversión de .NET Framework no siempre producen los mismos resultados que las palabras clave de conversión de Visual Basic. Esto es porque la conversión de Visual Basic conserva un comportamiento compatible con versiones anteriores. Para obtener más información, vea "Booleano tipo Does no convertir al tipo numérico correctamente" en [solución de problemas de los tipos de datos](../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md).  
  
## <a name="programming-tips"></a>Sugerencias de programación  
  
-   **Números negativos.** `Boolean` no es un tipo numérico y no puede representar un valor negativo. En cualquier caso, no debe utilizar `Boolean` para contener valores numéricos.  
  
-   **Caracteres de tipo.** `Boolean` no tiene ningún carácter de tipo literal o un carácter de tipo identificador.  
  
-   **Tipo de marco de trabajo.** El tipo correspondiente en .NET Framework es la estructura <xref:System.Boolean?displayProperty=nameWithType>.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente, `runningVB` es un `Boolean` variable, que almacena un sí/no.  
  
```  
Dim runningVB As Boolean  
' Check to see if program is running on Visual Basic engine.  
If scriptEngine = "VB" Then  
    runningVB = True  
End If  
```  
  
## <a name="see-also"></a>Vea también

- <xref:System.Boolean?displayProperty=nameWithType>
- [Tipos de datos](../../../visual-basic/language-reference/data-types/index.md)
- [Funciones de conversión de tipos](../../../visual-basic/language-reference/functions/type-conversion-functions.md)
- [Resumen de conversión](../../../visual-basic/language-reference/keywords/conversion-summary.md)
- [Uso eficiente de tipos de datos](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)
- [Solución de problemas de tipos de datos](../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)
- [Función CType](../../../visual-basic/language-reference/functions/ctype-function.md)
