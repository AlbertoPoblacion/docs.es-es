---
title: Elegir entre clases y structs
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- class library design guidelines [.NET Framework], structures
- class library design guidelines [.NET Framework], classes
- structures [.NET Framework], vs. classes
- classes [.NET Framework], design guidelines
- type design guidelines, structures
- structures [.NET Framework], design guidelines
- classes [.NET Framework], vs. structures
- type design guidelines, classes
ms.assetid: f8b8ec9b-0ba7-4dea-aadf-a93395cd804f
author: KrzysztofCwalina
ms.openlocfilehash: 5041368ca1a440698c399c935ac72aba2002c3ba
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2019
ms.locfileid: "64615268"
---
# <a name="choosing-between-class-and-struct"></a>Elegir entre clases y structs
Una de las decisiones de diseño básicos que se enfrenta a cada diseñador framework es si va a diseñar un tipo como una clase (un tipo de referencia) o como un struct (un tipo de valor). Buen conocimiento de las diferencias en el comportamiento de los tipos de referencia y tipos de valor es fundamental para tomar esta decisión.  
  
 La primera diferencia entre los tipos de referencia y tipos de valor que se tendrá en cuenta es que los tipos de referencia son asignados en el montón y se recolectan, mientras que se asignan los tipos de valor en la pila o en línea en que contiene los tipos y se desasigna cuando la pila desenreda o cuando se desasigna su tipo contenedor. Por lo tanto, las asignaciones y desasignaciones de tipos de valor son en general, más barato que las asignaciones y desasignaciones de tipos de referencia.  
  
 A continuación, matrices de referencia son tipos asignan fuera de línea, lo que significa que la matriz de elementos son las referencias a las instancias del tipo de referencia que se encuentran en el montón. Matrices de tipos de valor se asignan en línea, lo que significa que los elementos de matriz son las instancias reales del tipo de valor. Por lo tanto, las asignaciones y desasignaciones de matrices de tipos de valor son mucho más baratos que las asignaciones y desasignaciones de matrices de tipos de referencia. Además, en la mayoría de los casos las matrices de tipo de valor presentan mucho mejor localidad de referencia.  
  
 La diferencia siguiente está relacionada con el uso de memoria. Tipos de valor obtengan conversión boxing cuando se convierte a un tipo de referencia o una de las interfaces que implementan. Obtienen conversión unboxing cuando se convierte al tipo de valor. Dado que los cuadros son objetos que se asignan en el montón y están recolección, demasiado conversión boxing y unboxing puede tener un impacto negativo en el montón, el recolector de elementos no utilizados y, en última instancia, el rendimiento de la aplicación.  Por el contrario, se produce ninguna conversión boxing tal como se convierten tipos de referencia. (Para obtener más información, consulte [conversión Boxing y Unboxing](../../csharp/programming-guide/types/boxing-and-unboxing.md)).
  
 A continuación, las asignaciones de tipo de referencia copia la referencia, mientras que las asignaciones de tipo de valor copian el valor completo. Por lo tanto, las asignaciones de tipos de referencia de gran tamaño son menos costosas que las asignaciones de tipos de valor grande.  
  
 Por último, los tipos de referencia se pasan por referencia, mientras que los tipos de valor se pasan por valor. Cambios en una instancia de un tipo de referencia afectan a todas las referencias que apunta a la instancia. Cuando se pasan por valor, se copian las instancias del tipo de valor. Cuando se cambia una instancia de un tipo de valor, por supuesto no afecta cualquiera de sus copias. Dado que las copias no se crean explícitamente por el usuario, pero se crean implícitamente cuando se pasan argumentos o se devuelven los valores se devuelven, que se pueden cambiar los tipos de valor pueden ser confusos para muchos usuarios. Por lo tanto, los tipos de valor deben ser inmutables.  
  
 Como regla general, la mayoría de los tipos en un marco de trabajo debe ser clases. Sin embargo, hay algunas situaciones en que las características de un tipo de valor que sea más adecuado usar structs.  
  
 **✓ CONSIDER** definir una estructura en lugar de una clase si instancias del tipo son pequeñas y normalmente corta duración o suelen estar incrustadas en otros objetos.  
  
 **X AVOID** definir un struct a menos que el tipo tenga todas las características siguientes:  
  
- Representa un valor único, similar a los tipos primitivos lógicamente (`int`, `double`, etcetera.).  
  
- Tiene un tamaño de instancia inferior a 16 bytes.  
  
- Es inmutable.  
  
- No tendrá que realizar la conversión boxing con frecuencia.  
  
 En todos los demás casos, debe definir los tipos como clases.  
  
 *Portions © 2005, 2009 Microsoft Corporation. Reservados todos los derechos.*  
  
 *Reimpreso con permiso de Pearson Education, Inc. de [instrucciones de diseño de Framework: Convenciones, expresiones y patrones para bibliotecas reutilizables. NET, 2ª edición](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina y Brad Abrams, publicada el 22 de octubre de 2008 por Addison-Wesley Professional como parte de la serie de desarrollo de Microsoft Windows.*  
  
## <a name="see-also"></a>Vea también

- [Instrucciones de diseño de tipos](../../../docs/standard/design-guidelines/type.md)
- [Instrucciones de diseño de .NET Framework](../../../docs/standard/design-guidelines/index.md)
