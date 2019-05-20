---
title: 'Cláusula where: Referencia de C#'
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- whereclause_CSharpKeyword
helpviewer_keywords:
- where keyword [C#]
- where clause [C#]
ms.assetid: 7f9bf952-7744-4f91-b676-cddb55d107c3
ms.openlocfilehash: fc259f0e0a83d2f55bf2d50fa336c9201b8b5bef
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/15/2019
ms.locfileid: "65633224"
---
# <a name="where-clause-c-reference"></a>where (Cláusula, Referencia de C#)

La cláusula `where` se usa en una expresión de consulta para especificar los elementos del origen de datos que se devuelven en dicha expresión. Aplica una condición booleana (*predicate*) a cada elemento de origen (al que hace referencia la variable de rango) y devuelve aquellos en los que la condición especificada se cumple. Puede que una sola expresión de consulta contenga varias cláusulas `where` y que una sola cláusula contenga varias subexpresiones de predicado.

## <a name="example"></a>Ejemplo

En el ejemplo siguiente, la cláusula `where` filtra todos los números excepto los que son inferiores a cinco. Si la cláusula `where` se quita, se devolverán todos los números del origen de datos. La expresión `num < 5` es el predicado que se aplica a cada elemento.

[!code-csharp[cscsrefQueryKeywords#5](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsCsrefQueryKeywords/CS/Where.cs#5)]

## <a name="example"></a>Ejemplo

En una sola cláusula `where`, se pueden especificar todos los predicados que sean necesarios mediante los operadores [&&](../operators/boolean-logical-operators.md#conditional-logical-and-operator-) y [&#124;&#124;](../operators/boolean-logical-operators.md#conditional-logical-or-operator-). En el ejemplo siguiente, la consulta especifica dos predicados para seleccionar únicamente los números pares que sean inferiores a cinco.

[!code-csharp[cscsrefQueryKeywords#6](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsCsrefQueryKeywords/CS/Where.cs#6)]  

## <a name="example"></a>Ejemplo

Puede que una cláusula `where` contenga uno o más métodos que devuelvan valores booleanos. En el ejemplo siguiente, la cláusula `where` usa un método para determinar si el valor actual de la variable de rango es par o impar.

[!code-csharp[cscsrefQueryKeywords#7](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsCsrefQueryKeywords/CS/Where.cs#7)]

## <a name="remarks"></a>Comentarios

La cláusula `where` es un mecanismo de filtrado. Se puede colocar prácticamente en cualquier parte en una expresión de consulta, pero no puede ser la primera ni la última cláusula. Puede que una cláusula `where` aparezca antes o después de una cláusula [group](group-clause.md), en función de que haya que filtrar los elementos de origen antes o después de agruparlos.

Si un predicado especificado no es válido para los elementos del origen de datos, se producirá un error en tiempo de compilación. Esta es una de las ventajas de la comprobación estricta de tipos que [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] ofrece.

En tiempo de compilación, la palabra clave `where` se convierte en una llamada al método de operador de consulta estándar <xref:System.Linq.Enumerable.Where%2A>.

## <a name="see-also"></a>Vea también

- [Palabras clave para consultas (LINQ)](query-keywords.md)
- [from (cláusula)](from-clause.md)
- [select (cláusula)](select-clause.md)
- [Filtrado de datos](../../programming-guide/concepts/linq/filtering-data.md)
- [Expresiones de consulta LINQ](../../../csharp/programming-guide/linq-query-expressions/index.md)
- [Introducción a LINQ en C#](../../programming-guide/concepts/linq/getting-started-with-linq.md)
