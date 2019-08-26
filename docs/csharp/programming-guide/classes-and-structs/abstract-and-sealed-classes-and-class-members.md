---
title: 'Clases y miembros de clase abstractos y sellados: Guía de programación de C#'
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- abstract classes [C#]
- sealed classes [C#]
- C# language, abstract classes
- C# language, sealed
ms.assetid: 99aa52f7-b435-43f9-936e-2470af734c4e
ms.openlocfilehash: 1c98e2979ee96d4bcc885b8cc797eaac28c8d2ed
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/19/2019
ms.locfileid: "69597294"
---
# <a name="abstract-and-sealed-classes-and-class-members-c-programming-guide"></a>Clases y miembros de clase abstractos y sellados (Guía de programación de C#)
La palabra clave [abstract](../../language-reference/keywords/abstract.md) permite crear clases y miembros [class](../../language-reference/keywords/class.md) que están incompletos y se deben implementar en una clase derivada.  
  
 La palabra clave [sealed](../../language-reference/keywords/sealed.md) permite impedir la herencia de una clase o de ciertos miembros de clase marcados previamente como [virtual](../../language-reference/keywords/virtual.md).  
  
## <a name="abstract-classes-and-class-members"></a>Clases y miembros de clase abstractos  
 Las clases se pueden declarar como abstractas si se incluye la palabra clave `abstract` antes de la definición de clase. Por ejemplo:  
  
 [!code-csharp[csProgGuideInheritance#13](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#13)]  
  
 No se pueden crear instancias de una clase abstracta. El propósito de una clase abstracta es proporcionar una definición común de una clase base que múltiples clases derivadas pueden compartir. Por ejemplo, una biblioteca de clases puede definir una clase abstracta que se utiliza como parámetro para muchas de sus funciones y solicitar a los programadores que utilizan esa biblioteca que proporcionen su propia implementación de la clase mediante la creación de una clase derivada.  
  
 Las clases abstractas también pueden definir métodos abstractos. Esto se consigue agregando la palabra clave `abstract` antes del tipo de valor que devuelve el método. Por ejemplo:  
  
 [!code-csharp[csProgGuideInheritance#14](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#14)]  
  
 Los métodos abstractos no tienen ninguna implementación, de modo que la definición de método va seguida por un punto y coma en lugar de un bloque de método normal. Las clases derivadas de la clase abstracta deben implementar todos los métodos abstractos. Cuando una clase abstracta hereda un método virtual de una clase base, la clase abstracta puede reemplazar el método virtual con un método abstracto. Por ejemplo:  
  
 [!code-csharp[csProgGuideInheritance#15](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#15)]  
  
 Si un método `virtual` se declara como `abstract`, sigue siendo virtual para cualquier clase que herede de la clase abstracta. Una clase que hereda un método abstracto no puede tener acceso a la implementación original del método: en el ejemplo anterior, `DoWork` en la clase F no puede llamar a `DoWork` en la clase D. De esta manera, una clase abstracta puede exigir a las clases derivadas que proporcionen nuevas implementaciones de método para los métodos virtuales.  
  
## <a name="sealed-classes-and-class-members"></a>Clases y miembros de clase sellados  
 Las clases se pueden declarar como [selladas](../../language-reference/keywords/sealed.md) si se incluye la palabra clave `sealed` antes de la definición de clase. Por ejemplo:  
  
 [!code-csharp[csProgGuideInheritance#16](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#16)]  
  
 Una clase sellada no se puede utilizar como clase base. Por esta razón, tampoco puede ser una clase abstracta. Las clases selladas evitan la derivación. Puesto que nunca se pueden utilizar como clase base, algunas optimizaciones en tiempo de ejecución pueden hacer que sea un poco más rápido llamar a miembros de clase sellada.  
  
 Un método, indizador, propiedad o evento de una clase derivada que reemplaza a un miembro virtual de la clase base puede declarar ese miembro como sellado. Esto niega el aspecto virtual del miembro para cualquier clase derivada adicional. Esto se logra colocando la palabra clave `sealed` antes de la palabra clave [override](../../language-reference/keywords/override.md) en la declaración del miembro de clase. Por ejemplo:  
  
 [!code-csharp[csProgGuideInheritance#17](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#17)]  
  
## <a name="see-also"></a>Vea también

- [Guía de programación de C#](../index.md)
- [Clases y structs](./index.md)
- [Herencia](./inheritance.md)
- [Métodos](./methods.md)
- [Campos](./fields.md)
- [Cómo: Definir las propiedades abstractas](./how-to-define-abstract-properties.md)
