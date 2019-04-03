---
title: Los parámetros de tipo no se pueden utilizar como calificadores
ms.date: 07/20/2015
f1_keywords:
- vbc32098
- bc32098
helpviewer_keywords:
- BC32098
ms.assetid: bab05325-dde8-4621-a5f6-368b5b7b2d76
ms.openlocfilehash: 974d2935e64151109b688f576229fb008b59b229
ms.sourcegitcommit: bce0586f0cccaae6d6cbd625d5a7b824d1d3de4b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/02/2019
ms.locfileid: "58819806"
---
# <a name="type-parameters-cannot-be-used-as-qualifiers"></a>Los parámetros de tipo no se pueden utilizar como calificadores
Un elemento de programación se califica con una cadena de calificación que incluye un parámetro de tipo.  
  
 Un parámetro de tipo representa un requisito para un tipo que va a proporcionar al construir el tipo genérico. No representa un tipo específico definido. Una cadena de calificación debe incluir solo los elementos que se definen en tiempo de compilación.  
  
 Las instrucciones siguientes pueden generar este error.  
  
```  
Public Function checkText(Of c As System.Windows.Forms.Control)(  
    ByVal badText As String) As Boolean  
  
    Dim saveText As c.Text  
    ' Insert code to look for badText within saveText.  
End Function  
```  
  
 **Identificador de error:** BC32098  
  
## <a name="to-correct-this-error"></a>Para corregir este error  
  
1.  Quite el parámetro de tipo de la cadena de calificación o reemplazarlo con un tipo definido.  
  
2.  Si necesita utilizar un tipo construido para localizar el elemento de programación que se completa, debe usar la lógica del programa adicionales.  
  
## <a name="see-also"></a>Vea también

- [Referencias a elementos declarados](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)
- [Generic Types in Visual Basic](../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)
- [Lista de tipos](../../../visual-basic/language-reference/statements/type-list.md)
