---
title: Filtrar Animar un objeto a lo largo de un trazado (animación en matriz con acumulación de desplazamiento)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- offset accumulation [WPF]
- animation [WPF], objects along paths (matrix animation with offset accumulation)
- matrix animation with offset accumulation [WPF]
ms.assetid: 1bca90ef-9832-4128-8ed6-62908e7ec146
ms.openlocfilehash: 859a3556bc29d2b30572be03708ebab80ce692fb
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/05/2019
ms.locfileid: "57351609"
---
# <a name="how-to-animate-an-object-along-a-path-matrix-animation-with-offset-accumulation"></a>Filtrar Animar un objeto a lo largo de un trazado (animación en matriz con acumulación de desplazamiento)
En este ejemplo se muestra cómo usar el <xref:System.Windows.Media.Animation.MatrixAnimationUsingPath> clase para animar un objeto a lo largo de una ruta de acceso y hacer que dicha animación su desplazamiento se acumulan los valores de medida que se repite.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se usa el <xref:System.Windows.Media.Animation.MatrixAnimationUsingPath> objeto que se va a animar el <xref:System.Windows.Media.MatrixTransform.Matrix%2A> propiedad de un <xref:System.Windows.Media.MatrixTransform> aplicada a un botón. Como resultado, un botón se mueve a lo largo de un trazado curvo.  
  
 Además, el ejemplo establece la <xref:System.Windows.Media.Animation.MatrixAnimationUsingPath.IsOffsetCumulative%2A> propiedad `true`, lo que hace que el desplazamiento de la matriz animada se acumulen como la animación se repite. Dado que el desplazamiento se acumula, el botón se aleja por la pantalla cuando se repite la animación, en lugar de restablecerse a la posición inicial.  
  
 [!code-xaml[PathAnimationGallery_snippet#MatrixAnimationUsingPathOffsetCumulativeWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/PathAnimationGallery_snippet/CS/matrixanimationusingpathexampleoffsetcumulative.xaml#matrixanimationusingpathoffsetcumulativewholepage)]  
  
 [!code-csharp[PathAnimationGallery_procedural_snip#MatrixAnimationUsingPathOffsetCumulativeWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/PathAnimationGallery_procedural_snip/CSharp/MatrixAnimationUsingPathExampleOffsetCumulative.cs#matrixanimationusingpathoffsetcumulativewholepage)]
 [!code-vb[PathAnimationGallery_procedural_snip#MatrixAnimationUsingPathOffsetCumulativeWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PathAnimationGallery_procedural_snip/VisualBasic/MatrixAnimationUsingPathExampleOffsetCumulative.vb#matrixanimationusingpathoffsetcumulativewholepage)]  
  
 Tenga en cuenta que, aunque el <xref:System.Windows.Media.Animation.MatrixAnimationUsingPath.IsOffsetCumulative%2A> propiedad hace que los valores de desplazamiento se acumulen con repeticiones, no hace que los valores de rotación se acumulen. Para que los valores de rotación se acumulen, establezca la animación <xref:System.Windows.Media.Animation.MatrixAnimationUsingPath.DoesRotateWithTangent%2A> y <xref:System.Windows.Media.Animation.MatrixAnimationUsingPath.IsAngleCumulative%2A> propiedades a `true`.  
  
 Para obtener un ejemplo completo, vea [ejemplo de animación de trazado](https://go.microsoft.com/fwlink/?LinkID=160028). Para obtener un ejemplo que muestra cómo animar una <xref:System.Windows.Media.Matrix> a lo largo de un trazado sin acumulación de desplazamiento de valor, vea [animar un objeto a lo largo de un trazado (animación en matriz)](how-to-animate-an-object-along-a-path-matrix-animation.md).  
  
## <a name="see-also"></a>Vea también
- [Información general sobre animaciones](animation-overview.md)
- [Temas de procedimientos de animación de trazado](path-animation-how-to-topics.md)
