---
title: 'Tipos: Guía de programación de C#'
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- value types [C#]
- reference types [C#]
- types [C#]
- C# language, data types
- common type system [C#]
- data types [C#]
- C# language, types
- strong typing [C#]
ms.assetid: f782d7cc-035e-4500-b1b1-36a9881130ad
ms.openlocfilehash: 65a7fbb2ef8fd24e80b4ccf979a7f3fc7cf19934
ms.sourcegitcommit: 9b1ac36b6c80176fd4e20eb5bfcbd9d56c3264cf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/28/2019
ms.locfileid: "67423638"
---
# <a name="types-c-programming-guide"></a>Tipos (Guía de programación de C#)

## <a name="types-variables-and-values"></a>Tipos, variables y valores

C# es un lenguaje fuertemente tipado. Todas las variables y constantes tienen un tipo, al igual que todas las expresiones que se evalúan como un valor. Cada una de las firmas de método especifica un tipo para cada parámetro de entrada y para el valor devuelto. La biblioteca de clases .NET define un conjunto de tipos numéricos integrados, así como tipos más complejos que representan una amplia variedad de construcciones lógicas, como el sistema de archivos, conexiones de red, colecciones y matrices de objetos, y fechas. Los programas de C# típicos usan tipos de la biblioteca de clases, así como tipos definidos por el usuario que modelan los conceptos que son específicos del dominio del problema del programa.

Entre la información almacenada en un tipo se puede incluir lo siguiente:

- El espacio de almacenamiento que requiere una variable del tipo.

- Los valores máximo y mínimo que puede representar.

- Los miembros (métodos, campos, eventos, etc.) que contiene.

- El tipo base del que hereda.

- La ubicación donde se asignará la memoria para variables en tiempo de ejecución.

- Los tipos de operaciones permitidas.

El compilador usa información de tipo para garantizar que todas las operaciones que se realizan en el código cuentan *con seguridad de tipos*. Por ejemplo, si declara una variable de tipo [int](../../../csharp/language-reference/builtin-types/integral-numeric-types.md), el compilador le permite usar la variable en operaciones de suma y resta. Si intenta realizar esas mismas operaciones en una variable de tipo [bool](../../../csharp/language-reference/keywords/bool.md), el compilador genera un error, como se muestra en el siguiente ejemplo:

[!code-csharp[csProgGuideTypes#42](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/Class1.cs#42)]

> [!NOTE]
> Los desarrolladores de C y C++ deben tener en cuenta que, en C#, [bool](../../../csharp/language-reference/keywords/bool.md) no se puede convertir en [int](../../../csharp/language-reference/builtin-types/integral-numeric-types.md).

El compilador inserta la información de tipo en el archivo ejecutable como metadatos. Common Language Runtime (CLR) utiliza esos metadatos en tiempo de ejecución para garantizar aún más la seguridad de tipos cuando asigna y reclama memoria.

### <a name="specifying-types-in-variable-declarations"></a>Definición de tipos en declaraciones de variable

Cuando declare una variable o constante en un programa, debe especificar su tipo o utilizar la palabra clave [var](../../../csharp/language-reference/keywords/var.md) para que el compilador infiera el tipo. En el ejemplo siguiente se muestran algunas declaraciones de variable que utilizan tanto tipos numéricos integrados como tipos complejos definidos por el usuario:

[!code-csharp[csProgGuideTypes#36](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/Class1.cs#36)]

Los tipos de parámetros de método y valores devueltos se especifican en la firma del método. En la siguiente firma se muestra un método que requiere una variable [int](../../../csharp/language-reference/builtin-types/integral-numeric-types.md) como argumento de entrada y devuelve una cadena:

[!code-csharp[csProgGuideTypes#35](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/Class1.cs#35)]

Tras declarar una variable, no se puede volver a declarar con un nuevo tipo y no se le puede asignar un valor que no sea compatible con su tipo declarado. Por ejemplo, no puede declarar un valor [int](../../../csharp/language-reference/builtin-types/integral-numeric-types.md) y, luego, asignarle un valor booleano de [true](../../../csharp/language-reference/keywords/true-literal.md). En cambio, los valores se pueden convertir en otros tipos, por ejemplo, cuando se asignan a variables nuevas o se pasan como argumentos de método. El compilador realiza automáticamente una *conversión de tipo* que no da lugar a una pérdida de datos. Una conversión que pueda dar lugar a la pérdida de datos requiere un valor *cast* en el código fuente.

Para obtener más información, vea [Conversiones de tipos](../../../csharp/programming-guide/types/casting-and-type-conversions.md).

## <a name="built-in-types"></a>Tipos integrados

C# proporciona un conjunto estándar de tipos numéricos integrados para representar números enteros, valores de punto flotante, expresiones booleanas, caracteres de texto, valores decimales y otros tipos de datos. También hay tipos `string` y `object` integrados. Están disponibles para su uso en cualquier programa de C#. Para obtener más información sobre los tipos integrados, vea [Tablas de referencia para tipo integrados](../../../csharp/language-reference/keywords/built-in-types-table.md).

## <a name="custom-types"></a>Tipos personalizados

Las construcciones [struct](../../../csharp/language-reference/keywords/struct.md), [class](../../../csharp/language-reference/keywords/class.md), [interface](../../../csharp/language-reference/keywords/interface.md) y [enum](../../../csharp/language-reference/keywords/enum.md) se utilizan para crear sus propios tipos personalizados. La biblioteca de clases .NET es en sí misma una colección de tipos personalizados proporcionados por Microsoft que puede usar en sus propias aplicaciones. De forma predeterminada, los tipos usados con más frecuencia en la biblioteca de clases están disponibles en cualquier programa de C#. Otros están disponibles solo cuando agrega explícitamente una referencia de proyecto al ensamblado en el que se definen. Una vez que el compilador tenga una referencia al ensamblado, puede declarar variables (y constantes) de los tipos declarados en dicho ensamblado en el código fuente. Para más información, vea [Biblioteca de clases .NET](../../../standard/class-library-overview.md).

## <a name="the-common-type-system"></a>Common Type System

Es importante entender dos aspectos fundamentales sobre el sistema de tipos en .NET:

- Es compatible con el principio de herencia. Los tipos pueden derivarse de otros tipos, denominados *tipos base*. El tipo derivado hereda (con algunas restricciones), los métodos, las propiedades y otros miembros del tipo base. A su vez, el tipo base puede derivarse de algún otro tipo, en cuyo caso el tipo derivado hereda los miembros de ambos tipos base en su jerarquía de herencia. Todos los tipos, incluidos los tipos numéricos integrados como <xref:System.Int32?displayProperty=nameWithType> (palabra clave de C#: [int](../../../csharp/language-reference/builtin-types/integral-numeric-types.md)), derivan en última instancia de un único tipo base, que es <xref:System.Object?displayProperty=nameWithType> (palabra clave de C#: [object](../../../csharp/language-reference/keywords/object.md)). Esta jerarquía de tipos unificada se denomina [Common Type System](../../../standard/base-types/common-type-system.md) (CTS). Para más información sobre la herencia en C#, vea [Herencia](../../../csharp/programming-guide/classes-and-structs/inheritance.md).

- En CTS, cada tipo se define como un *tipo de valor* o un *tipo de referencia*. Esto incluye todos los tipos personalizados de la biblioteca de clases .NET y también sus propios tipos definidos por el usuario. Los tipos que se definen mediante el uso de la palabra clave [struct](../../../csharp/language-reference/keywords/struct.md) son tipos de valor; todos los tipos numéricos integrados son `structs`. Los tipos que se definen mediante el uso de la palabra clave [class](../../../csharp/language-reference/keywords/class.md) son tipos de referencia. Los tipos de referencia y los tipos de valor tienen distintas reglas de tiempo de compilación y distintos comportamientos de tiempo de ejecución.

En la ilustración siguiente se muestra la relación entre los tipos de valor y los tipos de referencia en CTS.

En la imagen siguiente se muestran tipos de valores y tipos de referencias en CTS:

![Captura de pantalla en la que se muestran tipos de valores y tipos de referencias en CTS.](./media/index/value-reference-types-common-type-system.png)

> [!NOTE]
> Puede ver que los tipos utilizados con mayor frecuencia están organizados en el espacio de nombres <xref:System>. Sin embargo, el espacio de nombres que contiene un tipo no tiene ninguna relación con un tipo de valor o un tipo de referencia.

### <a name="value-types"></a>Tipos de valor

Los tipos de valor derivan de <xref:System.ValueType?displayProperty=nameWithType>, el cual deriva de <xref:System.Object?displayProperty=nameWithType>. Los tipos que derivan de <xref:System.ValueType?displayProperty=nameWithType> tienen un comportamiento especial en CLR. Las variables de tipo de valor contienen directamente sus valores, lo que significa que la memoria se asigna insertada en cualquier contexto en el que se declare la variable. No se produce ninguna asignación del montón independiente ni sobrecarga de la recolección de elementos no utilizados para las variables de tipo de valor.

Existen dos categorías de tipos de valor: [struct](../../../csharp/language-reference/keywords/struct.md) y [enum](../../../csharp/language-reference/keywords/enum.md).

Los tipos numéricos integrados son structs y tienen propiedades y métodos a los que se puede obtener acceso:

```csharp
// Static method on type byte.
byte b = byte.MaxValue;
```

Pero se declaran y se les asignan valores como si fueran tipos simples no agregados:

```csharp
byte num = 0xA;
int i = 5;
char c = 'Z';
```

Los tipos de valor están *sellados*, lo que significa que, por ejemplo, no puede derivar un tipo de <xref:System.Int32?displayProperty=nameWithType>, y no puede definir un struct para que herede de cualquier clase o struct definido por el usuario, porque un struct solo puede heredar de <xref:System.ValueType?displayProperty=nameWithType>. A pesar de ello, un struct puede implementar una o más interfaces. Puede convertir un tipo struct en cualquier tipo de interfaz que implemente. Esto hace que una operación de conversión *boxing* encapsule el struct dentro de un objeto de tipo de referencia en el montón administrado. Las operaciones de conversión boxing se producen cuando se pasa un tipo de valor a un método que toma <xref:System.Object?displayProperty=nameWithType> o cualquier tipo de interfaz como parámetro de entrada. Para obtener más información, vea [Conversión boxing y unboxing](../../../csharp/programming-guide/types/boxing-and-unboxing.md).

Puede usar la palabra clave [struct](../../../csharp/language-reference/keywords/struct.md) para crear sus propios tipos de valor personalizados. Normalmente, un struct se usa como un contenedor para un pequeño conjunto de variables relacionadas, como se muestra en el ejemplo siguiente:

[!code-csharp[csProgGuideObjects#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#1)]

Para más información sobre estructuras, vea [Structs](../../../csharp/programming-guide/classes-and-structs/structs.md). Para más información sobre los tipos de valor en. NET, vea [Tipos de valor](../../../csharp/language-reference/keywords/value-types.md).

La otra categoría de tipos de valor es [enum](../../../csharp/language-reference/keywords/enum.md). Una enumeración define un conjunto de constantes integrales con nombre. Por ejemplo, la enumeración <xref:System.IO.FileMode?displayProperty=nameWithType> de la biblioteca de clases .NET contiene un conjunto de enteros constantes con nombre que especifican cómo se debe abrir un archivo. Se define como se muestra en el ejemplo siguiente:

[!code-csharp[csProgGuideTypes#44](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/Class1.cs#44)]

La constante `System.IO.FileMode.Create` tiene un valor de 2. Sin embargo, el nombre es mucho más significativo para los humanos que leen el código fuente y, por esa razón, es mejor utilizar enumeraciones en lugar de números literales constantes. Para más información, consulte <xref:System.IO.FileMode?displayProperty=nameWithType>.

Todas las enumeraciones se heredan de <xref:System.Enum?displayProperty=nameWithType>, el cual se hereda de <xref:System.ValueType?displayProperty=nameWithType>. Todas las reglas que se aplican a las estructuras también se aplican a las enumeraciones. Para más información sobre las enumeraciones, vea [Tipos de enumeración](../../../csharp/programming-guide/enumeration-types.md).

### <a name="reference-types"></a>Tipos de referencia

Un tipo que se define como [clase](../../../csharp/language-reference/keywords/class.md), [delegado](../../../csharp/language-reference/keywords/delegate.md), matriz o [interfaz](../../../csharp/language-reference/keywords/interface.md) es un *tipo de referencia*. Al declarar una variable de un tipo de referencia en tiempo de ejecución, esta contendrá el valor [null](../../../csharp/language-reference/keywords/null.md) hasta que se cree explícitamente un objeto mediante el operador [new](../../../csharp/language-reference/operators/new-operator.md), o bien que se le asigne un objeto creado en otro lugar mediante `new`, tal y como se muestra en el ejemplo siguiente:

```csharp
MyClass mc = new MyClass();
MyClass mc2 = mc;
```

Una interfaz debe inicializarse junto con un objeto de clase que lo implementa. Si `MyClass` implementa `IMyInterface`, cree una instancia de `IMyInterface`, tal como se muestra en el ejemplo siguiente:

```csharp
IMyInterface iface = new MyClass();
```

Cuando se crea el objeto, se asigna la memoria en el montón administrado y la variable solo contiene una referencia a la ubicación del objeto. Los tipos del montón administrado producen sobrecarga cuando se asignan y cuando los reclama la función de administración de memoria automática de CLR, conocida como *recolección de elementos no utilizados*. En cambio, la recolección de elementos no utilizados también está muy optimizada y no crea problemas de rendimiento en la mayoría de los escenarios. Para obtener más información sobre la recolección de elementos no utilizados, vea [Administración de memoria automática](../../../standard/automatic-memory-management.md).

Todas las matrices son tipos de referencia, incluso si sus elementos son tipos de valor. Las matrices derivan de manera implícita de la clase <xref:System.Array?displayProperty=nameWithType>, pero el usuario las declara y las usa con la sintaxis simplificada que proporciona C#, como se muestra en el ejemplo siguiente:

[!code-csharp[csProgGuideTypes#45](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/Class1.cs#45)]

Los tipos de referencia admiten la herencia completamente. Al crear una clase, puede heredar de cualquier otra interfaz o clase que no esté definida como [sealed](../../../csharp/language-reference/keywords/sealed.md); y otras clases pueden heredar de la clase e invalidar sus métodos virtuales. Para más información sobre cómo crear clases propias, vea [Clases y structs](../../../csharp/programming-guide/classes-and-structs/index.md). Para más información sobre la herencia y los métodos virtuales, vea [Herencia](../../../csharp/programming-guide/classes-and-structs/inheritance.md).

## <a name="types-of-literal-values"></a>Tipos de valores literales

En C#, los valores literales reciben un tipo del compilador. Puede especificar cómo debe escribirse un literal numérico; para ello, anexe una letra al final del número. Por ejemplo, para especificar que el valor 4.56 debe tratarse como un valor flotante, anexe "f" o "F" después del número: `4.56f`. Si no se anexa ninguna letra, el compilador inferirá un tipo para el literal. Para obtener más información sobre los tipos que se pueden especificar con sufijos de letras, vea las páginas de referencia de los tipos individuales en [Tipos de valor](../../../csharp/language-reference/keywords/value-types.md).

Dado que los literales tienen tipo y todos los tipos derivan en última instancia de <xref:System.Object?displayProperty=nameWithType>, puede escribir y compilar código como el siguiente:

[!code-csharp[csProgGuideTypes#37](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/Class1.cs#37)]

## <a name="generic-types"></a>Tipos genéricos

Los tipos se pueden declarar con uno o varios *parámetros de tipo* que actúan como un marcador de posición para el tipo real (el *tipo concreto*) que proporcionará el código de cliente cuando cree una instancia del tipo. Estos tipos se denominan *tipos genéricos*. Por ejemplo, el tipo de .NET <xref:System.Collections.Generic.List%601?displayProperty=nameWithType> tiene un parámetro de tipo al que, por convención, se le denomina *T*. Cuando crea una instancia del tipo, especifica el tipo de los objetos que contendrá la lista, por ejemplo, la cadena:

```csharp
List<string> stringList = new List<string>();
stringList.Add("String example");
// compile time error adding a type other than a string:
stringList.Add(4);
```

El uso del parámetro de tipo permite reutilizar la misma clase para incluir cualquier tipo de elemento, sin necesidad de convertir cada elemento en [object](../../../csharp/language-reference/keywords/object.md). Las clases de colección genéricas se denominan *colecciones fuertemente tipadas* porque el compilador conoce el tipo específico de los elementos de la colección y puede generar un error en tiempo de compilación si, por ejemplo, intenta agregar un valor entero al objeto `stringList` del ejemplo anterior. Para más información, vea [Genéricos](../../../csharp/programming-guide/generics/index.md).

## <a name="implicit-types-anonymous-types-and-nullable-types"></a>Tipos implícitos, tipos anónimos y tipos que aceptan valores NULL

Como se ha mencionado anteriormente, puede asignar implícitamente un tipo a una variable local (pero no miembros de clase) mediante la palabra clave [var](../../../csharp/language-reference/keywords/var.md). La variable sigue recibiendo un tipo en tiempo de compilación, pero este lo proporciona el compilador. Para más información, vea [Variables locales con asignación implícita de tipos](../../../csharp/programming-guide/classes-and-structs/implicitly-typed-local-variables.md).

En algunos casos, resulta conveniente crear un tipo con nombre para conjuntos sencillos de valores relacionados que no desea almacenar ni pasar fuera de los límites del método. Puede crear *tipos anónimos* para este fin. Para más información, vea [Tipos anónimos](../../../csharp/programming-guide/classes-and-structs/anonymous-types.md).

Los tipos de valor normales no pueden tener un valor [null](../../../csharp/language-reference/keywords/null.md), pero se pueden crear tipos de valor que aceptan valores NULL mediante la adición de `?` después del tipo. Por ejemplo, `int?` es un tipo `int` que también puede tener el valor [null](../../../csharp/language-reference/keywords/null.md). En CTS, los tipos que aceptan valores NULL son instancias del tipo struct genérico <xref:System.Nullable%601?displayProperty=nameWithType>. Los tipos que aceptan valores NULL son especialmente útiles cuando se pasan datos hacia y desde bases de datos en las que los valores numéricos podrían ser nulos. Para más información, vea [Tipos que aceptan valores NULL](../../../csharp/programming-guide/nullable-types/index.md).

## <a name="related-sections"></a>Secciones relacionadas

Para obtener más información, vea los temas siguientes:

- [Conversiones de tipos](../../../csharp/programming-guide/types/casting-and-type-conversions.md)

- [Conversión boxing y conversión unboxing](../../../csharp/programming-guide/types/boxing-and-unboxing.md)

- [Uso de tipo dinámico](../../../csharp/programming-guide/types/using-type-dynamic.md)

- [Tipos de valor](../../../csharp/language-reference/keywords/value-types.md)

- [Tipos de referencia](../../../csharp/language-reference/keywords/reference-types.md)

- [Clases y structs](../../../csharp/programming-guide/classes-and-structs/index.md)

- [Tipos anónimos](../../../csharp/programming-guide/classes-and-structs/anonymous-types.md)

- [Genéricos](../../../csharp/programming-guide/generics/index.md)

## <a name="c-language-specification"></a>Especificación del lenguaje C#

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>Vea también

- [Referencia de C#](../../../csharp/language-reference/index.md)
- [Guía de programación de C#](../../../csharp/programming-guide/index.md)
- [Conversión de tipos de datos XML](../../../standard/data/xml/conversion-of-xml-data-types.md)
- [Tipos enteros](../../language-reference/builtin-types/integral-numeric-types.md)
