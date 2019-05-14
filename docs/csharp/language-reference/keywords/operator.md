---
title: 'Palabra clave operator: Referencia de C#'
ms.custom: seodec18
description: Cómo sobrecargar un operador de C# integrado
ms.date: 08/27/2018
f1_keywords:
- operator_CSharpKeyword
- operator
helpviewer_keywords:
- operator keyword [C#]
ms.assetid: 59218cce-e90e-42f6-a6bb-30300981b86a
ms.openlocfilehash: 47ce91c343092ac2f7555c1edf3418527776e131
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2019
ms.locfileid: "64754762"
---
# <a name="operator-c-reference"></a>operator (Referencia de C#)

Use la palabra clave `operator` para sobrecargar un operador integrado o proporcionar una conversión definida por el usuario en una declaración de clase o estructura.

Para sobrecargar un operador en una clase o estructura personalizadas, puede crear una declaración de operador en el tipo correspondiente. La declaración del operador que sobrecarga un operador de C# integrado debe cumplir las reglas siguientes:

- Incluye los modificadores `public` y `static`.
- Incluye `operator X`, donde `X` es el nombre o símbolo del operador que está sobrecargado.
- Los operadores unarios tienen un parámetro y los operadores binarios tienen dos parámetros. En cada caso, por lo menos un parámetro debe ser del mismo tipo que la clase o estructura que declara el operador.

Para obtener información sobre cómo definir operadores de conversión, vea los artículos sobre las palabras clave [explicit](explicit.md) e [implicit](implicit.md).

Para obtener información general sobre los operadores C# que se pueden sobrecargar, vea el artículo [Operadores sobrecargables](../../programming-guide/statements-expressions-operators/overloadable-operators.md).

## <a name="example"></a>Ejemplo

En el ejemplo siguiente se define un tipo `Fraction` que representa números fraccionarios. Sobrecarga los operadores `+` y `*` para realizar multiplicaciones y sumas fraccionarias, y también proporciona un operador de conversión que convierte un tipo `Fraction` en un tipo `double`.

[!code-csharp[csrefKeywordsConversion#6](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsConversion/CS/csrefKeywordsConversion.cs#6)]

## <a name="c-language-specification"></a>Especificación del lenguaje C#

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>Vea también

- [Referencia de C#](../index.md)
- [Guía de programación de C#](../../programming-guide/index.md)
- [Palabras clave de C#](index.md)
- [implicit](implicit.md)
- [explicit](explicit.md)
- [Operadores sobrecargables](../../programming-guide/statements-expressions-operators/overloadable-operators.md)
- [Cómo: Implementar conversiones definidas por el usuario entre structs](../../programming-guide/statements-expressions-operators/how-to-implement-user-defined-conversions-between-structs.md)
