---
title: Seleccionar una clase de colección
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- last-in-first-out collections
- first-in-first-out collections
- collections [.NET Framework], selecting collection class
- indexed collections
- Collections classes
- grouping data in collections, selecting collection class
ms.assetid: ba049f9a-ce87-4cc4-b319-3f75c8ddac8a
author: mairaw
ms.author: mairaw
ms.openlocfilehash: fd40e35c001318f7e5e685a68fd591b253cbf051
ms.sourcegitcommit: bd28ff1e312eaba9718c4f7ea272c2d4781a7cac
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/26/2019
ms.locfileid: "56836375"
---
# <a name="selecting-a-collection-class"></a>Seleccionar una clase de colección
Asegúrese de elegir con cuidado la clase de colección. Usar un tipo incorrecto puede restringir el uso de la colección. En general, evite usar los tipos del espacio de nombres <xref:System.Collections> a menos que su objetivo sea específicamente la versión 1.1 de .NET Framework. Se preferirán las versiones genéricas y simultáneas de las colecciones por la mayor seguridad de los tipos y otras mejoras.  
  
 Pregúntese lo siguiente:  
  
-   ¿Necesita una lista secuencial en la que normalmente se descarta el elemento después de recuperar su valor?  
  
    -   En caso afirmativo, considere usar la clase <xref:System.Collections.Queue> o la clase genérica <xref:System.Collections.Generic.Queue%601> si necesita un comportamiento de tipo primero en entrar, primero en salir (FIFO). Considere usar la clase <xref:System.Collections.Stack> o la clase genérica <xref:System.Collections.Generic.Stack%601> si necesita un comportamiento de tipo último en entrar, primero en salir (LIFO). Para obtener acceso seguro desde varios subprocesos, use las versiones simultáneas <xref:System.Collections.Concurrent.ConcurrentQueue%601> y <xref:System.Collections.Concurrent.ConcurrentStack%601>.  
  
    -   En caso contrario, considere usar las demás colecciones.  
  
-   ¿Necesita acceder a los elementos en cierto orden, como FIFO, LIFO o aleatorio?  
  
    -   La clase <xref:System.Collections.Queue> y las clases genéricas <xref:System.Collections.Generic.Queue%601> o <xref:System.Collections.Concurrent.ConcurrentQueue%601> ofrecen acceso FIFO. Para obtener más información, consulte [Cuándo usar una colección segura para subprocesos](../../../docs/standard/collections/thread-safe/when-to-use-a-thread-safe-collection.md).  
  
    -   La clase <xref:System.Collections.Stack> y las clases genéricas <xref:System.Collections.Generic.Stack%601> o <xref:System.Collections.Concurrent.ConcurrentStack%601> ofrecen acceso LIFO. Para obtener más información, consulte [Cuándo usar una colección segura para subprocesos](../../../docs/standard/collections/thread-safe/when-to-use-a-thread-safe-collection.md).  
  
    -   La clase genérica <xref:System.Collections.Generic.LinkedList%601> permite el acceso secuencial desde el encabezado hasta el final o desde el final hasta el encabezado.  
  
-   ¿Necesita acceder a cada elemento por índice?  
  
    -   Las clases <xref:System.Collections.ArrayList> y <xref:System.Collections.Specialized.StringCollection> y la clase genérica <xref:System.Collections.Generic.List%601> ofrecen acceso a sus elementos por el índice de base cero del elemento.  
  
    -   Las clases <xref:System.Collections.Hashtable>, <xref:System.Collections.SortedList>, <xref:System.Collections.Specialized.ListDictionary> y <xref:System.Collections.Specialized.StringDictionary>, y las clases genéricas <xref:System.Collections.Generic.Dictionary%602> y <xref:System.Collections.Generic.SortedDictionary%602> ofrecen acceso a sus elementos por la clave del elemento.  
  
    -   Las clases <xref:System.Collections.Specialized.NameObjectCollectionBase> y <xref:System.Collections.Specialized.NameValueCollection>, y las clases genéricas <xref:System.Collections.ObjectModel.KeyedCollection%602> y <xref:System.Collections.Generic.SortedList%602> ofrecen acceso a sus elementos por el índice de base cero o por la clave del elemento.  
  
-   ¿Cada elemento contendrá un valor, una combinación de una clave y un valor, o una combinación de una clave y varios valores?  
  
    -   Un valor: use cualquiera de las colecciones basadas en la interfaz <xref:System.Collections.IList> o en la interfaz genérica <xref:System.Collections.Generic.IList%601>.  
  
    -   Una clave y un valor: use cualquiera de las colecciones basadas en la interfaz <xref:System.Collections.IDictionary> o en la interfaz genérica <xref:System.Collections.Generic.IDictionary%602>.  
  
    -   Un valor con clave insertada: use la clase genérica <xref:System.Collections.ObjectModel.KeyedCollection%602>.  
  
    -   Una clave y varios valores: use la clase <xref:System.Collections.Specialized.NameValueCollection>.  
  
-   ¿Necesita ordenar los elementos de manera diferente a como se especificaron?  
  
    -   La clase <xref:System.Collections.Hashtable> ordena los elementos por sus códigos hash.  
  
    -   La clase <xref:System.Collections.SortedList> y las clases genéricas <xref:System.Collections.Generic.SortedDictionary%602> y <xref:System.Collections.Generic.SortedList%602> ordenan sus elementos por la clave, en función de las implementaciones de la interfaz <xref:System.Collections.IComparer> y de la interfaz genérica <xref:System.Collections.Generic.IComparer%601>.  
  
    -   <xref:System.Collections.ArrayList> proporciona un método <xref:System.Collections.ArrayList.Sort%2A> que toma una implementación de <xref:System.Collections.IComparer> como parámetro. Su homóloga genérica, la clase genérica <xref:System.Collections.Generic.List%601>, proporciona un método <xref:System.Collections.Generic.List%601.Sort%2A> que toma una implementación de la interfaz genérica <xref:System.Collections.Generic.IComparer%601> como parámetro.  
  
-   ¿Necesita realizar búsquedas y recuperaciones rápidas de información?  
  
    -   <xref:System.Collections.Specialized.ListDictionary> es más rápida que <xref:System.Collections.Hashtable> para colecciones pequeñas (de 10 elementos o menos). La clase genérica <xref:System.Collections.Generic.Dictionary%602> proporciona búsquedas más rápidas que la clase genérica <xref:System.Collections.Generic.SortedDictionary%602>. La implementación multiproceso es <xref:System.Collections.Concurrent.ConcurrentDictionary%602>. <xref:System.Collections.Concurrent.ConcurrentBag%601> proporciona una inserción multiproceso rápida para datos no ordenados. Para más información sobre ambos tipos multiproceso, consulte [Cuándo usar una colección segura para subprocesos](../../../docs/standard/collections/thread-safe/when-to-use-a-thread-safe-collection.md).  
  
-   ¿Necesita colecciones que acepten solo cadenas?  
  
    -   <xref:System.Collections.Specialized.StringCollection> (basada en <xref:System.Collections.IList>) y <xref:System.Collections.Specialized.StringDictionary> (basada en <xref:System.Collections.IDictionary>) están en el espacio de nombres <xref:System.Collections.Specialized>.  
  
    -   Además, puede usar cualquiera de las clases de colección genéricas del espacio de nombres <xref:System.Collections.Generic> como colecciones de cadenas fuertemente tipadas especificando la clase <xref:System.String> para sus argumentos de tipo genéricos.  
  
## <a name="linq-to-objects-and-plinq"></a>LINQ to Objects y PLINQ  
 LINQ to Objects permite usar consultas LINQ para acceder a los objetos en memoria siempre que el tipo de objeto implemente las interfaces <xref:System.Collections.IEnumerable> o <xref:System.Collections.Generic.IEnumerable%601>. Las consultas LINQ proporcionan un modelo común para acceder a los datos; suelen ser más concisas y legibles que los bucles `foreach` estándar y proporcionan funciones de filtrado, ordenación y agrupación. Para obtener más información, vea [LINQ to Objects (C#)](../../csharp/programming-guide/concepts/linq/linq-to-objects.md) y [LINQ to Objects (Visual Basic)](../../visual-basic/programming-guide/concepts/linq/linq-to-objects.md).  
  
 PLINQ proporciona una implementación paralela de LINQ to Objects que puede ofrecer una ejecución de consultas más rápida en muchos escenarios gracias a un uso más eficaz de los equipos de varios núcleos. Para más información, consulte [Parallel LINQ (PLINQ)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md).  
  
## <a name="see-also"></a>Vea también

- <xref:System.Collections>
- <xref:System.Collections.Specialized>
- <xref:System.Collections.Generic>
- [Colecciones seguras para subprocesos](../../../docs/standard/collections/thread-safe/index.md)
