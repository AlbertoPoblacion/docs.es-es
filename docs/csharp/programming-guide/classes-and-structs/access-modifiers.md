---
title: 'Modificadores de acceso: Guía de programación de C#'
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- C# Language, access modifiers
- access modifiers [C#], about
ms.assetid: 6e81ee82-224f-4a12-9baf-a0dca2656c5b
ms.openlocfilehash: 6622612e927b800e1a4769c99df0e2fa7d99a33d
ms.sourcegitcommit: eaa6d5cd0f4e7189dbe0bd756e9f53508b01989e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/07/2019
ms.locfileid: "67609653"
---
# <a name="access-modifiers-c-programming-guide"></a>Modificadores de acceso (Guía de programación de C#)
Todos los tipos y miembros de tipo tienen un nivel de accesibilidad que controla si se pueden usar desde otro código del ensamblado u otros ensamblados. Puede usar los siguientes modificadores de acceso para especificar la accesibilidad de un tipo o miembro cuando lo declare:  
  
 [public](../../../csharp/language-reference/keywords/public.md)  
 Puede obtener acceso al tipo o miembro cualquier otro código del mismo ensamblado o de otro ensamblado que haga referencia a éste. 
  
 [private](../../../csharp/language-reference/keywords/private.md)  
 Solamente el código de la misma clase o estructura puede acceder al tipo o miembro.  
  
 [protected](../../../csharp/language-reference/keywords/protected.md)  
 Solamente el código de la misma clase, o de una clase derivada de esa clase, puede acceder al tipo o miembro.  
 [internal](../../../csharp/language-reference/keywords/internal.md)  
 Puede obtener acceso al tipo o miembro cualquier código del mismo ensamblado, pero no de un ensamblado distinto.  
  
 [protected internal](../../../csharp/language-reference/keywords/protected-internal.md) Cualquier código del ensamblado en el que se ha declarado, o desde cualquier clase derivada de otro ensamblado, puede acceder al tipo o miembro. 

 [private protected](../../../csharp/language-reference/keywords/private-protected.md) El código de la misma clase, o de un tipo derivado de esa clase, puede acceder al tipo o miembro solo dentro de su ensamblado que declara.
  
 En los ejemplos siguientes se muestra cómo especificar modificadores de acceso en un tipo y miembro:  
  
 [!code-csharp[csProgGuideObjects#72](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#72)]  
  
 No todos los tipos o miembros pueden usar todos los modificadores de acceso en todos los contextos; en algunos casos la accesibilidad de un miembro de tipo está restringida por la accesibilidad de su tipo contenedor. En las secciones siguientes se proporcionan más detalles sobre la accesibilidad.  
  
## <a name="class-and-struct-accessibility"></a>Accesibilidad de clase y estructura  
 Las clases y estructuras que se declaran directamente en un espacio de nombres (es decir, que no están anidadas en otras clases o estructuras) pueden ser públicas o internas. Si no se especifica ningún modificador de acceso, el valor predeterminado es internal.  
  
 Los miembros de estructura, incluidas las clases y las estructuras anidadas, se pueden declarar como public, internal, o private. Los miembros de clase, incluidas las clases y las estructuras anidadas, pueden ser public, protected internal, protected, internal, private protected o private. El nivel de acceso de los miembros de clase y los miembros de estructura, incluidas las clases y estructuras anidadas, es private de forma predeterminada. Los tipos anidados privados no son accesibles desde fuera del tipo contenedor.  
  
 Las clases derivadas no pueden tener mayor accesibilidad que sus tipos base. En otras palabras, no puede tener una clase pública `B` que derive de una clase interna `A`. Si se permitiera, convertiría `A` en público, porque todos los miembros protegidos o internos de `A` son accesibles desde la clase derivada.  
  
 Puede habilitar otros ensamblados concretos para acceder a los tipos internos mediante InternalsVisibleToAttribute. Para más información, vea [Ensamblados de confianza](../../../standard/assembly/friend-assemblies.md).  
  
## <a name="class-and-struct-member-accessibility"></a>Accesibilidad de miembros de clase y estructura  
 Los miembros de clase (incluidas las clases y las estructuras anidadas) se pueden declarar con cualquiera de los seis tipos de acceso. Los miembros de estructura no se pueden declarar como protegidos porque las estructuras no admiten la herencia.  
  
 Normalmente, la accesibilidad de un miembro no es mayor que la del tipo que lo contiene. Pero un miembro público de una clase interna podría ser accesible desde fuera del ensamblado si el miembro implementa los métodos de interfaz o invalida los métodos virtuales definidos en una clase base pública.  
  
 El tipo de cualquier miembro que sea un campo, propiedad o evento debe ser al menos tan accesible como el propio miembro. Del mismo modo, el tipo devuelto y los tipos de parámetro de cualquier miembro que sea un método, indizador o delegado deben ser al menos tan accesibles como el propio miembro. Por ejemplo, no puede tener un método público `M` que devuelva una clase `C` a menos que `C` también sea público. Del mismo modo, no puede tener una propiedad protegida de tipo `A` si `A` se declara como private.  
  
 Los operadores definidos por el usuario siempre deben declararse como public y static. Para obtener más información, vea [Sobrecarga de operadores](../../../csharp/language-reference/operators/operator-overloading.md).  
  
 Los finalizadores no pueden tener modificadores de accesibilidad.  
  
 Para establecer el nivel de acceso de un miembro de clase o estructura, agregue la palabra clave adecuada a la declaración de miembro, como se muestra en el ejemplo siguiente.  
  
 [!code-csharp[csProgGuideObjects#73](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#73)]  
  
> [!NOTE]
>  El nivel de accesibilidad protected internal significa protected O internal, no protected E internal. Es decir, se puede acceder a un miembro protegido interno desde cualquier clase del mismo ensamblado, incluidas las clases derivadas. Para limitar la accesibilidad a las clases derivadas del mismo ensamblado, declare la propia clase como internal y sus miembros como protected. Además, a partir de C# 7.2, puede usar el modificador de acceso private protected para lograr el mismo resultado sin necesidad de convertir en internal la clase contenedora.  
  
## <a name="other-types"></a>Otros tipos  
 Las interfaces declaradas directamente en un espacio de nombres se pueden declarar como public o internal y, al igual que las clases y las estructuras, su valor predeterminado es el acceso interno. Los miembros de interfaz son siempre públicos porque el propósito de una interfaz es permitir que otros tipos accedan a una clase o estructura. A los miembros de interfaz no se les puede aplicar ningún modificador de acceso.  
  
 Los miembros de enumeración siempre son públicos y no se les puede aplicar ningún modificador de acceso.  
  
 Los delegados se comportan como las clases y las estructuras. De forma predeterminada, tienen acceso interno cuando se declaran directamente en un espacio de nombres y acceso privado cuando están anidados.  
  
## <a name="c-language-specification"></a>Especificación del lenguaje C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>Vea también

- [Guía de programación de C#](../../../csharp/programming-guide/index.md)
- [Clases y structs](../../../csharp/programming-guide/classes-and-structs/index.md)
- [Interfaces](../../../csharp/programming-guide/interfaces/index.md)
- [private](../../../csharp/language-reference/keywords/private.md)
- [public](../../../csharp/language-reference/keywords/public.md)
- [internal](../../../csharp/language-reference/keywords/internal.md)
- [protected](../../../csharp/language-reference/keywords/protected.md)
- [protected internal](../../../csharp/language-reference/keywords/protected-internal.md)
- [private protected](../../../csharp/language-reference/keywords/private-protected.md)
- [class](../../../csharp/language-reference/keywords/class.md)
- [struct](../../../csharp/language-reference/keywords/struct.md)
- [interface](../../../csharp/language-reference/keywords/interface.md)
