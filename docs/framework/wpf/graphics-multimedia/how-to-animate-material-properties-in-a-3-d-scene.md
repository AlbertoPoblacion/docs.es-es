---
title: Procedimiento Animar propiedades de material en una escena 3D
ms.date: 03/30/2017
helpviewer_keywords:
- Material properties [WPF], animating in 3-D scenes
- animation [WPF], Material properties in 3-D scenes
- 3-D scenes [WPF], animating Material properties
ms.assetid: 229fd6eb-7401-4992-b0c9-8b28de230c0f
ms.openlocfilehash: 58e880a2828d21ee76f7fac6bdcf313e8454e65b
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61789329"
---
# <a name="how-to-animate-material-properties-in-a-3-d-scene"></a>Procedimiento Animar propiedades de material en una escena 3D
En este ejemplo se muestra cómo animar la <xref:System.Windows.Media.Brush.Opacity%2A> propiedad de la <xref:System.Windows.Media.Media3D.Material> aplicado a un [!INCLUDE[TLA#tla_3d](../../../../includes/tlasharptla-3d-md.md)] modelo.  
  
 En el ejemplo de código siguiente se define la <xref:System.Windows.Media.LinearGradientBrush> usa como el <xref:System.Windows.Media.Media3D.Material> aplicado al objeto 3D.  
  
 [!code-xaml[Animation3DGallery_snip#AnimateMaterialExampleInline1](~/samples/snippets/csharp/VS_Snippets_Wpf/Animation3DGallery_snip/CS/AnimateMaterialExample.xaml#animatematerialexampleinline1)]  
  
 El <xref:System.Windows.Media.Brush.Opacity%2A> propiedad de este <xref:System.Windows.Media.LinearGradientBrush> se anima mediante el ejemplo de código siguiente.  
  
 [!code-xaml[Animation3DGallery_snip#AnimateMaterialExampleInline2](~/samples/snippets/csharp/VS_Snippets_Wpf/Animation3DGallery_snip/CS/AnimateMaterialExample.xaml#animatematerialexampleinline2)]  
  
## <a name="example"></a>Ejemplo  
 El código siguiente muestra el ejemplo completo.  
  
 [!code-xaml[Animation3DGallery_snip#AnimateMaterialExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/Animation3DGallery_snip/CS/AnimateMaterialExample.xaml#animatematerialexamplewholepage)]  
  
## <a name="see-also"></a>Vea también

- [Crear una escena 3D](how-to-create-a-3-d-scene.md)
- [Información general sobre gráficos 3D](3-d-graphics-overview.md)
