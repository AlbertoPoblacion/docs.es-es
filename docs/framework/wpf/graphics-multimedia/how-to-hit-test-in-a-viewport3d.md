---
title: Procedimiento Hacer una prueba de posicionamiento en Viewport3D
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- 3-D visuals [WPF], hit-testing for
- hit tests [WPF], for 3-D visuals
- Viewport3D [WPF]
ms.assetid: 42bfbd99-c7c6-43f1-940b-90448faa412e
ms.openlocfilehash: d795f5aa768c360b6e27a9a1114179a5c27f0b23
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/05/2019
ms.locfileid: "57356577"
---
# <a name="how-to-hit-test-in-a-viewport3d"></a>Filtrar Hacer una prueba de posicionamiento en Viewport3D
En este ejemplo se muestra cómo la objetos visuales 3D de prueba de posicionamiento un <xref:System.Windows.Controls.Viewport3D>.  
  
 Dado que <xref:System.Windows.Media.VisualTreeHelper.HitTest%2A> devuelve información de 2D y 3D, es posible recorrer en iteración los resultados de pruebas para leer los resultados solo 3D.  
  
 [!code-csharp[HitTest3D#HitTest3D3DN4](~/samples/snippets/csharp/VS_Snippets_Wpf/HitTest3D/CSharp/Window1.xaml.cs#hittest3d3dn4)]
 [!code-vb[HitTest3D#HitTest3D3DN4](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HitTest3D/visualbasic/window1.xaml.vb#hittest3d3dn4)]  
  
 El <xref:System.Windows.Media.HitTestResultBehavior> en el código siguiente determina cómo se procesan los resultados de prueba de posicionamiento.  `UpdateResultInfo` y `UpdateMaterial` son métodos definidos localmente.  
  
 [!code-csharp[HitTest3D#HitTest3D3DN5](~/samples/snippets/csharp/VS_Snippets_Wpf/HitTest3D/CSharp/Window1.xaml.cs#hittest3d3dn5)]
 [!code-vb[HitTest3D#HitTest3D3DN5](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HitTest3D/visualbasic/window1.xaml.vb#hittest3d3dn5)]  
  
## <a name="see-also"></a>Vea también
- [Ejemplo de pruebas de posicionamiento de 3D](https://go.microsoft.com/fwlink/?LinkID=159959)
