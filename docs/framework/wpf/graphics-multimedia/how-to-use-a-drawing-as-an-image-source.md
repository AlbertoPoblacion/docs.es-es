---
title: Procedimiento Usar un dibujo como el origen de una imagen
ms.date: 03/30/2017
helpviewer_keywords:
- graphics [WPF], drawings [WPF], as image sources
- image sources [WPF], drawings
- drawings [WPF], as image sources
ms.assetid: dcf71c7b-9e86-4b8e-8e39-0d0ce0389ef4
ms.openlocfilehash: d4b91a6495e1c54400d5fbfe43b6311d908565a7
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59097865"
---
# <a name="how-to-use-a-drawing-as-an-image-source"></a>Procedimiento Usar un dibujo como el origen de una imagen
En este ejemplo se muestra cómo usar un <xref:System.Windows.Media.Drawing> como el <xref:System.Windows.Controls.Image.Source%2A> para un <xref:System.Windows.Controls.Image> control. Para mostrar un <xref:System.Windows.Media.Drawing> con un <xref:System.Windows.Controls.Image> controlar, use un <xref:System.Windows.Media.DrawingImage> como el <xref:System.Windows.Controls.Image> del control <xref:System.Windows.Controls.Image.Source%2A> y establezca el <xref:System.Windows.Media.DrawingImage> del objeto <xref:System.Windows.Media.DrawingImage.Drawing%2A?displayProperty=nameWithType> propiedad para el dibujo que desea mostrar.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se usa un <xref:System.Windows.Media.DrawingImage> y un <xref:System.Windows.Controls.Image> control para mostrar un <xref:System.Windows.Media.GeometryDrawing>. Este ejemplo produce el siguiente resultado:  
  
 ![GeometryDrawing de dos elipses](./media/graphicsmm-geodraw.jpg "graphicsmm_geodraw")  
DrawingImage  
  
 [!code-csharp[DrawingMiscSnippets_snip#DrawingImageExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/DrawingImageExample.cs#drawingimageexamplewholepage)]
 [!code-xaml[DrawingMiscSnippets_snip#DrawingImageExampleWholePage](~/samples/snippets/xaml/VS_Snippets_Wpf/DrawingMiscSnippets_snip/XAML/DrawingImageExample.xaml#drawingimageexamplewholepage)]  
  
## <a name="see-also"></a>Vea también

- <xref:System.Windows.Freezable.Freeze%2A>
- [Dibujar una imagen usando un objeto ImageDrawing](how-to-draw-an-image-using-imagedrawing.md)
- [Información general sobre objetos Drawing](drawing-objects-overview.md)
- [Información general sobre objetos Freezable](../advanced/freezable-objects-overview.md)
- [PresentationOptions:Freeze (Atributo)](../advanced/presentationoptions-freeze-attribute.md)
