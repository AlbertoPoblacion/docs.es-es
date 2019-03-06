---
title: Filtrar Obtener una colección de líneas de un control TextBox
ms.date: 03/30/2017
helpviewer_keywords:
- lines [WPF], getting collection of
- TextBox control [WPF], getting collection of lines
ms.assetid: a12f529d-b926-47f6-92bf-cad5f17b532a
ms.openlocfilehash: 1aa73e55a3fdfd658c6a337b598dff96244ace40
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/05/2019
ms.locfileid: "57354198"
---
# <a name="how-to-get-a-collection-of-lines-from-a-textbox"></a>Procedimiento Obtener una colección de líneas de un control TextBox
En este ejemplo se muestra cómo obtener una colección de líneas de texto de un <xref:System.Windows.Controls.TextBox>.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente muestra un método simple que toma un <xref:System.Windows.Controls.TextBox> como argumento y devuelve un <xref:System.Collections.Specialized.StringCollection> que contiene las líneas de texto en el **TextBox**.  El <xref:System.Windows.Controls.TextBox.LineCount%2A> propiedad se utiliza para determinar cuántas líneas están actualmente en el **TextBox**y el <xref:System.Windows.Controls.TextBox.GetLineText%2A> método, a continuación, se usa para extraer cada línea y agregarla a la colección de líneas.  
  
 [!code-csharp[TextBox_MiscCode#_TextBox_GetLines](~/samples/snippets/csharp/VS_Snippets_Wpf/TextBox_MiscCode/CSharp/Window1.xaml.cs#_textbox_getlines)]  
  
## <a name="see-also"></a>Vea también
- [Información general sobre TextBox](textbox-overview.md)
- [RichTextBox Overview](richtextbox-overview.md) (Introducción a RichTextBox)
