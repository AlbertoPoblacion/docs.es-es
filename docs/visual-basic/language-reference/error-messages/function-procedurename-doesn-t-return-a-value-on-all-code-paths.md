---
title: La función '<procedurename>' no devuelve un valor en todas las rutas de acceso a código
ms.date: 07/20/2015
f1_keywords:
- bc42105
- vbc42105
helpviewer_keywords:
- BC42105
ms.assetid: b6929bf4-a365-4a70-8dc9-6b0fc09e1468
ms.openlocfilehash: badcfea4f24ba3858071e02ba47b8f77ab557f88
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "58824837"
---
# <a name="function-procedurename-doesnt-return-a-value-on-all-code-paths"></a>Función '\<NombreDeProcedimiento >' no devuelve un valor en todas las rutas de código
Función '\<NombreDeProcedimiento >' no devuelve un valor en todas las rutas de código. ¿Falta alguna instrucción 'Return'?  
  
 Un `Function` procedimiento tiene al menos una ruta de acceso posibles a través de su código que no devuelve un valor.  
  
 Puede devolver un valor desde un `Function` procedimiento en cualquiera de las maneras siguientes:  
  
-   Incluya el valor en un [instrucción Return](../../../visual-basic/language-reference/statements/return-statement.md).  
  
-   Asigne el valor para el `Function` procedimiento asigne un nombre y, a continuación, realizar un `Exit Function` instrucción.  
  
-   Asigne el valor para el `Function` procedimiento asigne un nombre y, a continuación, realizar el `End Function` instrucción.  
  
 Si el control se transfiere a `Exit Function` o `End Function` y no ha asignado ningún valor para el nombre del procedimiento, el procedimiento devuelve el valor predeterminado del tipo de datos devuelto. Para obtener más información, vea "Comportamiento" en [instrucción Function](../../../visual-basic/language-reference/statements/function-statement.md).  
  
 De forma predeterminada, este mensaje es una advertencia. Para obtener más información sobre cómo ocultar las advertencias o cómo tratarlas como errores, vea [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic).  
  
 **Identificador de error:** BC42105  
  
## <a name="to-correct-this-error"></a>Para corregir este error  
  
-   Compruebe la lógica del flujo de control y asegúrese de que asignar un valor antes de cada instrucción que genera un valor devuelto.  
  
     Es más fácil garantizar que todos los valores devueltos desde el procedimiento devuelve un valor si siempre usa el `Return` instrucción. Si lo hace, la última instrucción antes de `End Function` debe ser un `Return` instrucción.  
  
## <a name="see-also"></a>Vea también

- [Procedimientos de función](../../../visual-basic/programming-guide/language-features/procedures/function-procedures.md)
- [Function (instrucción)](../../../visual-basic/language-reference/statements/function-statement.md)
- [Página Compilación, Diseñador de proyectos (Visual Basic)](/visualstudio/ide/reference/compile-page-project-designer-visual-basic)
