---
title: Friend (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.Friend
helpviewer_keywords:
- Friend keyword [Visual Basic]
- Friend access modifier
- Friend keyword [Visual Basic], syntax
- Protected Friend keyword combination
- Friend keyword [Visual Basic], and Protected
ms.assetid: b664605e-1c79-4728-b996-aa59c50846bc
ms.openlocfilehash: 18681935d0380f9be3970fdb5d17ffb089152f59
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61802549"
---
# <a name="friend-visual-basic"></a>Friend (Visual Basic)
Especifica que uno o varios elementos de programación declarados son accesibles únicamente desde dentro del ensamblado que contiene su declaración.  
  
## <a name="remarks"></a>Comentarios  
 En muchos casos, desea que elementos de programación como clases y estructuras que se usará en todo el ensamblado, no solo por el componente que declara. Sin embargo, es posible que no desea que sea accesible para el código fuera del ensamblado (por ejemplo, si la aplicación es propietaria). Si desea limitar el acceso a un elemento de esta manera, puede declarar mediante el `Friend` modificador.  
  
 Código de otras clases, estructuras y los módulos que se compilan en el mismo ensamblado puede tener acceso a todas las `Friend` elementos en ese ensamblado.  
  
 `Friend` acceso a menudo es el nivel preferido para los elementos de programación de la aplicación, y `Friend` es el acceso predeterminado en nivel de una interfaz, un módulo, una clase o una estructura.  
  
 Puede usar `Friend` sólo en el nivel de módulo, interfaz o espacio de nombres. Por lo tanto, el contexto de declaración de un `Friend` elemento debe ser un archivo de código fuente, un espacio de nombres, una interfaz, un módulo, una clase o una estructura; no puede ser un procedimiento.  

> [!NOTE]
> También puede usar el [Protected Friend](protected-friend.md) modificador de acceso, lo que hace que un miembro de clase accesible desde dentro de esa clase, desde las clases derivadas y desde el mismo ensamblado en el que se define la clase. Para restringir el acceso a un miembro desde dentro de su clase y de las clases derivadas en el mismo ensamblado, usa el [Private Protected](private-protected.md) modificador de acceso.

 Para obtener una comparación de `Friend` y otros modificadores de acceso, consulte [tener acceso a los niveles en Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md).  
  
> [!NOTE]
>  Puede especificar que el otro ensamblado es un ensamblado de confianza, lo que le permite tener acceso a todos los tipos y miembros que están marcados como `Friend`. Para más información, vea [Ensamblados de confianza](../../../standard/assembly/friend-assemblies.md).  
  
## <a name="example"></a>Ejemplo  
 La siguiente clase utiliza la `Friend` modificador para permitir que otros elementos de programación dentro del mismo ensamblado para tener acceso a ciertos miembros.  
  
 [!code-vb[VbVbalrAccessModifiers#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbvbalraccessmodifiers/vb/class1.vb#1)]  
  
## <a name="usage"></a>Uso  
 Puede usar el `Friend` modificador en estos contextos:  
  
 [Class (instrucción)](../../../visual-basic/language-reference/statements/class-statement.md)  
  
 [Const (instrucción)](../../../visual-basic/language-reference/statements/const-statement.md)  
  
 [Declare (instrucción)](../../../visual-basic/language-reference/statements/declare-statement.md)  
  
 [Delegate (instrucción)](../../../visual-basic/language-reference/statements/delegate-statement.md)  
  
 [Dim (instrucción)](../../../visual-basic/language-reference/statements/dim-statement.md)  
  
 [Enum (instrucción)](../../../visual-basic/language-reference/statements/enum-statement.md)  
  
 [Event (instrucción)](../../../visual-basic/language-reference/statements/event-statement.md)  
  
 [Function (instrucción)](../../../visual-basic/language-reference/statements/function-statement.md)  
  
 [Interface (instrucción)](../../../visual-basic/language-reference/statements/interface-statement.md)  
  
 [Module (instrucción)](../../../visual-basic/language-reference/statements/module-statement.md)  
  
 [Property (instrucción)](../../../visual-basic/language-reference/statements/property-statement.md)  
  
 [Structure (instrucción)](../../../visual-basic/language-reference/statements/structure-statement.md)  
  
 [Sub (instrucción)](../../../visual-basic/language-reference/statements/sub-statement.md)  
  
## <a name="see-also"></a>Vea también

- <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>
- [Public](../../../visual-basic/language-reference/modifiers/public.md)
- [Protected](../../../visual-basic/language-reference/modifiers/protected.md)
- [Private](../../../visual-basic/language-reference/modifiers/private.md)
- [Private Protected](./private-protected.md)
- [Protected Friend](./protected-friend.md)
- [Niveles de acceso en Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)
- [Procedimientos](../../../visual-basic/programming-guide/language-features/procedures/index.md)
- [Estructuras](../../../visual-basic/programming-guide/language-features/data-types/structures.md)
- [Objetos y clases](../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)
