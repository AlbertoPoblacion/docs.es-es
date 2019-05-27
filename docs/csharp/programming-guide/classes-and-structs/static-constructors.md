---
title: 'Constructores estáticos: Guía de programación de C#'
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- static constructors [C#]
- constructors [C#], static
ms.assetid: 151ec95e-3c4d-4ed7-885d-95b7a3be2e7d
ms.openlocfilehash: 110d83caad0c588fa899a4129897784e9c74aab8
ms.sourcegitcommit: c4e9d05644c9cb89de5ce6002723de107ea2e2c4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2019
ms.locfileid: "65881912"
---
# <a name="static-constructors-c-programming-guide"></a>Constructores estáticos (Guía de programación de C#)
Un constructor estático se usa para inicializar cualquier dato [estático](../../../csharp/language-reference/keywords/static.md) o realizar una acción determinada que solo debe realizarse una vez. Es llamado automáticamente antes de crear la primera instancia o de hacer referencia a cualquier miembro estático.  
  
 [!code-csharp[csProgGuideObjects#14](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#14)]  
  
 Los constructores estáticos tienen las propiedades siguientes:  
  
- Un constructor estático no permite modificadores de acceso ni tiene parámetros.  
  
- Se le llama automáticamente para inicializar la [clase](../../../csharp/language-reference/keywords/class.md) antes de crear la primera instancia o de hacer referencia a cualquier miembro estático. Observe que se llama al constructor estático de un tipo cuando se invoca a un método estático asignado a un evento o un delegado y no cuando se asigna.
  
- Un constructor estático no puede ser llamado directamente.  
  
- El usuario no puede controlar cuándo se ejecuta el constructor estático en el programa.  
  
- Los constructores estáticos se usan normalmente cuando la clase hace uso de un archivo de registro y el constructor escribe entradas en dicho archivo.  
  
- Los constructores estáticos también son útiles al crear clases contenedoras para código no administrado, cuando el constructor puede llamar al método `LoadLibrary`.  
  
- Si un constructor estático inicia una excepción, el motor en tiempo de ejecución no lo invocará una segunda vez y el tipo seguirá sin inicializar durante el período de duración del dominio de aplicación donde se ejecuta el programa.  
  
## <a name="example"></a>Ejemplo  
 En este ejemplo, la clase `Bus` tiene un constructor estático. Cuando se crea la primera instancia de `Bus` (`bus1`), se invoca el constructor estático para inicializar la clase. En el resultado del ejemplo, se comprueba que el constructor estático se ejecuta solo una vez, incluso si se crean dos instancias de `Bus`, y que se ejecuta antes de que se ejecute el constructor de instancia.  
  
 [!code-csharp[csProgGuideObjects#15](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#15)]  
  
## <a name="see-also"></a>Vea también

- [Guía de programación de C#](../../../csharp/programming-guide/index.md)
- [Clases y structs](../../../csharp/programming-guide/classes-and-structs/index.md)
- [Constructores](../../../csharp/programming-guide/classes-and-structs/constructors.md)
- [Clases estáticas y sus miembros](../../../csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members.md)
- [Finalizadores](../../../csharp/programming-guide/classes-and-structs/destructors.md)
