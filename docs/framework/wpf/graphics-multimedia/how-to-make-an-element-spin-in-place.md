---
title: Procedimiento Hacer que un elemento gire en su posición
ms.date: 03/30/2017
helpviewer_keywords:
- graphics [WPF], spinning elements
- spinning elements [WPF]
ms.assetid: 1f011976-8b07-4c31-9faf-019e0ddaa24c
ms.openlocfilehash: aca9bd577f2882e31e8d49abe5eeb5ade86f95f7
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59110669"
---
# <a name="how-to-make-an-element-spin-in-place"></a>Procedimiento Hacer que un elemento gire en su posición
En este ejemplo se muestra cómo hacer que un elemento gire mediante el uso de un <xref:System.Windows.Media.RotateTransform> y un <xref:System.Windows.Media.Animation.DoubleAnimation>.  
  
 El ejemplo siguiente se aplica el <xref:System.Windows.Media.RotateTransform> a la <xref:System.Windows.UIElement.RenderTransform%2A> propiedad del elemento. El ejemplo se usa un <xref:System.Windows.Media.Animation.DoubleAnimation> para animar la <xref:System.Windows.Media.RotateTransform.Angle%2A> de la <xref:System.Windows.Media.RotateTransform>. Para hacer que el elemento gire en su lugar, el ejemplo establece la <xref:System.Windows.UIElement.RenderTransformOrigin%2A> propiedad del elemento en el punto (0,5, 0,5).  
  
## <a name="example"></a>Ejemplo  
 [!code-xaml[transformanimations_snip#11](~/samples/snippets/xaml/VS_Snippets_Wpf/transformanimations_snip/XAML/RotateAboutCenterExample.xaml#11)]  
  
 Para el ejemplo completo, que incluye más ejemplos de transformaciones, vea [ejemplo de transformaciones 2D](https://go.microsoft.com/fwlink/?LinkID=158252).  
  
## <a name="see-also"></a>Vea también

- [Información general sobre animaciones](animation-overview.md)
- [Información general sobre transformaciones](transforms-overview.md)
