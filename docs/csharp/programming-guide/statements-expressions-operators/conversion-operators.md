---
title: 'Operadores de conversión: Guía de programación de C#'
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- C# language, conversion operators
- conversion operators [C#]
- operators [C#], conversion
- user-defined conversions [C#]
ms.assetid: c5ad73a3-d57b-4d2b-b4c9-24e3c2856efc
ms.openlocfilehash: 43e81a342377b155fafe26bd0430384cddad5fd4
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2019
ms.locfileid: "64608229"
---
# <a name="conversion-operators-c-programming-guide"></a>Operadores de conversión (Guía de programación de C#)

C# permite a los programadores declarar conversiones en clases o structs, de manera que las clases o structs puedan convertirse a o desde otras clases o structs, o tipos básicos. Las conversiones se definen como los operadores y se denominan por el tipo al que se convierten. El tipo del argumento que se va a convertir o el tipo del resultado de la conversión, pero no ambos, debe ser el tipo contenedor.  
  
 [!code-csharp[csProgGuideStatements#10](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideStatements/CS/Statements.cs#10)]  
  
## <a name="conversion-operators-overview"></a>Información general sobre operadores de conversión

 Los operadores de conversión tienen las propiedades siguientes:  
  
- Las conversiones declaradas como `implicit` se producen automáticamente cuando se necesita.  
  
- Las conversiones declaradas como `explicit` necesitan que se llame a una conversión.  
  
- Todas las conversiones se deben declarar como `static`.  
  
## <a name="related-sections"></a>Secciones relacionadas

 Para obtener más información:  
  
- [Utilizar operadores de conversión](../../../csharp/programming-guide/statements-expressions-operators/using-conversion-operators.md)  
  
- [Conversiones de tipos](../../../csharp/programming-guide/types/casting-and-type-conversions.md)  
  
- [Cómo: Implementar conversiones definidas por el usuario entre structs](../../../csharp/programming-guide/statements-expressions-operators/how-to-implement-user-defined-conversions-between-structs.md)  
  
- [explicit](../../../csharp/language-reference/keywords/explicit.md)  
  
- [implicit](../../../csharp/language-reference/keywords/implicit.md)  
  
- [static](../../../csharp/language-reference/keywords/static.md)  
  
## <a name="see-also"></a>Vea también

- <xref:System.Convert>
- [Guía de programación de C#](../../../csharp/programming-guide/index.md)
- [Chained user-defined explicit conversions in C#](https://blogs.msdn.microsoft.com/ericlippert/2007/04/16/chained-user-defined-explicit-conversions-in-c/) (Conversiones explícitas encadenadas definidas por el usuario en C#)
