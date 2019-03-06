---
title: Procedimiento Colocar el cursor al principio o al final del texto de un control
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- positioning cursor [WPF]
- TextBox control [WPF], positioning cursor
- cursor [WPF], positioning
ms.assetid: c771a0b8-c6b4-4240-aecd-a21d0ba51a2e
ms.openlocfilehash: e4058518e4eb56e1cd9d5fdafd792d8f8d3b77ab
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/05/2019
ms.locfileid: "57367848"
---
# <a name="how-to-position-the-cursor-at-the-beginning-or-end-of-text-in-a-textbox-control"></a>Filtrar Colocar el cursor al principio o al final del texto de un control
En este ejemplo se muestra cómo colocar el cursor al principio o al final del contenido de texto de un <xref:System.Windows.Controls.TextBox> control.  
  
## <a name="example"></a>Ejemplo  
 La siguiente [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] código describe una <xref:System.Windows.Controls.TextBox> controlar y le asigna un nombre.  
  
 [!code-xaml[TextBox_MiscCode#_MoveCursorXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/TextBox_MiscCode/CSharp/Window1.xaml#_movecursorxaml)]  
  
## <a name="example"></a>Ejemplo  
 Para colocar el cursor al principio del contenido de un <xref:System.Windows.Controls.TextBox> control, llame a la <xref:System.Windows.Controls.TextBox.Select%2A> método y especificar la selección de inicio la posición 0 y una longitud de selección de 0.  
  
 [!code-csharp[TextBox_MiscCode#_CursorToStart](~/samples/snippets/csharp/VS_Snippets_Wpf/TextBox_MiscCode/CSharp/Window1.xaml.cs#_cursortostart)]
 [!code-vb[TextBox_MiscCode#_CursorToStart](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TextBox_MiscCode/VisualBasic/Window1.xaml.vb#_cursortostart)]  
  
## <a name="example"></a>Ejemplo  
 Para colocar el cursor al final del contenido de un <xref:System.Windows.Controls.TextBox> control, llame a la <xref:System.Windows.Controls.TextBox.Select%2A> método y especificar la posición inicial igual a la longitud del contenido de texto y una longitud de selección de 0.  
  
 [!code-csharp[TextBox_MiscCode#_CursorToEnd](~/samples/snippets/csharp/VS_Snippets_Wpf/TextBox_MiscCode/CSharp/Window1.xaml.cs#_cursortoend)]
 [!code-vb[TextBox_MiscCode#_CursorToEnd](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TextBox_MiscCode/VisualBasic/Window1.xaml.vb#_cursortoend)]  
  
## <a name="see-also"></a>Vea también
- [Información general sobre TextBox](textbox-overview.md)
- [RichTextBox Overview](richtextbox-overview.md) (Introducción a RichTextBox)
