---
title: 'Clases y estructuras: Guía de programación de C#'
ms.custom: seodec18
description: Describe el uso de clases y estructuras (struct) en C#.
ms.date: 01/17/2016
helpviewer_keywords:
- structs [C#], about structs
- classes [C#], overview
- C# language, structs
- C# language, objects
- objects [C#]
- C# language, classes
ms.assetid: cc39dbda-8754-423e-b5b1-16a1db0734c0
ms.openlocfilehash: 7b85940f8ce64139d056497a8007379f1658010d
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61646337"
---
# <a name="classes-and-structs-c-programming-guide"></a>Clases y estructuras (Guía de programación de C#)
Las clases (class) y estructuras (struct) son dos de las construcciones básicas de Common Type System en .NET Framework. Cada una de ellas es básicamente una estructura de datos que encapsula un conjunto de datos y comportamientos que forman un conjunto como una unidad lógica. Los datos y comportamientos son los *miembros* de la clase o estructura, e incluyen sus métodos, propiedades y eventos, entre otros elementos, como se muestra más adelante en este tema.  
  
 Una declaración de clase o estructura es como un plano que se utiliza para crear instancias u objetos en tiempo de ejecución. Si define una clase o estructura llamada `Person`, `Person` es el nombre del tipo. Si declara e inicializa una variable `p` de tipo `Person`, se dice que `p` es un objeto o instancia de `Person`. Se pueden crear varias instancias del mismo tipo `Person`, y cada instancia tiene diferentes valores en sus propiedades y campos.  
  
 Una clase es un tipo de referencia. Cuando se crea un objeto de la clase, la variable a la que se asigna el objeto contiene solo una referencia a esa memoria. Cuando la referencia de objeto se asigna a una nueva variable, la nueva variable hace referencia al objeto original. Los cambios realizados en una variable se reflejan en la otra variable porque ambas hacen referencia a los mismos datos.  
  
 Una estructura es un tipo de valor. Cuando se crea una estructura, la variable a la que se asigna la estructura contiene los datos reales de ella. Cuando la estructura se asigna a una nueva variable, se copia. Por lo tanto, la nueva variable y la variable original contienen dos copias independientes de los mismos datos. Los cambios realizados en una copia no afectan a la otra copia.  
  
 En general, las clases se utilizan para modelar comportamientos más complejos, o datos que se prevén modificar después de haber creado un objeto de clase. Las estructuras son más adecuadas para las estructuras de datos pequeñas que contienen principalmente datos que no se prevén modificar después de haber creado la estructura.  
  
 Para más información, vea [Clases](../../../csharp/programming-guide/classes-and-structs/classes.md), [Objectos](../../../csharp/programming-guide/classes-and-structs/objects.md) y [Estructuras](../../../csharp/programming-guide/classes-and-structs/structs.md).  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente, `CustomClass` en el espacio de nombres `ProgrammingGuide` tiene tres miembros: un constructor de instancia, una propiedad denominada `Number` y un método denominado `Multiply`. El método `Main` de la clase `Program` crea una instancia (objeto) de `CustomClass`, y se puede acceder a la propiedad y al método del objeto mediante una notación de puntos.
  
 [!code-csharp[csProgGuideObjects#1](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/class1.cs#1)]  
  
## <a name="encapsulation"></a>Encapsulación  
 A veces se hace referencia a la *encapsulación* como el primer pilar o principio de la programación orientada a objetos. Según el principio de encapsulación, una clase o una estructura pueden especificar hasta qué punto se puede acceder a sus miembros para codificar fuera de la clase o la estructura. No se prevé el uso de los métodos y las variables fuera de la clase, o el ensamblado puede ocultarse para limitar el potencial de los errores de codificación o de los ataques malintencionados.  
  
 Para más información sobre las clases, vea [Clases](../../../csharp/programming-guide/classes-and-structs/classes.md) y [Objetos](../../../csharp/programming-guide/classes-and-structs/objects.md).  
  
### <a name="members"></a>Miembros  
 Todos los métodos, campos, constantes, propiedades y eventos deben declararse dentro de un tipo; se les denomina *miembros* del tipo. En C#, no hay métodos ni variables globales como en otros lenguajes. Incluso un punto de entrada del programa, el método `Main`, debe declararse dentro de una clase o estructura. La lista siguiente incluye los diversos tipos de miembros que se pueden declarar en una clase o estructura.  
  
-   [Campos](../../../csharp/programming-guide/classes-and-structs/fields.md)  
  
-   [Constantes](../../../csharp/programming-guide/classes-and-structs/constants.md)  
  
-   [Propiedades](../../../csharp/programming-guide/classes-and-structs/properties.md)  
  
-   [Métodos](../../../csharp/programming-guide/classes-and-structs/methods.md)  
  
-   [Constructores](../../../csharp/programming-guide/classes-and-structs/constructors.md)  
  
-   [Eventos](../../../csharp/programming-guide/events/index.md)  
  
-   [Finalizadores](../../../csharp/programming-guide/classes-and-structs/destructors.md)  
  
-   [Indizadores](../../../csharp/programming-guide/indexers/index.md)  
  
-   [Operadores](../../../csharp/programming-guide/statements-expressions-operators/operators.md)  
  
-   [Tipos anidados](../../../csharp/programming-guide/classes-and-structs/nested-types.md)  
  
### <a name="accessibility"></a>Accesibilidad  
 Algunos métodos y propiedades están diseñados para ser invocables y accesibles desde el código fuera de la clase o la estructura, lo que se conoce como *código de cliente*. Otros métodos y propiedades pueden estar indicados exclusivamente para utilizarse en la propia clase o estructura. Es importante limitar la accesibilidad del código, a fin de que solo el código de cliente previsto pueda acceder a él. Puede usar los modificadores de acceso [public](../../../csharp/language-reference/keywords/public.md), [protected](../../../csharp/language-reference/keywords/protected.md), [internal](../../../csharp/language-reference/keywords/internal.md), [protected internal](../../../csharp/language-reference/keywords/protected-internal.md), [private](../../../csharp/language-reference/keywords/private.md) y [private protected](../../../csharp/language-reference/keywords/private-protected.md) para especificar hasta qué punto los tipos y sus miembros son accesibles para el código de cliente. La accesibilidad predeterminada es `private`. Para obtener más información, consulte [Modificadores de acceso](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md).  
  
### <a name="inheritance"></a>Herencia  
 Las clases (pero no las estructuras) admiten el concepto de herencia. Una clase que deriva de otra clase (la *clase base*) contiene automáticamente todos los miembros públicos, protegidos e internos de la clase base, salvo sus constructores y finalizadores. Para más información, vea [Herencia](../../../csharp/programming-guide/classes-and-structs/inheritance.md) y [Polimorfismo](../../../csharp/programming-guide/classes-and-structs/polymorphism.md).  
  
 Las clases pueden declararse como [abstract](../../../csharp/language-reference/keywords/abstract.md), lo que significa que uno o varios de sus métodos no tienen ninguna implementación. Aunque no se pueden crear instancias de clases abstractas directamente, pueden servir como clases base para otras clases que proporcionan la implementación que falta. Las clases también pueden declararse como [sealed](../../../csharp/language-reference/keywords/sealed.md) para evitar que otras clases hereden de ellas. Para más información, vea [Clases y miembros de clase abstractos y sellados](../../../csharp/programming-guide/classes-and-structs/abstract-and-sealed-classes-and-class-members.md).  
  
### <a name="interfaces"></a>Interfaces  
 Las clases y las estructuras pueden heredar varias interfaces. Heredar de una interfaz significa que el tipo implementa todos los métodos definidos en la interfaz. Para más información, vea [Interfaces](../../../csharp/programming-guide/interfaces/index.md).  
  
### <a name="generic-types"></a>Tipos genéricos  
 Las clases y estructuras pueden definirse con uno o varios parámetros de tipo. El código de cliente proporciona el tipo cuando crea una instancia del tipo. Por ejemplo, la clase <xref:System.Collections.Generic.List%601> del espacio de nombres <xref:System.Collections.Generic> se define con un parámetro de tipo. El código de cliente crea una instancia de `List<string>` o `List<int>` para especificar el tipo que contendrá la lista. Para más información, vea [Genéricos](../../../csharp/programming-guide/generics/index.md).  
  
### <a name="static-types"></a>Tipos estáticos  
 Las clases (pero no las estructuras) pueden declararse como [static](../../../csharp/language-reference/keywords/static.md). Una clase estática puede contener solo miembros estáticos y no se puede crear una instancia de ellos con la palabra clave new. Una copia de la clase se carga en memoria cuando se carga el programa, y sus miembros son accesibles a través del nombre de clase. Las clases y estructuras pueden contener miembros estáticos. Para más información, vea [Clases estáticas y sus miembros](../../../csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members.md).  
  
### <a name="nested-types"></a>Tipos anidados  
 Una clase o estructura se puede anidar dentro de otra clase o estructura. Para obtener más información, consulte [Tipos anidados](../../../csharp/programming-guide/classes-and-structs/nested-types.md).  
  
### <a name="partial-types"></a>Tipos parciales  
 Puede definir parte de una clase, estructura o método en un archivo de código y otra parte en un archivo de código independiente. Para más información, vea [Clases y métodos parciales](../../../csharp/programming-guide/classes-and-structs/partial-classes-and-methods.md).  
  
### <a name="object-initializers"></a>Inicializadores de objeto  
 Puede crear instancias de objetos de clase o estructura y de colecciones de objetos e iniciarlizarlos, sin llamar de forma explícita a su constructor. Para más información, vea [Inicializadores de objeto y de colección](../../../csharp/programming-guide/classes-and-structs/object-and-collection-initializers.md).  
  
### <a name="anonymous-types"></a>Tipos anónimos  
 En situaciones donde no es conveniente o necesario crear una clase con nombre, por ejemplo al rellenar una lista con estructuras de datos que no tiene que conservar o pasar a otro método, utilice los tipos anónimos. Para más información, vea [Tipos anónimos](../../../csharp/programming-guide/classes-and-structs/anonymous-types.md).  
  
### <a name="extension-methods"></a>Métodos de extensión.  
 Puede "extender" una clase sin crear una clase derivada mediante la creación de un tipo independiente cuyos métodos pueden llamarse como si pertenecieran al tipo original. Para más información, vea [Métodos de extensión](../../../csharp/programming-guide/classes-and-structs/extension-methods.md).  
  
### <a name="implicitly-typed-local-variables"></a>Variables locales con asignación implícita de tipos  
 Dentro de un método de clase o estructura, puede utilizar tipos implícitos para indicar al compilador que determine el tipo correcto en tiempo de compilación. Para más información, vea [Variables locales con asignación implícita de tipos](../../../csharp/programming-guide/classes-and-structs/implicitly-typed-local-variables.md).  
  
## <a name="c-language-specification"></a>Especificación del lenguaje C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>Vea también

- [Guía de programación de C#](../../../csharp/programming-guide/index.md)
