---
title: using (Instrucción, Referencia de C#)
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- using statement [C#]
ms.assetid: afc355e6-f0b9-4240-94dd-0d93f17d9fc3
ms.openlocfilehash: e1a1a960fa69be593ea01cab51be576b0055fd5e
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/15/2019
ms.locfileid: "65632898"
---
# <a name="using-statement-c-reference"></a>using (Instrucción, Referencia de C#)

Ofrece una sintaxis adecuada que garantiza el uso correcto de objetos <xref:System.IDisposable>.

## <a name="example"></a>Ejemplo

En el ejemplo siguiente se muestra cómo usar la instrucción `using`.

[!code-csharp[csrefKeywordsNamespace#4](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsNamespace/CS/csrefKeywordsNamespace.cs#4)]

## <a name="remarks"></a>Comentarios

<xref:System.IO.File> y <xref:System.Drawing.Font> son ejemplos de tipos administrados que acceden a recursos no administrados (en este caso, identificadores de archivo y contextos de dispositivo). Hay muchos otros tipos de recursos no administrados y tipos de la biblioteca de clases que los encapsulan. Todos estos tipos deben implementar la interfaz <xref:System.IDisposable>.

Cuando la duración de un objeto `IDisposable` se limita a un único método, debe declarar y crear instancias del mismo en la instrucción `using`. La instrucción `using` llama al método <xref:System.IDisposable.Dispose%2A> del objeto de forma correcta y (cuando se usa tal y como se muestra anteriormente) también hace que el propio objeto salga del ámbito en cuanto se llame a <xref:System.IDisposable.Dispose%2A>. Dentro del bloque `using`, el objeto es de solo lectura y no se puede modificar ni reasignar.

La instrucción `using` asegura que se llama al método <xref:System.IDisposable.Dispose%2A> incluso cuando se produzca una excepción en el bloque `using`. Puede lograr el mismo resultado colocando el objeto dentro de un bloque `try` y llamando luego a <xref:System.IDisposable.Dispose%2A> en un bloque `finally`; de hecho, es así cómo el compilador traduce la instrucción `using`. El ejemplo de código anterior se extiende al siguiente código en tiempo de compilación (tenga en cuenta las llaves adicionales para crear el ámbito limitado del objeto):

[!code-csharp[csrefKeywordsNamespace#5](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsNamespace/CS/csrefKeywordsNamespace.cs#5)]

Vea el tema [try-finally](try-finally.md) para obtener más información sobre la instrucción `try`-`finally`.

Se pueden declarar varias instancias de un tipo en la instrucción `using`, tal y como se muestra en el ejemplo siguiente:

[!code-csharp[csrefKeywordsNamespace#6](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsNamespace/CS/csrefKeywordsNamespace.cs#6)]

Puede crear una instancia del objeto de recurso y luego pasar la variable a la instrucción `using`, pero esto no es un procedimiento recomendado. En este caso, después de que el control abandone el bloque `using` el objeto permanece en el ámbito, pero probablemente ya no tenga acceso a sus recursos no administrados. En otras palabras, ya no se inicializa totalmente. Si intenta usar el objeto fuera del bloque `using`, corre el riesgo de iniciar una excepción. Por este motivo, suele ser mejor crear una instancia del objeto en la instrucción `using` y limitar su ámbito al bloque `using`.

[!code-csharp[csrefKeywordsNamespace#7](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsNamespace/CS/csrefKeywordsNamespace.cs#7)]

Para obtener más información sobre cómo eliminar objetos `IDisposable`, vea [Uso de objetos que implementan IDisposable](../../../standard/garbage-collection/using-objects.md).

## <a name="c-language-specification"></a>Especificación del lenguaje C#

Para obtener más información, vea el apartado [Instrucción using](~/_csharplang/spec/statements.md#the-using-statement) en la [Especificación del lenguaje C#](../language-specification/index.md). La especificación del lenguaje es la fuente definitiva de la sintaxis y el uso de C#.

## <a name="see-also"></a>Vea también

- [Referencia de C#](../index.md)
- [Guía de programación de C#](../../programming-guide/index.md)
- [Palabras clave de C#](index.md)
- [using (directiva)](using-directive.md)
- [Recolección de elementos no utilizados](../../../standard/garbage-collection/index.md)
- [Uso de objetos que implementan IDisposable](../../../standard/garbage-collection/using-objects.md)
- [IDisposable interface](xref:System.IDisposable) (Interfaz IDisposable)
