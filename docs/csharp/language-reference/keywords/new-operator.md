---
title: 'Operador new: Referencia de C#'
ms.custom: seodec18
ms.date: 03/15/2018
helpviewer_keywords:
- new operator keyword [C#]
ms.assetid: a212b697-a79b-4105-9923-1f7b108036e8
ms.openlocfilehash: 409a5307eaacd2eac865e2882cc7228521260dbe
ms.sourcegitcommit: 10986410e59ff29f2ec55c6759bde3eb4d1a00cb
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/31/2019
ms.locfileid: "66421877"
---
# <a name="new-operator-c-reference"></a>Operador new (Referencia de C#)

Se usa para crear objetos e invocar constructores. Por ejemplo:

```csharp
Class1 obj  = new Class1();
```

También se usa para crear instancias de tipos anónimos:

```csharp
var query = from cust in customers
            select new { Name = cust.Name, Address = cust.PrimaryAddress };
```

El operador `new` también se usa para invocar al constructor sin parámetros para tipos de valor. Por ejemplo:

```csharp
int i = new int();
```

En la instrucción anterior, `i` se ha inicializado en `0`, que es el valor predeterminado para el tipo `int`. La instrucción tiene el mismo efecto que lo siguiente:

```csharp
int i = 0;
```

Para obtener una lista completa de valores predeterminados, vea [Tabla de valores predeterminados](default-values-table.md).

Recuerde que es un error declarar un constructor sin parámetros para un [struct](struct.md), ya que cada tipo de valor tiene implícitamente un constructor sin parámetros público. Es posible declarar constructores parametrizados en un tipo struct para establecer sus valores iniciales, pero esto solo es necesario si se requieren valores distintos de los predeterminados.

Los objetos de tipo de valor, como las estructuras, y los objetos de tipo de referencia, como las clases, se destruyen automáticamente, pero los objetos de tipo de valor se destruyen junto al contexto que los contiene. En el caso de los objetos de tipo de referencia, los destruye el recolector de elementos no utilizados en un momento no especificado después de que se haya quitado la última referencia a ellos. Para los tipos que contienen recursos como identificadores de archivos o conexiones de red, lo recomendable es llevar a cabo una limpieza determinista para asegurarse de que los recursos que contienen se liberan tan pronto como sea posible. Para obtener más información, vea [Instrucción using](using-statement.md).

El operador `new` no se puede sobrecargar.

Si el operador `new` no puede asignar memoria, se produce la excepción <xref:System.OutOfMemoryException>.

## <a name="example"></a>Ejemplo

En el ejemplo siguiente, se crean y se inicializan un objeto `struct` y un objeto de clase mediante el operador `new` y, después, se les asignan valores. Se muestran el valor predeterminado y los valores asignados.

[!code-csharp[csrefKeywordsOperator#7](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsOperator/CS/csrefKeywordsOperators.cs#7)]

Observe en el ejemplo que el valor predeterminado de una cadena es `null`. Por lo tanto, no se muestra.

## <a name="c-language-specification"></a>Especificación del lenguaje C#

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>Vea también

- [Referencia de C#](../../language-reference/index.md)
- [Guía de programación de C#](../../programming-guide/index.md)
- [Palabras clave de C#](index.md)
- [new](new.md)
- [Tipos anónimos](../../programming-guide/classes-and-structs/anonymous-types.md)
