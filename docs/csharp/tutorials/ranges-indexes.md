---
title: Explorar los intervalos de datos con índices y rangos
description: En este tutorial avanzado se explica cómo explorar datos con índices e intervalos para examinar los segmentos de un conjunto de datos secuencial.
ms.date: 04/19/2019
ms.custom: mvc
ms.openlocfilehash: 118d3c9ccad98ec02195c2b5e26a2ca203990adf
ms.sourcegitcommit: 682c64df0322c7bda016f8bfea8954e9b31f1990
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/13/2019
ms.locfileid: "65557183"
---
# <a name="indices-and-ranges"></a>Índices y rangos

Los rangos e índices proporcionan una sintaxis concisa para acceder a elementos únicos o intervalos en una <xref:System.Array>, <xref:System.Span%601> o <xref:System.ReadOnlySpan%601>. Estas características permiten una sintaxis más concisa y clara para acceder a elementos únicos o intervalos de elementos de una secuencia.

En este tutorial aprenderá lo siguiente:

> [!div class="checklist"]
> * Usar la sintaxis para intervalos de una secuencia.
> * Comprender las decisiones de diseño para iniciar y finalizar cada secuencia.
> * Descubrir escenarios para los tipos <xref:System.Index> y <xref:System.Range>.

## <a name="language-support-for-indices-and-ranges"></a>Compatibilidad con idiomas para los índices y los rangos

Esta compatibilidad con idiomas se basa en dos nuevos tipos y dos nuevos operadores.
- <xref:System.Index?displayProperty=nameWithType> representa un índice en una secuencia.
- El operador `^`, que especifica que un índice es relativo al final de una secuencia.
- <xref:System.Range?displayProperty=nameWithType> representa un subrango de una secuencia.
- El operador de rango (`..`), que especifica el inicio y el fin de un intervalo como sus operandos.

Comencemos con las reglas de los índices. Considere un elemento `sequence` de matriz. El índice `0` es igual que `sequence[0]`. El índice `^0` es igual que `sequence[sequence.Length]`. Tenga en cuenta que `sequence[^0]` produce una excepción, al igual que `sequence[sequence.Length]`. Para cualquier número `n`, el índice `^n` es igual que `sequence[sequence.Length - n]`.

```csharp-interactive
string[] words = new string[]
{
                // index from start    index from end
    "The",      // 0                   ^9
    "quick",    // 1                   ^8
    "brown",    // 2                   ^7
    "fox",      // 3                   ^6
    "jumped",   // 4                   ^5
    "over",     // 5                   ^4
    "the",      // 6                   ^3
    "lazy",     // 7                   ^2
    "dog"       // 8                   ^1
};              // 9 (or words.Length) ^0
```

Puede recuperar la última palabra con el índice `^1`. Agregue el código siguiente a la inicialización:

[!code-csharp[LastIndex](~/samples/csharp/tutorials/RangesIndexes/IndicesAndRanges.cs#IndicesAndRanges_LastIndex)]

Un rango especifica el *inicio* y el *final* de un intervalo. Los rangos son excluyentes, lo que significa que el *final* no se incluye en el intervalo. El rango `[0..^0]` representa todo el intervalo, al igual que `[0..sequence.Length]` representa todo el intervalo. 

El siguiente código crea un subrango con las palabras "quick", "brown" y "fox". Va de `words[1]` a `words[3]`. El elemento `words[4]` no se encuentra en el intervalo. Agregue el código siguiente al mismo método. Cópielo y péguelo en la parte inferior de la ventana interactiva.

[!code-csharp[Range](~/samples/csharp/tutorials/RangesIndexes/IndicesAndRanges.cs#IndicesAndRanges_Range)]

El siguiente código crea un subrango con "lazy" y "dog". Incluye `words[^2]` y `words[^1]`. El índice del final `words[^0]` no se incluye. Agregue el código siguiente también:

[!code-csharp[LastRange](~/samples/csharp/tutorials/RangesIndexes/IndicesAndRanges.cs#IndicesAndRanges_LastRange)]

En los ejemplos siguientes se crean rangos con final abierto para el inicio, el final o ambos:

[!code-csharp[PartialRange](~/samples/csharp/tutorials/RangesIndexes/IndicesAndRanges.cs#IndicesAndRanges_PartialRanges)]

También puede declarar rangos o índices como variables. La variable se puede usar luego dentro de los caracteres `[` y `]`:

[!code-csharp[IndexRangeTypes](~/samples/csharp/tutorials/RangesIndexes/IndicesAndRanges.cs#IndicesAndRanges_RangeIndexTypes)]

El ejemplo siguiente muestra muchos de los motivos para esas opciones. Modifique `x`, `y` y `z` para probar diferentes combinaciones. Al experimentar, use valores donde `x` sea menor que `y` y `y` sea menor que `z` para las combinaciones válidas. Agregue el código siguiente a un nuevo método. Pruebe diferentes combinaciones:

[!code-csharp[SemanticsExamples](~/samples/csharp/tutorials/RangesIndexes/IndicesAndRanges.cs#IndicesAndRanges_Semantics)]

## <a name="scenarios-for-indices-and-ranges"></a>Escenarios para los índices y los rangos

A menudo usará rangos e índices cuando desee realizar un poco de análisis en el subrango de una secuencia completa. La nueva sintaxis es más clara al leer exactamente lo que implica el subrango. La función local `MovingAverage` toma un <xref:System.Range> como su argumento. El método enumera solo ese rango al calcular el mínimo, el máximo y la media. Pruebe con el código siguiente en su proyecto:

[!code-csharp[MovingAverages](~/samples/csharp/tutorials/RangesIndexes/IndicesAndRanges.cs#IndicesAndRanges_MovingAverage)]

Puede descargar el código completado del repositorio [dotnet/samples](https://github.com/dotnet/samples/tree/master/csharp/tutorials/RangesIndexes).