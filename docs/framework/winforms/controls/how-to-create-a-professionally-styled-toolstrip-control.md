---
title: Filtrar Crear un Control ToolStrip de estilo profesional
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- toolbars [Windows Forms]
- ToolStripProfessionalRenderer class [Windows Forms]
- ToolStripRenderer class [Windows Forms]
- ToolStrip control [Windows Forms]
ms.assetid: c208b2f6-8105-474b-9075-d582e1792870
ms.openlocfilehash: 039bdd3907851d1f5e756652dd1b42765606c0c6
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/09/2019
ms.locfileid: "57719291"
---
# <a name="how-to-create-a-professionally-styled-toolstrip-control"></a>Filtrar Crear un Control ToolStrip de estilo profesional
Puede dar a los controles <xref:System.Windows.Forms.ToolStrip> de la aplicación un aspecto y comportamiento profesional escribiendo su propia clase derivada del tipo <xref:System.Windows.Forms.ToolStripProfessionalRenderer>.  
  
 Hay una amplia compatibilidad para esta característica en Visual Studio.  
  
 Vea [Tutorial: Crear un Control ToolStrip de estilo profesional](walkthrough-creating-a-professionally-styled-toolstrip-control.md).  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo de código siguiente se muestra cómo usar <xref:System.Windows.Forms.ToolStrip> controles para crear un control compuesto que imite el **panel de navegación** proporcionado por Microsoft® Outlook®.  
  
 [!code-csharp[System.Windows.Forms.ToolStrip.StackView#1](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/CS/StackView.cs#1)]
 [!code-vb[System.Windows.Forms.ToolStrip.StackView#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/VB/StackView.vb#1)]  
  
## <a name="compiling-the-code"></a>Compilar el código  
 Para este ejemplo se necesita:  
  
-   Referencias a los ensamblados System.Drawing y System.Windows.Forms.  
  
 Para obtener información sobre cómo compilar este ejemplo desde la línea de comandos para Visual Basic o Visual C#, vea [compilar desde la línea de comandos](~/docs/visual-basic/reference/command-line-compiler/building-from-the-command-line.md) o [de línea de comandos con csc.exe](~/docs/csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md). También puede compilar este ejemplo en Visual Studio pegando el código en un nuevo proyecto.  Consulte también [Tutorial: Crear un Control ToolStrip de estilo profesional](walkthrough-creating-a-professionally-styled-toolstrip-control.md).  
  
## <a name="see-also"></a>Vea también
- <xref:System.Windows.Forms.MenuStrip>
- <xref:System.Windows.Forms.ToolStrip>
- <xref:System.Windows.Forms.StatusStrip>
- [Control ToolStrip](toolstrip-control-windows-forms.md)
- [Cómo: Proporcionar elementos de menú estándar a un formulario](how-to-provide-standard-menu-items-to-a-form.md)
