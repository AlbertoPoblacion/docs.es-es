---
title: Parallel LINQ (PLINQ)
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- PLINQ, overview
ms.assetid: 3d4d0cd3-bde4-490b-99e7-f4e41be96455
ms.openlocfilehash: 1ea880c6403a5fc8b26ba67fe21dfce79c4683db
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/30/2019
ms.locfileid: "73140039"
---
# <a name="parallel-linq-plinq"></a>Parallel LINQ (PLINQ)
Parallel LINQ (PLINQ) es una implementación en paralelo de LINQ to Objects. PLINQ implementa el conjunto completo de operadores de consulta estándar de LINQ como métodos de extensión para el espacio de nombres <xref:System.Linq> y tiene operadores adicionales para las operaciones en paralelo. PLINQ combina la simplicidad y legibilidad de la sintaxis de LINQ con la eficacia de la programación en paralelo. Al igual que el código que tiene como destino la biblioteca TPL, PLINQ consulta la escala en el grado de simultaneidad según las funcionalidades del equipo host.  
  
 En muchos escenarios, PLINQ puede aumentar considerablemente la velocidad de las consultas de LINQ to Objects usando de manera más eficiente todos los núcleos disponibles en el equipo host. Este mayor rendimiento aporta capacidad de procesamiento de alto rendimiento al escritorio.  
  
## <a name="in-this-section"></a>En esta sección  
 [Introducción a PLINQ](../../../docs/standard/parallel-programming/introduction-to-plinq.md)  
  
 [Introducción a la velocidad en PLINQ](../../../docs/standard/parallel-programming/understanding-speedup-in-plinq.md)  
  
 [Conversación del orden en PLINQ](../../../docs/standard/parallel-programming/order-preservation-in-plinq.md)  
  
 [Opciones de combinación en PLINQ](../../../docs/standard/parallel-programming/merge-options-in-plinq.md)  
  
 [Cómo: Crear y ejecutar una consulta PLINQ simple](../../../docs/standard/parallel-programming/how-to-create-and-execute-a-simple-plinq-query.md)  
  
 [Cómo: Controlar la ordenación en una consulta PLINQ](../../../docs/standard/parallel-programming/how-to-control-ordering-in-a-plinq-query.md)  
  
 [Cómo: Combinar consultas LINQ paralelas y secuenciales](../../../docs/standard/parallel-programming/how-to-combine-parallel-and-sequential-linq-queries.md)  
  
 [Cómo: Controlar excepciones en una consulta PLINQ](../../../docs/standard/parallel-programming/how-to-handle-exceptions-in-a-plinq-query.md)  
  
 [Cómo: Cancelar una consulta PLINQ](../../../docs/standard/parallel-programming/how-to-cancel-a-plinq-query.md)  
  
 [Cómo: Escribir una función de agregado personalizada de PLINQ](../../../docs/standard/parallel-programming/how-to-write-a-custom-plinq-aggregate-function.md)  
  
 [Cómo: Especificar el modo de ejecución en PLINQ](../../../docs/standard/parallel-programming/how-to-specify-the-execution-mode-in-plinq.md)  
  
 [Cómo: Especificar opciones de fusión mediante combinación en PLINQ](../../../docs/standard/parallel-programming/how-to-specify-merge-options-in-plinq.md)  
  
 [Cómo: Recorrer en iteración directorios con PLINQ](../../../docs/standard/parallel-programming/how-to-iterate-file-directories-with-plinq.md)  
  
 [Cómo: Medir el rendimiento de consultas PLINQ](../../../docs/standard/parallel-programming/how-to-measure-plinq-query-performance.md)  
  
 [Ejemplo de datos de PLINQ](../../../docs/standard/parallel-programming/plinq-data-sample.md)  
  
## <a name="see-also"></a>Vea también

- <xref:System.Linq.ParallelEnumerable>
- [Programación en paralelo](../../../docs/standard/parallel-programming/index.md)
- [Language Integrated Query (LINQ) (C#)](../../csharp/programming-guide/concepts/linq/index.md)  
- [Language Integrated Query (LINQ) (Visual Basic)](../../visual-basic/programming-guide/concepts/linq/index.md)  
