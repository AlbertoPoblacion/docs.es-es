---
title: No está definido el tipo '<typename>'
ms.date: 07/20/2015
f1_keywords:
- vbc30002
- bc30002
helpviewer_keywords:
- BC30002
ms.assetid: b0faf204-57fd-44de-8c05-9db027eea663
ms.openlocfilehash: c2675d61307d92da1710368668f43af3559060a3
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "58825045"
---
# <a name="type-typename-is-not-defined"></a>Tipo de '\<typename >' no está definido
La instrucción hace referencia a un tipo que no se ha definido. Puede definir un tipo en una instrucción de declaración como `Enum`, `Structure`, `Class`, o `Interface`.  
  
 **Identificador de error:** BC30002  
  
## <a name="to-correct-this-error"></a>Para corregir este error  
  
-   Asegúrese de que la definición de tipo y su referencia usan la misma ortografía.  
  
-   Asegúrese de que la definición de tipo es accesible para la referencia. Por ejemplo, si el tipo está en otro módulo y se ha declarado `Private`, mueva la definición de tipo al que hace referencia a módulo o declárelo `Public`.  
  
-   Asegúrese de que el espacio de nombres del tipo no se ha redefinido en el proyecto. Si es así, utilice el `Global` palabra clave para el nombre de tipo completo. Por ejemplo, si un proyecto define un espacio de nombres denominado `System`, <xref:System.Object?displayProperty=nameWithType> tipo no se puede acceder a menos que se completa con el `Global` palabra clave: `Global.System.Object`.  
  
-   Si el tipo está definido, pero no se registra la biblioteca de objetos o la biblioteca de tipos en el que se define en Visual Basic, haga clic **Agregar referencia** en el **proyecto** menú y, a continuación, seleccione el objeto adecuado biblioteca o biblioteca de tipos.  
  
-   Asegúrese de que el tipo está en un ensamblado que es parte del perfil de .NET Framework de destino. Para obtener más información, consulte [Solucionar problemas de versión de .NET Framework de destino](/visualstudio/msbuild/troubleshooting-dotnet-framework-targeting-errors).  
  
## <a name="see-also"></a>Vea también

- [Espacios de nombres en Visual Basic](../../../visual-basic/programming-guide/program-structure/namespaces.md)
- [Enum (instrucción)](../../../visual-basic/language-reference/statements/enum-statement.md)
- [Structure (instrucción)](../../../visual-basic/language-reference/statements/structure-statement.md)
- [Class (instrucción)](../../../visual-basic/language-reference/statements/class-statement.md)
- [Interface (instrucción)](../../../visual-basic/language-reference/statements/interface-statement.md)
- [Administrar referencias en un proyecto](/visualstudio/ide/managing-references-in-a-project)
