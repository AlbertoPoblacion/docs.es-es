---
title: '&lt;proceduresignature1&gt; no es conforme a CLS porque sobrecarga &lt;proceduresignature2&gt; que difiere de él en la matriz de tipos de parámetro de matriz o en el rango de los tipos de parámetro de matriz'
ms.date: 07/20/2015
f1_keywords:
- vbc40035
- bc40035
helpviewer_keywords:
- BC40035
ms.assetid: 50a66dbe-2c1e-41bf-96bc-369301c891ac
ms.openlocfilehash: 0f4eaa09c3d04af350637fba0d672f55040a6466
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/23/2019
ms.locfileid: "54626854"
---
# <a name="ltproceduresignature1gt-is-not-cls-compliant-because-it-overloads-ltproceduresignature2gt-which-differs-from-it-only-by-array-of-array-parameter-types-or-by-the-rank-of-the-array-parameter-types"></a>&lt;proceduresignature1&gt; no es conforme a CLS porque sobrecarga &lt;proceduresignature2&gt; que difiere de él en la matriz de tipos de parámetro de matriz o en el rango de los tipos de parámetro de matriz
Un procedimiento o propiedad se marca como `<CLSCompliant(True)>` cuando reemplaza otro procedimiento o propiedad y la única diferencia entre sus listas de parámetros es el nivel de anidamiento de una matriz escalonada o el rango de matriz.  
  
 En las declaraciones siguientes, la segunda y tercera declaraciones generan este error.  
  
 `Overloads Sub processArray(ByVal arrayParam() As Integer)`  
  
 `Overloads Sub processArray(ByVal arrayParam()() As Integer)`  
  
 `Overloads Sub processArray(ByVal arrayParam(,) As Integer)`  
  
 La segunda declaración cambia el parámetro unidimensional original `arrayParam` a una matriz de matrices. Los cambios en la terceros declaración `arrayParam` a una matriz bidimensional (rango 2). Aunque Visual Basic permite las sobrecargas que difieren solo en uno de estos cambios, dicha sobrecarga no es compatible con la [independencia del lenguaje y componentes independientes del lenguaje](../../../standard/language-independence-and-language-independent-components.md) (CLS).  
  
 Al aplicar <xref:System.CLSCompliantAttribute> a un elemento de programación, establezca el parámetro `isCompliant` del atributo en `True` o `False` para indicar conformidad o disconformidad. No hay ningún valor predeterminado para este parámetro, por lo que debe proporcionar uno.  
  
 Si no se aplica <xref:System.CLSCompliantAttribute> a un elemento, se considera que no es conforme.  
  
 De forma predeterminada, este mensaje es una advertencia. Para obtener más información sobre cómo ocultar las advertencias o cómo tratarlas como errores, vea [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic).  
  
 **Identificador de error:** BC40035  
  
## <a name="to-correct-this-error"></a>Para corregir este error  
  
-   Si necesita conformidad con CLS, defina sus sobrecargas para difieren entre sí de más formas que solo los cambios indicados en esta página de ayuda.  
  
-   Si necesita que las sobrecargas difieren solo por los cambios indicados en esta Ayuda, página, quite el <xref:System.CLSCompliantAttribute> de sus definiciones o marcarlos como `<CLSCompliant(False)>`.  
  
## <a name="see-also"></a>Vea también

- [Sobrecarga de procedimientos](../../../visual-basic/programming-guide/language-features/procedures/procedure-overloading.md)
- [Sobrecargas](../../../visual-basic/language-reference/modifiers/overloads.md)
