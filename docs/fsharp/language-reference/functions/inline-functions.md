---
title: Funciones insertadas
description: Aprenda a usar F# funciones insertadas que se integran directamente en el código de llamada.
ms.date: 05/16/2016
ms.openlocfilehash: d1c3fb3d2721024febc95b3c5e01e06cd547f81e
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/15/2019
ms.locfileid: "65642070"
---
# <a name="inline-functions"></a>Funciones insertadas

*Las funciones insertadas* son funciones que se integran directamente en el código de llamada.

## <a name="using-inline-functions"></a>Uso de funciones Inline

Al usar parámetros de tipo estático, todas las funciones que están parametrizadas según los parámetros de tipo deben ser en línea. Esto garantiza que el compilador puede resolver estos parámetros de tipo. Cuando se usan parámetros de tipo genérico normal, no hay ninguna restricción.

Además de habilitar el uso de restricciones de miembro, funciones insertadas pueden ser útil para optimizar el código. Sin embargo, uso excesivo de las funciones insertadas puede provocar que el código sea menos resistente a los cambios en las optimizaciones del compilador y la implementación de funciones de biblioteca. Por este motivo, debe evitar el uso de funciones insertadas para la optimización, a menos que haya intentado todas las otras técnicas de optimización. Realizar una función o método en línea a veces puede mejorar el rendimiento, pero no es siempre el caso. Por lo tanto, también debe usar las medidas de rendimiento para comprobar que la que hace el código de una función realmente tiene un efecto positivo.

El `inline` modificador se puede aplicar a las funciones en el nivel superior, en el nivel de módulo o en el nivel de método en una clase.

El ejemplo de código siguiente muestra una función inline en el nivel superior, un método de instancia en línea y un método estático en línea.

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-3/snippet201.fs)]

## <a name="inline-functions-and-type-inference"></a>Las funciones insertadas e inferencia de tipo

La presencia de `inline` afecta a la inferencia de tipo. Esto es porque las funciones insertadas pueden resueltos estáticamente los parámetros de tipo, mientras que las funciones no insertadas no. El ejemplo de código siguiente muestra un caso donde `inline` es útil porque, utilizas una función que tiene un parámetro de tipo resueltos estáticamente el `float` operador de conversión.

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-3/snippet202.fs)]

Sin el `inline` fuerza la inferencia de tipo modificador, la función que tome un tipo específico, en este caso `int`. Pero con la `inline` modificador, la función también se infiere para tener un parámetro de tipo resueltos estáticamente. Con el `inline` modificador, el tipo se infiere para ser lo siguiente:

```fsharp
^a -> unit when ^a : (static member op_Explicit : ^a -> float)
```

Esto significa que la función acepta cualquier tipo que admita una conversión a **float**.

## <a name="see-also"></a>Vea también

- [Funciones](index.md)
- [Restricciones](../generics/constraints.md)
- [Parámetros de tipo resueltos estáticamente](../generics/statically-resolved-type-parameters.md)
