---
title: El espacio de nombres o tipo especificado en las importaciones '<qualifiedelementname>' no contiene miembros públicos o no se encuentra
ms.date: 07/20/2015
f1_keywords:
- bc40056
- vbc40056
helpviewer_keywords:
- BC40056
ms.assetid: b59f5754-444f-4378-9272-9678b437e84a
ms.openlocfilehash: 1873c0af7a251afd7754557f5dcb6aed13eb9f11
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/05/2019
ms.locfileid: "57357890"
---
# <a name="namespace-or-type-specified-in-the-imports-qualifiedelementname-doesnt-contain-any-public-member-or-cannot-be-found"></a>Namespace o tipo especificado en las importaciones\<nombrecompletoelemento >' no contiene ningún miembro público o no se encuentra

Namespace o tipo especificado en las importaciones\<nombrecompletoelemento >' no contiene ningún miembro público o no se encuentra. Asegúrese de que el espacio de nombres o el tipo se define y contiene a al menos un miembro público. Asegúrese de que el nombre de alias no contiene otros alias.

Un `Imports` instrucción especifica un elemento contenedor que no se puede encontrar o no define `Public` miembros.

Un *que contiene el elemento* puede ser el espacio de nombres, clase, estructura, módulo, interfaz o enumeración. El elemento contenedor contiene a miembros, como variables, procedimientos u otros elementos que lo contiene.

El propósito de la importación es permitir que el código para obtener acceso a los miembros de tipo o espacio de nombres sin tener que calificarlos. También podría necesitar el proyecto agregar una referencia al espacio de nombres o tipo. Para obtener más información, vea "Importar elementos contenedores" en [References to Declared Elements](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md).

Si el compilador no encuentra el elemento contenedor especificado, no se puede resolver las referencias que lo usan. Si encuentra el elemento, pero el elemento no exponen ninguno `Public` miembros, ninguna referencia puede ser correcta. En cualquier caso, tiene sentido para importar el elemento.

Tenga en cuenta que si importa un elemento contenedor y asignarle un alias de importación, a continuación, no se puede usar ese alias de importación para importar otro elemento. El código siguiente genera un error del compilador.

```vb
Imports winfrm = System.Windows.Forms

' The following statement is INVALID  because it reuses an import alias.

Imports behave = winfrm.Design.Behavior`
```

**Identificador de error:** BC40056

## <a name="to-correct-this-error"></a>Para corregir este error

1. Compruebe que el elemento contenedor es accesible desde el proyecto.

2. Compruebe que la especificación del elemento contenedor no incluye ningún alias de importación desde otra importación.

3. Compruebe que el elemento contenedor expone al menos una `Public` miembro.

## <a name="see-also"></a>Vea también

- [Imports (instrucción), espacio de nombres y tipo .NET](../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)
- [Namespace (instrucción)](../../../visual-basic/language-reference/statements/namespace-statement.md)
- [Public](../../../visual-basic/language-reference/modifiers/public.md)
- [Espacios de nombres en Visual Basic](../../../visual-basic/programming-guide/program-structure/namespaces.md)
- [Referencias a elementos declarados](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)
