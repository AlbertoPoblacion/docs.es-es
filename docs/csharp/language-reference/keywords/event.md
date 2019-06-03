---
title: 'event: Referencia de C#'
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- event
- remove
- event_CSharpKeyword
- add
helpviewer_keywords:
- event keyword [C#]
ms.assetid: 7858fd85-153b-4259-85d0-6aa13c35f174
ms.openlocfilehash: 9575d6e998ff709b06f1da21abd17a3629c17029
ms.sourcegitcommit: 26f4a7697c32978f6a328c89dc4ea87034065989
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/28/2019
ms.locfileid: "66251042"
---
# <a name="event-c-reference"></a>event (Referencia de C#)
La palabra clave `event` se usa para declarar un evento en una clase de publicador.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se muestra cómo declarar y generar un evento que usa <xref:System.EventHandler> como el tipo de delegado subyacente. Para obtener el código de ejemplo completo que también muestra cómo usar el tipo delegado <xref:System.EventHandler%601> genérico y cómo suscribirse a un evento y crear un método de controlador de evento, vea [Cómo: Publicar eventos que cumplan las directrices de .NET Framework](../../../csharp/programming-guide/events/how-to-publish-events-that-conform-to-net-framework-guidelines.md).  
  
 [!code-csharp[csrefKeywordsModifiers#7](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsModifiers/CS/csrefKeywordsModifiers.cs#7)]
  
 Los eventos son un tipo especial de delegado de multidifusión que solo se pueden invocar desde la clase o el struct en la que se declaran (la clase de publicador). Si otras clases o structs se suscriben al evento, se llamará a sus métodos de controlador de eventos cuando la clase de publicador genera el evento. Para más información y ejemplos de código, vea [Eventos](../../../csharp/programming-guide/events/index.md) y [Delegados](../../../csharp/programming-guide/delegates/index.md).  
  
 Las constantes pueden marcarse como [public](../../../csharp/language-reference/keywords/public.md), [private](../../../csharp/language-reference/keywords/private.md), [protected](../../../csharp/language-reference/keywords/protected.md), [internal](../../../csharp/language-reference/keywords/internal.md), [protected internal](../../../csharp/language-reference/keywords/protected-internal.md) o [private protected](../../../csharp/language-reference/keywords/private-protected.md). Estos modificadores de acceso definen cómo los usuarios de la clase pueden obtener acceso al evento. Para obtener más información, vea [Modificadores de acceso](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md).  
  
## <a name="keywords-and-events"></a>Palabras clave y eventos  
 Las palabras clave siguientes se aplican a eventos.  
  
|Palabra clave|Descripción|Para obtener más información|  
|-------------|-----------------|--------------------------|  
|[static](../../../csharp/language-reference/keywords/static.md)|Hace que el evento esté disponible para los llamadores en cualquier momento, aunque no exista ninguna instancia de la clase.|[Clases estáticas y sus miembros](../../../csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members.md)|  
|[virtual](../../../csharp/language-reference/keywords/virtual.md)|Permite que las clases derivadas invaliden el comportamiento de eventos mediante la palabra clave [override](../../../csharp/language-reference/keywords/override.md).|[Herencia](../../../csharp/programming-guide/classes-and-structs/inheritance.md)|  
|[sealed](../../../csharp/language-reference/keywords/sealed.md)|Especifica que ya no es virtual para las clases derivadas.||  
|[abstract](../../../csharp/language-reference/keywords/abstract.md)|El compilador no generará los bloques de descriptor de acceso de eventos `add` y `remove`, y por tanto, las clases deben proporcionar su propia implementación.||  
  
 Un evento puede declararse como evento estático mediante la palabra clave [static](../../../csharp/language-reference/keywords/static.md). Esto hace que el evento esté disponible para los llamadores en cualquier momento, aunque no exista ninguna instancia de la clase. Para más información, vea [Clases estáticas y sus miembros](../../../csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members.md).  
  
 Un evento puede marcarse como virtual mediante la palabra clave [virtual](../../../csharp/language-reference/keywords/virtual.md). Esto permite que las clases derivadas invaliden el comportamiento de eventos mediante la palabra clave [override](../../../csharp/language-reference/keywords/override.md). Para obtener más información, vea [Herencia](../../../csharp/programming-guide/classes-and-structs/inheritance.md). Un evento que reemplaza un evento virtual también puede ser [sealed](../../../csharp/language-reference/keywords/sealed.md), que especifica que ya no es virtual para las clases derivadas. Por último, se puede declarar un evento como [abstract](../../../csharp/language-reference/keywords/abstract.md), lo que significa que el compilador no generará los bloques de descriptor de acceso de eventos `add` y `remove`. Por tanto, las clases derivadas deben proporcionar una implementación propia.  
  
## <a name="c-language-specification"></a>Especificación del lenguaje C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>Vea también

- [Referencia de C#](../../../csharp/language-reference/index.md)
- [Guía de programación de C#](../../../csharp/programming-guide/index.md)
- [Palabras clave de C#](../../../csharp/language-reference/keywords/index.md)
- [add](../../../csharp/language-reference/keywords/add.md)
- [remove](../../../csharp/language-reference/keywords/remove.md)
- [Modificadores](../../../csharp/language-reference/keywords/modifiers.md)
- [Cómo: Combinar delegados (delegados de multidifusión)](../../../csharp/programming-guide/delegates/how-to-combine-delegates-multicast-delegates.md)
