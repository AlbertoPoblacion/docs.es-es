---
title: Procedimiento Utilizar los métodos de desplazamiento de contenido de ScrollViewer
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- IScrollInfo interface [WPF]
- scrolling methods [WPF]
- ScrollViewer control [WPF], scrolling methods
ms.assetid: 4708cc65-6510-45f8-82e6-30b0d3e30045
ms.openlocfilehash: b9da9ca2512a39164f2b3a6f5e98fe63b89f0b9a
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/05/2019
ms.locfileid: "57370012"
---
# <a name="how-to-use-the-content-scrolling-methods-of-scrollviewer"></a>Filtrar Utilizar los métodos de desplazamiento de contenido de ScrollViewer
En este ejemplo se muestra cómo usar los métodos de desplazamiento del <xref:System.Windows.Controls.ScrollViewer> elemento. Estos métodos proporcionan desplazamiento incremental del contenido, de línea o por página, en un <xref:System.Windows.Controls.ScrollViewer>.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se crea un <xref:System.Windows.Controls.ScrollViewer> denominado `sv1`, que hospeda un elemento secundario <xref:System.Windows.Controls.TextBlock> elemento. Dado que el <xref:System.Windows.Controls.TextBlock> es mayor que el elemento primario <xref:System.Windows.Controls.ScrollViewer>, aparecen barras de desplazamiento con el fin de habilitar el desplazamiento. <xref:System.Windows.Controls.Button> los elementos que representan los distintos métodos de desplazamiento se acoplan a la izquierda en otro <xref:System.Windows.Controls.StackPanel>. Cada <xref:System.Windows.Controls.Button> en el [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] archivo llama a un método personalizado relacionado que controla el comportamiento de desplazamiento en <xref:System.Windows.Controls.ScrollViewer>.  
  
 [!code-xaml[ScrollViewerMethods#1](~/samples/snippets/csharp/VS_Snippets_Wpf/ScrollViewerMethods/CSharp/Window1.xaml#1)]  
  
 En el ejemplo siguiente se usa el <xref:System.Windows.Controls.ScrollViewer.LineUp%2A> y <xref:System.Windows.Controls.ScrollViewer.LineDown%2A> métodos.  
  
 [!code-csharp[ScrollViewerMethods#2](~/samples/snippets/csharp/VS_Snippets_Wpf/ScrollViewerMethods/CSharp/Window1.xaml.cs#2)]
 [!code-vb[ScrollViewerMethods#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ScrollViewerMethods/VisualBasic/Window1.xaml.vb#2)]  
  
## <a name="see-also"></a>Vea también
- <xref:System.Windows.Controls.ScrollViewer>
- <xref:System.Windows.Controls.StackPanel>
