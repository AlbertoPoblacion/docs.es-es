---
title: 'Interfaces: Guía de programación de C#'
ms.custom: seodec18
ms.date: 08/21/2018
helpviewer_keywords:
- interfaces [C#]
- C# language, interfaces
ms.assetid: 2feda177-ce11-432d-81b4-d50f5f35fd37
ms.openlocfilehash: 30c44b9f98bcc61d54b8103b6b40d14fd35715f4
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/19/2019
ms.locfileid: "69589185"
---
# <a name="interfaces-c-programming-guide"></a>Interfaces (Guía de programación de C#)

Una interfaz contiene las definiciones de un grupo de funcionalidades relacionadas que una [clase](../../language-reference/keywords/class.md) o una [estructura](../../language-reference/keywords/struct.md) pueden implementar.
  
Mediante las interfaces puede incluir, por ejemplo, un comportamiento de varios orígenes en una clase. Esta capacidad es importante en C# porque el lenguaje no admite la herencia múltiple de clases. Además, debe usar una interfaz si desea simular la herencia de estructuras, porque no pueden heredar de otra estructura o clase.  
  
Defina una interfaz mediante la palabra clave [interface](../../language-reference/keywords/interface.md), como se muestra en el ejemplo siguiente.  
  
 [!code-csharp[csProgGuideInheritance#47](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#47)]  

El nombre de la estructura debe ser un [nombre de identificador](../inside-a-program/identifier-names.md) de C# válido. Por convención, los nombres de interfaz comienzan con una letra `I` mayúscula.

Cualquier clase o estructura que implementa la interfaz <xref:System.IEquatable%601> debe contener una definición para un método <xref:System.IEquatable%601.Equals%2A> que coincida con la firma que la interfaz especifica. Como resultado, puede contar con una clase que implementa `IEquatable<T>` para contener un método `Equals` con el que una instancia de la clase puede determinar si es igual a otra instancia de la misma clase.  
  
La definición de `IEquatable<T>` no proporciona una implementación para `Equals`. La interfaz define solo la firma. De esa manera, una interfaz en C# es similar a una clase abstracta en la que todos los métodos son abstractos. Sin embargo, una clase o estructura puede implementar varias interfaces, pero una clase solo puede heredar una clase única, ya sea abstracta o no.
  
Para obtener más información sobre las clases abstractas, vea [Abstract and Sealed Classes and Class Members](../classes-and-structs/abstract-and-sealed-classes-and-class-members.md) (Clases y miembros de clase abstractos y sellados [Guía de programación de C#]).  
  
Las interfaces pueden contener métodos, propiedades, eventos, indizadores o cualquier combinación de estos cuatro tipos de miembros. Para obtener vínculos a ejemplos, vea [Secciones relacionadas](./index.md#BKMK_RelatedSections). Una interfaz no puede contener constantes, campos, operadores, constructores de instancias, finalizadores ni tipos. Los miembros de interfaz son públicos automáticamente y no pueden incluir modificadores de acceso. Los miembros tampoco pueden ser [estáticos](../../language-reference/keywords/static.md).  
  
Para implementar un miembro de interfaz, el miembro correspondiente de la clase de implementación debe ser público, no estático y tener el mismo nombre y firma que el miembro de interfaz.  
  
Cuando una clase o estructura implementa una interfaz, la clase o estructura debe proporcionar una implementación para todos los miembros que define la interfaz. La propia interfaz no proporciona ninguna funcionalidad que una clase o estructura puedan heredar de la misma la forma en que pueden heredar la funcionalidad de la clase base. Sin embargo, si una clase base implementa una interfaz, cualquier clase que se derive de la clase base hereda esta implementación.  
  
En el siguiente ejemplo se muestra una implementación de la interfaz <xref:System.IEquatable%601>. La clase de implementación `Car` debe proporcionar una implementación del método <xref:System.IEquatable%601.Equals%2A>.  
  
 [!code-csharp[csProgGuideInheritance#48](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#48)]  
  
Las propiedades y los indizadores de una clase pueden definir descriptores de acceso adicionales para una propiedad o indizador que estén definidos en una interfaz. Por ejemplo, una interfaz puede declarar una propiedad que tenga un descriptor de acceso [get](../../language-reference/keywords/get.md). La clase que implementa la interfaz puede declarar la misma propiedad con un descriptor de acceso `get` y [set](../../language-reference/keywords/set.md). Sin embargo, si la propiedad o el indizador usan una implementación explícita, los descriptores de acceso deben coincidir. Para obtener más información sobre la implementación explícita, vea [Implementación de interfaz explícita](explicit-interface-implementation.md) y [Propiedades de interfaces](../classes-and-structs/interface-properties.md).  

Las interfaces pueden heredar de otras interfaces. Una clase puede incluir una interfaz varias veces mediante las clases base que hereda o mediante las interfaces que otras interfaces heredan. Sin embargo, la clase puede proporcionar una implementación de una interfaz solo una vez y solo si la clase declara la interfaz como parte de la definición de la clase (`class ClassName : InterfaceName`). Si la interfaz se hereda porque se heredó una clase base que implementa la interfaz, la clase base proporciona la implementación de los miembros de la interfaz. Sin embargo, la clase derivada puede volver a implementar cualquier miembro de la interfaz virtual, en lugar de usar la implementación heredada.  
  
Una clase base también puede implementar miembros de interfaz mediante el uso de los miembros virtuales. En ese caso, una clase derivada puede cambiar el comportamiento de la interfaz reemplazando los miembros virtuales. Para obtener más información sobre los miembros virtuales, vea [Polimorfismo](../classes-and-structs/polymorphism.md).  
  
## <a name="interfaces-summary"></a>Resumen de interfaces

Una interfaz tiene las propiedades siguientes:  

- Una interfaz es como una clase base abstracta con solo miembros abstractos. Cualquier clase o estructura que implementa la interfaz debe implementar todos sus miembros.
- No se puede crear una instancia de una interfaz directamente. Sus miembros se implementan por medio de cualquier clase o estructura que implementa la interfaz.
- Las interfaces pueden contener eventos, indizadores, métodos y propiedades.
- Las interfaces no contienen ninguna implementación de métodos.
- Una clase o estructura puede implementar varias interfaces. Una clase puede heredar una clase base y también implementar una o varias interfaces.

## <a name="in-this-section"></a>En esta sección

[Implementación de interfaz explícita](explicit-interface-implementation.md)  
 Explica cómo crear un miembro de clase que es específico de una interfaz.  
  
 [Cómo: Implementar explícitamente miembros de interfaz](how-to-explicitly-implement-interface-members.md)  
 Proporciona un ejemplo de cómo implementar explícitamente miembros de interfaces.  
  
 [Cómo: Implementar explícitamente miembros de dos interfaces](how-to-explicitly-implement-members-of-two-interfaces.md)  
 Proporciona un ejemplo de cómo implementar explícitamente miembros de interfaces con herencia.  
  
## <a name="BKMK_RelatedSections"></a> Secciones relacionadas

- [Propiedades de interfaz](../classes-and-structs/interface-properties.md)  
- [Indizadores en Interfaces](../indexers/indexers-in-interfaces.md)  
- [Cómo:  Implementar eventos de interfaz](../events/how-to-implement-interface-events.md)  
- [Clases y structs](../classes-and-structs/index.md)  
- [Herencia](../classes-and-structs/inheritance.md)  
- [Métodos](../classes-and-structs/methods.md)  
- [Polimorfismo](../classes-and-structs/polymorphism.md)  
- [Clases y miembros de clase abstractos y sellados](../classes-and-structs/abstract-and-sealed-classes-and-class-members.md)  
- [Propiedades](../classes-and-structs/properties.md)  
- [Eventos](../events/index.md)  
- [Indizadores](../indexers/index.md)  
  
## <a name="featured-book-chapter"></a>Capítulo destacado del libro

[Interfaces](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/ff652489%28v%3Dorm.10%29) en [Learning C# 3.0: Master the Fundamentals of C# 3.0](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/ff652493%28v%253dorm.10%29)

## <a name="see-also"></a>Vea también

- [Guía de programación de C#](../index.md)
- [Herencia](../classes-and-structs/inheritance.md)
- [Nombres de identificador](../inside-a-program/identifier-names.md)
