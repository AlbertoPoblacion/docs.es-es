---
title: Uso de objetos que implementan IDisposable
ms.date: 04/07/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Dispose method
- try/finally block
- garbage collection, encapsulating resources
ms.assetid: 81b2cdb5-c91a-4a31-9c83-eadc52da5cf0
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 074b97f29946390170abe3c40d71d2ee2cb214ce
ms.sourcegitcommit: cdf67135a98a5a51913dacddb58e004a3c867802
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/21/2019
ms.locfileid: "69666476"
---
# <a name="using-objects-that-implement-idisposable"></a>Uso de objetos que implementan IDisposable

El recolector de elementos no utilizados de Common Language Runtime reclama la memoria utilizada por los objetos administrados, aunque los tipos que utilizan recursos no administrados implementan la interfaz <xref:System.IDisposable> para permitir que se reclame la memoria asignada a estos recursos no administrados. Cuando termine de usar un objeto que implemente <xref:System.IDisposable>, debe llamar a la implementación <xref:System.IDisposable.Dispose%2A?displayProperty=nameWithType> del objeto. Hay dos maneras de hacerlo:  
  
* Mediante la instrucción `using` de C# o la instrucción `Using` de Visual Basic.  
  
* Mediante la implementación de un bloque `try/finally`.  

## <a name="the-using-statement"></a>La instrucción using

Las instrucciones `using` de C# y `Using` de Visual Basic simplifican el código que se debe escribir para crear y limpiar un objeto. La instrucción `using` obtiene uno o más recursos, ejecuta las instrucciones especificadas y desecha el objeto automáticamente. Pero la instrucción `using` solo resulta útil para los objetos que se usan dentro del ámbito del método en el que se construyen.  
  
En el ejemplo siguiente se utiliza la instrucción `using` para crear y liberar un objeto <xref:System.IO.StreamReader?displayProperty=nameWithType>.  
  
[!code-csharp[Conceptual.Disposable#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.disposable/cs/using1.cs#1)]
[!code-vb[Conceptual.Disposable#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.disposable/vb/using1.vb#1)]  
  
Si bien la clase <xref:System.IO.StreamReader> implementa la interfaz <xref:System.IDisposable>, que indica que utiliza un recurso no administrado, en el ejemplo no se llama al método <xref:System.IO.StreamReader.Dispose%2A?displayProperty=nameWithType> de manera explícita. Cuando el compilador de C# o de Visual Basic encuentra la instrucción `using`, emite un lenguaje intermedio (IL), que equivale al código siguiente que contiene un bloque `try/finally` de manera explícita.  
  
[!code-csharp[Conceptual.Disposable#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.disposable/cs/using3.cs#3)]
[!code-vb[Conceptual.Disposable#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.disposable/vb/using3.vb#3)]  
  
La instrucción `using` de C# también permite adquirir varios recursos en una sola instrucción, lo que internamente equivale a instrucciones `using` anidadas. En el ejemplo siguiente se crean instancias de dos objetos <xref:System.IO.StreamReader> para leer el contenido de dos archivos.  
  
[!code-csharp[Conceptual.Disposable#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.disposable/cs/using4.cs#4)]

## <a name="tryfinally-block"></a>Bloque try/finally

En lugar de ajustar un bloque `try/finally` en una instrucción `using`, puede elegir implementar el bloque `try/finally` directamente. Puede adoptar este estilo como su método de codificación personal, o bien puede hacer esto por una de las razones siguientes:  
  
* Para incluir un bloque `catch` para controlar las excepciones producidas en el bloque `try`. De lo contrario, las excepciones que produzca la instrucción `using` no se controlan, al igual que las excepciones producidas dentro del bloque `using` si no hay ningún bloque `try/catch` presente.  
  
* Para crear instancias de un objeto que implementa <xref:System.IDisposable> cuyo ámbito no es local en el bloque en el que se declara.  
  
El siguiente ejemplo es similar al anterior, a excepción de que se usa un bloque `try/catch/finally` para crear instancias, usar y eliminar un objeto <xref:System.IO.StreamReader>, y para controlar las excepciones que produce el constructor <xref:System.IO.StreamReader> y su método <xref:System.IO.StreamReader.ReadToEnd%2A>. Observe que el código del bloque `finally` comprueba que el objeto que implementa <xref:System.IDisposable> no es `null` antes de llamar al método <xref:System.IDisposable.Dispose%2A>. Si no se realiza este paso, se puede producir una excepción <xref:System.NullReferenceException> en tiempo de ejecución.  
  
[!code-csharp[Conceptual.Disposable#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.disposable/cs/using5.cs#6)]
[!code-vb[Conceptual.Disposable#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.disposable/vb/using5.vb#6)]  
  
Puede seguir este patrón básico si elige implementar o debe implementar un bloque `try/finally`, ya que el lenguaje de programación no admite una instrucción `using` pero sí llamadas directas al método <xref:System.IDisposable.Dispose%2A>. 
  
## <a name="see-also"></a>Vea también

- [Limpieza de recursos no administrados](../../../docs/standard/garbage-collection/unmanaged.md)
- [using (Instrucción) (Referencia de C#)](../../csharp/language-reference/keywords/using-statement.md)
- [Using (Instrucción, Visual Basic)](../../visual-basic/language-reference/statements/using-statement.md)
