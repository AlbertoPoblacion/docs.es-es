---
title: Filtrar Utilizar la clase FontSizeConverter
ms.date: 03/30/2017
helpviewer_keywords:
- FontSizeConverter objects [WPF]
- typography [WPF], FontSizeConverter objects
ms.assetid: 3b0592bd-7223-4860-a108-a5d72f3a9178
ms.openlocfilehash: 21050ae69ad834b56c70f40d85138714af334dab
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/05/2019
ms.locfileid: "57364104"
---
# <a name="how-to-use-the-fontsizeconverter-class"></a>Procedimiento Utilizar la clase FontSizeConverter
## <a name="example"></a>Ejemplo  
 En este ejemplo se muestra cómo crear una instancia de <xref:System.Windows.FontSizeConverter> y usarlo para cambiar el tamaño de fuente.  
  
 El ejemplo define un método personalizado llamado `changeSize` que convierte el contenido de un <xref:System.Windows.Controls.ListBoxItem>, tal como se define en otro [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] archivo a una instancia de <xref:System.Double>y versiones posteriores en un <xref:System.String>. Este método pasa el <xref:System.Windows.Controls.ListBoxItem> a un <xref:System.Windows.FontSizeConverter> objeto, que convierte el <xref:System.Windows.Controls.ContentControl.Content%2A> de un <xref:System.Windows.Controls.ListBoxItem> a una instancia de <xref:System.Double>. Este valor, a continuación, se pasa como el valor de la <xref:System.Windows.Controls.TextBlock.FontSize%2A> propiedad de la <xref:System.Windows.Controls.TextBlock> elemento.  
  
 En este ejemplo también define un segundo método personalizado que se denomina `changeFamily`. Este método convierte el <xref:System.Windows.Controls.ContentControl.Content%2A> de la <xref:System.Windows.Controls.ListBoxItem> a un <xref:System.String>y, a continuación, pasa ese valor a la <xref:System.Windows.Controls.TextBlock.FontFamily%2A> propiedad de la <xref:System.Windows.Controls.TextBlock> elemento.  
  
 En este ejemplo no se ejecuta.  
  
 [!code-csharp[FontSizeConverter#1](~/samples/snippets/csharp/VS_Snippets_Wpf/FontSizeConverter/CSharp/Window1.xaml.cs#1)]  
  
## <a name="see-also"></a>Vea también
- <xref:System.Windows.FontSizeConverter>
