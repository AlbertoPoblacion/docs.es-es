---
title: Filtrar Ocultar una Variable con el mismo nombre que su Variable (Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- qualification [Visual Basic], of element names
- declarations [Visual Basic], elements
- element names [Visual Basic], qualification
- references [Visual Basic], declared elements
- declaration statements [Visual Basic], declared elements
- declaring elements [Visual Basic]
- referencing declared elements [Visual Basic]
- declared elements [Visual Basic], referencing
- declared elements [Visual Basic], about declared elements
ms.assetid: e39c0752-f19f-4d2e-a453-00df1b5fc7ee
ms.openlocfilehash: 744c7aed50690d5591d1e8248e121cb66ef39108
ms.sourcegitcommit: 558d78d2a68acd4c95ef23231c8b4e4c7bac3902
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/09/2019
ms.locfileid: "59296191"
---
# <a name="how-to-hide-a-variable-with-the-same-name-as-your-variable-visual-basic"></a>Filtrar Ocultar una Variable con el mismo nombre que su Variable (Visual Basic)
Puede ocultar una variable por *sombrear* él, es decir, si se redefine con una variable del mismo nombre. Puede reemplazar la variable que desea ocultar de dos maneras:  
  
-   **Sombreado por ámbito.** Puede ocultar a través de ámbito por si vuelve a declarar dentro de una subregión de la región que contiene la variable que desea ocultar.  
  
-   **Sombreado por herencia.** Si la variable que desea ocultar se define en el nivel de clase, puede reemplazar mediante herencia volviéndola a declarar con la [sombras](../../../../visual-basic/language-reference/modifiers/shadows.md) palabra clave en una clase derivada.  
  
## <a name="two-ways-to-hide-a-variable"></a>Dos maneras para ocultar una Variable  
  
#### <a name="to-hide-a-variable-by-shadowing-it-through-scope"></a>Para ocultar una variable por él sombreado por ámbito  
  
1. Determinar la región en la definición de la variable que desee ocultar y determine una subregión en la que se va a volver a definirlo con la variable.  
  
    |Región de la variable|Subregión permitida para volverla a definir|  
    |-----------------------|-------------------------------------------|  
    |Module|Una clase dentro del módulo|  
    |Clase|Una subclase dentro de la clase<br /><br /> Un procedimiento dentro de la clase|  
  
     No se puede definir una variable de procedimiento en un bloque dentro de ese procedimiento, por ejemplo en un `If`... `End If` construcción o `For` bucle.  
  
2. Cree la subregión si aún no existe.  
  
3. Dentro de la subregión, escribir un [instrucción Dim](../../../../visual-basic/language-reference/statements/dim-statement.md) declarar la variable de sombreado.  
  
     Cuando el código de la subregión hace referencia al nombre de variable, el compilador resuelve la referencia a la variable de sombreado.  
  
     El ejemplo siguiente ilustra el sombreado por ámbito, así como una referencia que omite el sombreado.  
  
    ```  
    Module shadowByScope  
        ' The following statement declares num as a module-level variable.  
        Public num As Integer  
        Sub show()  
            ' The following statement declares num as a local variable.  
            Dim num As Integer  
            ' The following statement sets the value of the local variable.  
            num = 2  
            ' The following statement displays the module-level variable.  
            MsgBox(CStr(shadowByScope.num))  
        End Sub  
        Sub useModuleLevelNum()  
            ' The following statement sets the value of the module-level variable.  
            num = 1  
            show()  
        End Sub  
    End Module  
    ```  
  
     El ejemplo anterior declara la variable `num` tanto a nivel de módulo en el nivel de procedimiento (en el procedimiento `show`). La variable local `num` oculta o prevalece sobre la variable de nivel de módulo `num` en `show`, por lo que la variable local se establece en 2. Sin embargo, no hay ninguna variable local para instantáneas `num` en el `useModuleLevelNum` procedimiento. Por lo tanto, `useModuleLevelNum` establece el valor de la variable de nivel de módulo en 1.  
  
     El `MsgBox` volat `show` omite el mecanismo de sombreado calificando `num` con el nombre del módulo. Por lo tanto, muestra la variable de nivel de módulo en lugar de la variable local.  
  
#### <a name="to-hide-a-variable-by-shadowing-it-through-inheritance"></a>Para ocultar una variable por él sombreado por herencia  
  
1. Asegúrese de que la variable que desea ocultar está declarada en una clase y en el nivel de clase (fuera de cualquier procedimiento). En caso contrario, no puede prevalecer mediante herencia.  
  
2. Defina una clase derivada de la clase de la variable si no existe.  
  
3. Dentro de la clase derivada, escribe un `Dim` instrucción declara la variable. Incluir el [sombras](../../../../visual-basic/language-reference/modifiers/shadows.md) palabra clave en la declaración.  
  
     Cuando el código de la clase derivada hace referencia al nombre de variable, el compilador resuelve la referencia a la variable.  
  
     El ejemplo siguiente ilustra el sombreado por herencia. Hace que dos referencias, uno que tiene acceso a la variable de sombreado y otro que omite el sombreado.  
  
    ```  
    Public Class shadowBaseClass  
        Public shadowString As String = "This is the base class string."  
    End Class  
    Public Class shadowDerivedClass  
        Inherits shadowBaseClass  
        Public Shadows shadowString As String = "This is the derived class string."  
        Public Sub showStrings()  
            Dim s As String = "Unqualified shadowString: " & shadowString &  
                 vbCrLf & "MyBase.shadowString: " & MyBase.shadowString  
            MsgBox(s)  
        End Sub  
    End Class  
    ```  
  
     El ejemplo anterior declara la variable `shadowString` en la clase base y lo reemplaza en la clase derivada. El procedimiento `showStrings` en la clase derivada, muestra la versión de sombreado de la cadena cuando el nombre `shadowString` no está calificado. A continuación, muestra la versión sombreada cuando `shadowString` se califica con el `MyBase` palabra clave.  
  
## <a name="robust-programming"></a>Programación sólida  
 El sombreado presenta más de una versión de una variable con el mismo nombre. Cuando una instrucción de código hace referencia al nombre de variable, la versión a la que el compilador resuelve la referencia depende de factores como la ubicación de la instrucción de código y la presencia de una cadena de calificación. Esto puede aumentar el riesgo de que hace referencia a una versión no deseada de una variable sombreada. Puede reducir este riesgo si califica completamente todas las referencias a una variable sombreada.  
  
## <a name="see-also"></a>Vea también

- [References to Declared Elements](../../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)
- [Sombrear en Visual Basic](../../../../visual-basic/programming-guide/language-features/declared-elements/shadowing.md)
- [Diferencias entre sombrear y reemplazar](../../../../visual-basic/programming-guide/language-features/declared-elements/differences-between-shadowing-and-overriding.md)
- [Filtrar para ocultar una variable heredada](../../../../visual-basic/programming-guide/language-features/declared-elements/how-to-hide-an-inherited-variable.md)
- [Filtrar para obtener acceso a una variable que se encuentra oculta por una clase derivada](../../../../visual-basic/programming-guide/language-features/declared-elements/how-to-access-a-variable-hidden-by-a-derived-class.md)
- [Overrides](../../../../visual-basic/language-reference/modifiers/overrides.md)
- [Me, My, MyBase y MyClass](../../../../visual-basic/programming-guide/program-structure/me-my-mybase-and-myclass.md)
- [Fundamentos de la herencia](../../../../visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics.md)
