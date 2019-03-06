---
title: Filtrar Usar el corrector ortográfico con un menú contextual
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- enabling spell checking in a text box [WPF]
- reenabling spell checking in a text box [WPF]
- spell checking with a context menu [WPF]
ms.assetid: 61f69a20-2ff3-4056-9060-e32f4483ec5e
ms.openlocfilehash: 38d41aa6710fd13ffd2a5d13a6900a1a05303f35
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/05/2019
ms.locfileid: "57377812"
---
# <a name="how-to-use-spell-checking-with-a-context-menu"></a>Procedimiento Usar el corrector ortográfico con un menú contextual
De forma predeterminada, cuando se habilita el corrector ortográfico en un control de edición como <xref:System.Windows.Controls.TextBox> o <xref:System.Windows.Controls.RichTextBox>, obtendrá las opciones de corrector ortográfico en el menú contextual. Por ejemplo, cuando los usuarios, haga clic en una palabra mal escrita, obtener un conjunto de sugerencias de ortografía o la opción de **omitir todas**. Sin embargo, cuando se reemplaza el menú contextual de forma predeterminada con su propio menú contextual personalizado, esta funcionalidad se pierde y necesita escribir código para volver a habilitar la característica de corrector ortográfico en el menú contextual. En el ejemplo siguiente se muestra cómo habilitar esto en un <xref:System.Windows.Controls.TextBox>.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente se muestra el [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] que crea un <xref:System.Windows.Controls.TextBox> con algunos eventos que se usan para implementar el menú contextual.  
  
 [!code-xaml[TextBoxMiscSnippets_snip#SpellerCustomContextMenuExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/TextBoxMiscSnippets_snip/csharp/speller_custom_context_menu.xaml#spellercustomcontextmenuexamplewholepage)]  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente muestra el código que implementa el menú contextual.  
  
 [!code-csharp[TextBoxMiscSnippets_snip#SpellerCustomContextMenuCodeExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/TextBoxMiscSnippets_snip/csharp/speller_custom_context_menu.xaml.cs#spellercustomcontextmenucodeexamplewholepage)]
 [!code-vb[TextBoxMiscSnippets_snip#SpellerCustomContextMenuCodeExampleWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TextBoxMiscSnippets_snip/visualbasic/speller_custom_context_menu.xaml.vb#spellercustomcontextmenucodeexamplewholepage)]  
  
 El código que se usa para hacer esto con un <xref:System.Windows.Controls.RichTextBox> es similar. La diferencia principal radica en el parámetro pasado a la `GetSpellingError` método. Para un <xref:System.Windows.Controls.TextBox>, pase el índice de entero de la posición del símbolo de intercalación:  
  
 `spellingError = myTextBox.GetSpellingError(caretIndex);`  
  
 Para un <xref:System.Windows.Controls.RichTextBox>, pase el <xref:System.Windows.Documents.TextPointer> que especifica la posición del símbolo de intercalación:  
  
 `spellingError = myRichTextBox.GetSpellingError(myRichTextBox.CaretPosition);`  
  
## <a name="see-also"></a>Vea también
- [Información general sobre TextBox](textbox-overview.md)
- [RichTextBox Overview](richtextbox-overview.md) (Introducción a RichTextBox)
- [Habilitar el corrector ortográfico en un control de edición de texto](how-to-enable-spell-checking-in-a-text-editing-control.md)
- [Usar un menú contextual personalizado con un control TextBox](how-to-use-a-custom-context-menu-with-a-textbox.md)
