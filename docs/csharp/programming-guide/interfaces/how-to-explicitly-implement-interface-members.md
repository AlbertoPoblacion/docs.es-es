---
title: 'Procedimiento Implementar explícitamente miembros de interfaz: Guía de programación de C#'
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- interfaces [C#], explicitly implementing
ms.assetid: 514cde76-f981-474e-8b40-9493619f899c
ms.openlocfilehash: 8cef6c840bf6afff8ccbf7d02012990e11d47991
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2019
ms.locfileid: "64595371"
---
# <a name="how-to-explicitly-implement-interface-members-c-programming-guide"></a>Procedimiento Implementar explícitamente miembros de interfaz (Guía de programación de C#)
Este ejemplo declara una [interfaz](../../../csharp/language-reference/keywords/interface.md), `IDimensions`, y una clase, `Box`, que implementa explícitamente los miembros de interfaz `getLength` y `getWidth`. Se tiene acceso a los miembros mediante la instancia de interfaz `dimensions`.  
  
## <a name="example"></a>Ejemplo  
 [!code-csharp[csProgGuideInheritance#8](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#8)]  
  
## <a name="robust-programming"></a>Programación sólida  
  
- Tenga en cuenta que las siguientes líneas, en el método `Main`, se comentan porque producirían errores de compilación. No se puede tener acceso a un miembro de interfaz que se implementa explícitamente desde una instancia [class](../../../csharp/language-reference/keywords/class.md):  
  
     [!code-csharp[csProgGuideInheritance#45](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#45)]  
  
- Tenga en cuenta también que las líneas siguientes, en el método `Main`, imprimen correctamente las dimensiones del cuadro porque se llama a los métodos desde una instancia de la interfaz:  
  
     [!code-csharp[csProgGuideInheritance#46](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#46)]  
  
## <a name="see-also"></a>Vea también

- [Guía de programación de C#](../../../csharp/programming-guide/index.md)
- [Clases y structs](../../../csharp/programming-guide/classes-and-structs/index.md)
- [Interfaces](../../../csharp/programming-guide/interfaces/index.md)
- [Cómo: Implementar explícitamente miembros de dos interfaces](../../../csharp/programming-guide/interfaces/how-to-explicitly-implement-members-of-two-interfaces.md)
