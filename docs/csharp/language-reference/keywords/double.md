---
title: 'Palabra clave double: Referencia de C#'
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- double
- double_CSharpKeyword
helpviewer_keywords:
- double data type [C#]
ms.assetid: 0980e11b-6004-4102-abcf-cfc280fc6991
ms.openlocfilehash: f4d6bb4eb698e4afbda6571ba382e828a5f836a4
ms.sourcegitcommit: 9b1ac36b6c80176fd4e20eb5bfcbd9d56c3264cf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/28/2019
ms.locfileid: "67424261"
---
# <a name="double-c-reference"></a>double (Referencia de C#)

La palabra clave `double` indica un tipo simple que almacena valores de punto flotante de 64 bits. En la tabla siguiente se muestran la precisión y el intervalo aproximado para el tipo `double`.

|Tipo|Intervalo aproximado|Precisión|Tipo de .NET|
|----------|-----------------------|---------------|-------------------------|
|`double`|De ±5,0 × 10<sup>−324</sup> a ±1,7 × 10<sup>308</sup>|De 15 a 17 dígitos aproximadamente|<xref:System.Double?displayProperty=nameWithType>|

## <a name="literals"></a>Literales

De forma predeterminada, un literal numérico real a la derecha del operador de asignación se trata como `double`. Pero si quiere que un número entero se trate como `double`, use el sufijo d o D, por ejemplo:

```csharp
double x = 3D;
```

## <a name="conversions"></a>Conversiones

Puede combinar tipos numéricos enteros y tipos de punto flotante en una expresión. En este caso, los tipos enteros se convierten a tipos de punto flotante. La evaluación de la expresión se realiza según las reglas siguientes:

- Si uno de los tipos de punto flotante es `double`, la expresión se evalúa como `double` o [bool](../../../csharp/language-reference/keywords/bool.md) en comparaciones relacionales y de igualdad.

- Si no hay ningún tipo `double` en la expresión, se evalúa como [float](../../../csharp/language-reference/keywords/float.md) o [bool](../../../csharp/language-reference/keywords/bool.md) en comparaciones relacionales y de igualdad.

 Una expresión de punto flotante puede contener los siguientes conjuntos de valores:

- Cero positivo y negativo.

- Infinito positivo y negativo.

- Valor no numérico (NaN).

- El conjunto finito de valores distintos de cero.

Para obtener más información sobre estos valores, vea el estándar IEEE para aritmética binaria de punto flotante, disponible en el sitio web de [IEEE](https://www.ieee.org).

## <a name="example"></a>Ejemplo

En el ejemplo siguiente, se agregan [int](../builtin-types/integral-numeric-types.md), [short](../../../csharp/language-reference/builtin-types/integral-numeric-types.md), [float](../../../csharp/language-reference/keywords/float.md) y `double`, que dan un resultado `double`.

[!code-csharp[csrefKeywordsTypes#9](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsTypes/CS/keywordsTypes.cs#9)]

## <a name="c-language-specification"></a>Especificación del lenguaje C#

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>Vea también

- [Referencia de C#](../../../csharp/language-reference/index.md)
- [Guía de programación de C#](../../../csharp/programming-guide/index.md)
- [Palabras clave de C#](../../../csharp/language-reference/keywords/index.md)
- [Tabla de valores predeterminados](../../../csharp/language-reference/keywords/default-values-table.md)
- [Tabla de tipos integrados](../../../csharp/language-reference/keywords/built-in-types-table.md)
- [Tabla de tipos de punto flotante](../../../csharp/language-reference/keywords/floating-point-types-table.md)
- [Tabla de conversiones numéricas implícitas](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md)
- [Tabla de conversiones numéricas explícitas](../../../csharp/language-reference/keywords/explicit-numeric-conversions-table.md)
