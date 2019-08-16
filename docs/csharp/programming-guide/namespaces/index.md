---
title: 'Espacios de nombres: Guía de programación de C#'
ms.custom: seodec18
ms.date: 08/21/2018
helpviewer_keywords:
- C# language, namespaces
- namespaces [C#]
ms.assetid: b1c4ab46-3fad-4ffa-9deb-dd50a2d8c65a
ms.openlocfilehash: cf5a7f239cf7d3cd3a6e39f31d16adb830646afc
ms.sourcegitcommit: cf9515122fce716bcfb6618ba366e39b5a2eb81e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/15/2019
ms.locfileid: "69039489"
---
# <a name="namespaces-c-programming-guide"></a>Espacios de nombres (Guía de programación de C#)

Los espacios de nombres se usan mucho en programación de C# de dos maneras. En primer lugar, .NET Framework usa espacios de nombres para organizar sus clases, de la siguiente manera:  
  
 [!code-csharp[csProgGuide#22](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuide/CS/progGuide.cs#22)]  
  
`System` es un espacio de nombres y `Console` es una clase de ese espacio de nombres. La palabra clave `using` se puede usar para que no se necesite el nombre completo, como en el ejemplo siguiente:  
  
 [!code-csharp[csProgGuide#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuide/CS/using.cs#1)]  
  
 [!code-csharp[csProgGuide#25](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuide/CS/progGuide.cs#25)]  
  
Para más información, vea [using (Directiva)](../../language-reference/keywords/using-directive.md).  
  
En segundo lugar, declarar sus propios espacios de nombres puede ayudarle a controlar el ámbito de nombres de clase y método en proyectos de programación grandes. Use la palabra clave [namespace](../../language-reference/keywords/namespace.md) para declarar un espacio de nombres, como en el ejemplo siguiente:  
  
 [!code-csharp[csProgGuideNamespaces#6](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideNamespaces/CS/Namespaces.cs#6)]

El nombre del espacio de nombres debe ser un [nombre de identificador](../inside-a-program/identifier-names.md) de C# válido.

## <a name="namespaces-overview"></a>Información general sobre los espacios de nombres  

Los espacios de nombres tienen las propiedades siguientes:  
  
- Organizan proyectos de código de gran tamaño.  
- Se delimitan mediante el operador `.`.  
- La directiva `using` obvia la necesidad de especificar el nombre del espacio de nombres para cada clase.  
- El espacio de nombres `global` es el espacio de nombres "raíz": `global::System` siempre hará referencia al espacio de nombres <xref:System> de .NET.  

## <a name="c-language-specification"></a>Especificación del lenguaje C#

Para más información, vea la sección [Espacio de nombres](~/_csharplang/spec/namespaces.md) de la [Especificación del lenguaje C#](~/_csharplang/spec/introduction.md).
  
## <a name="see-also"></a>Vea también

- [Guía de programación de C#](../index.md)
- [Utilizar espacios de nombres](using-namespaces.md)
- [Cómo: Utilizar el espacio de nombres My](how-to-use-the-my-namespace.md)
- [Nombres de identificador](../inside-a-program/identifier-names.md)
- [using (directiva)](../../language-reference/keywords/using-directive.md)
- [:: !](../../language-reference/operators/namespace-alias-qualifier.md)
