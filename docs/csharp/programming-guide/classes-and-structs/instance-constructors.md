---
title: 'Constructores de instancias: Guía de programación de C#'
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- constructors [C#], instance constructors
- instance constructors [C#]
ms.assetid: 24663779-c1e5-4af4-a942-ca554e4c542d
ms.openlocfilehash: 5cc7c06a763c4b274b154afc581e495a7e2aa09b
ms.sourcegitcommit: bdd930b5df20a45c29483d905526a2a3e4d17c5b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/11/2018
ms.locfileid: "53241660"
---
# <a name="instance-constructors-c-programming-guide"></a>Constructores de instancias (Guía de programación de C#)
Los constructores de instancias se usan para crear e inicializar las variables miembro de instancia cuando se usa la expresión [new](../../../csharp/language-reference/keywords/new.md) para crear un objeto de una [clase](../../../csharp/language-reference/keywords/class.md). Para inicializar una clase [estática](../../../csharp/language-reference/keywords/static.md), o variables estáticas en una clase no estática, se debe definir un constructor estático. Para obtener más información, vea [Static Constructors](../../../csharp/programming-guide/classes-and-structs/static-constructors.md) (Constructores estáticos [Guía de programación de C#]).  
  
 En el siguiente ejemplo se muestra un constructor de instancias:  
  
 [!code-csharp[csProgGuideObjects#5](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/instance-constructors_1.cs)]  
  
> [!NOTE]
>  Para mayor claridad, esta clase contiene campos públicos. El uso de campos públicos no es una práctica de programación recomendada porque permite que cualquier método de cualquier parte de un programa obtenga acceso sin restricciones ni comprobaciones a los mecanismos internos de un objeto. Los miembros de datos generalmente deberían ser privados y solo se debería tener acceso a ellos a través de las propiedades y métodos de la clase.  
  
 Se llama a este constructor de instancias cada vez que se crea un objeto basado en la clase `CoOrds`. Un constructor como este, que no toma ningún argumento, se denomina *constructor predeterminado*. Pero a menudo resulta útil proporcionar constructores adicionales. Por ejemplo, se puede agregar un constructor a la clase `CoOrds` que permita especificar los valores iniciales de los miembros de datos:  
  
 [!code-csharp[csProgGuideObjects#76](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/instance-constructors_2.cs)]  
  
 Esto permite crear objetos `CoOrd` con valores iniciales predeterminados o específicos, como este:  
  
 [!code-csharp[csProgGuideObjects#77](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/instance-constructors_3.cs)]  
  
 Si una clase no tiene un constructor, se genera automáticamente un constructor predeterminado y los valores predeterminados se usan para inicializar los campos del objeto. Por ejemplo, un [int](../../../csharp/language-reference/keywords/int.md) se inicializa en 0. Para más información sobre los valores predeterminados, vea [Tabla de valores predeterminados (Referencia de C#)](../../../csharp/language-reference/keywords/default-values-table.md). Por tanto, dado que el constructor predeterminado de la clase `CoOrds` inicializa todos los miembros de datos en cero, se puede quitar por completo sin cambiar el funcionamiento de la clase. Más adelante en este tema se proporciona un ejemplo completo del uso de varios constructores en el Ejemplo 1 y en el Ejemplo 2 se proporciona un ejemplo de un constructor generado automáticamente.  
  
 Los constructores de instancias también se pueden usar para llamar a los constructores de instancias de las clases base. El constructor de clase puede invocar el constructor de la clase base a través del inicializador, como sigue:  
  
 [!code-csharp[csProgGuideObjects#78](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/instance-constructors_4.cs)]  
  
 En este ejemplo, la clase `Circle` pasa valores que representan el radio y el alto al constructor proporcionado por `Shape` desde el que se deriva `Circle`. Un ejemplo completo del uso de `Shape` y `Circle` aparece en este tema en el Ejemplo 3.  
  
## <a name="example-1"></a>Ejemplo 1  
 En el ejemplo siguiente se muestra una clase con dos constructores de clase, uno sin argumentos y uno con dos argumentos.  
  
 [!code-csharp[csProgGuideObjects#4](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/instance-constructors_5.cs)]  
  
## <a name="example-2"></a>Ejemplo 2  
 En este ejemplo, la clase `Person` no tiene ningún constructor, en cuyo caso, se proporciona automáticamente un constructor predeterminado y los campos se inicializan en sus valores predeterminados.  
  
 [!code-csharp[csProgGuideObjects#8](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/instance-constructors_6.cs)]  
  
 Observe que el valor predeterminado de `age` es `0` y el valor predeterminado de `name` es `null`. Para más información sobre los valores predeterminados, vea [Tabla de valores predeterminados (Referencia de C#)](../../../csharp/language-reference/keywords/default-values-table.md).  
  
## <a name="example-3"></a>Ejemplo 3  
 En el ejemplo siguiente se muestra cómo usar el inicializador de la clase base. La clase `Circle` se deriva de la clase general `Shape` y la clase `Cylinder` se deriva de la clase `Circle`. En cada clase derivada, el constructor usa su inicializador de clase base.  
  
 [!code-csharp[csProgGuideObjects#9](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/instance-constructors_7.cs)]  
  
 Para obtener más ejemplos sobre cómo invocar los constructores de clase base, vea [virtual](../../../csharp/language-reference/keywords/virtual.md), [override](../../../csharp/language-reference/keywords/override.md) y [base](../../../csharp/language-reference/keywords/base.md).  
  
## <a name="see-also"></a>Vea también

- [Guía de programación de C#](../../../csharp/programming-guide/index.md)  
- [Clases y structs](../../../csharp/programming-guide/classes-and-structs/index.md)  
- [Constructores](../../../csharp/programming-guide/classes-and-structs/constructors.md)  
- [Finalizadores](../../../csharp/programming-guide/classes-and-structs/destructors.md)  
- [static](../../../csharp/language-reference/keywords/static.md)
