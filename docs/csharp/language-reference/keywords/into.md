---
title: 'into: Referencia de C#'
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- into_CSharpKeyword
- into
helpviewer_keywords:
- into keyword [C#]
ms.assetid: 81ec62c1-f0b1-4755-8a31-959876e77f65
ms.openlocfilehash: dc1e2ee004c21bb3d05155eec3e42ea80bf641a1
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/19/2019
ms.locfileid: "69608641"
---
# <a name="into-c-reference"></a>into (Referencia de C#)

La palabra clave contextual `into` puede usarse para crear un identificador temporal para almacenar los resultados de una cláusula [group](group-clause.md), [join](join-clause.md) o [select](select-clause.md) en un nuevo identificador. Este identificador puede ser un generador de comandos de consulta adicionales. Cuando se usa en una cláusula `group` o `select`, el uso del nuevo identificador se denomina a veces una *continuación*.

## <a name="example"></a>Ejemplo

En el ejemplo siguiente, se muestra el uso de la palabra clave `into` para habilitar un identificador temporal `fruitGroup` que tiene un tipo deducido de `IGrouping`. Mediante el identificador, puede invocar el método <xref:System.Linq.Enumerable.Count%2A> en cada grupo y seleccionar solo los grupos que contienen dos o más palabras.

[!code-csharp[cscsrefQueryKeywords#18](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsCsrefQueryKeywords/CS/Into.cs#18)]

El uso de `into` en una cláusula `group` solo es necesario cuando quiere realizar operaciones de consulta adicionales en cada grupo. Para obtener más información, vea [group (Cláusula)](group-clause.md).

Para obtener un ejemplo del uso de `into` en una cláusula `join`, vea [join (Cláusula)](join-clause.md).

## <a name="see-also"></a>Vea también

- [Palabras clave para consultas (LINQ)](query-keywords.md)
- [Expresiones de consulta LINQ](../../programming-guide/linq-query-expressions/index.md)
- [group (cláusula)](group-clause.md)
