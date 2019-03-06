---
title: Procedimiento Pintar un área con un degradado radial
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- brushes [WPF], painting with radial gradients
- radial gradients [WPF], painting with
- painting [WPF], with radial gradients
ms.assetid: b5d0fc8a-8986-4796-b003-a75b41a48928
ms.openlocfilehash: c3bcc11dea4b1f223f629415591ab03588881dde
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/05/2019
ms.locfileid: "57379788"
---
# <a name="how-to-paint-an-area-with-a-radial-gradient"></a>Filtrar Pintar un área con un degradado radial
En este ejemplo se muestra cómo usar el <xref:System.Windows.Media.RadialGradientBrush> clase para pintar un área con un degradado radial.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se usa un <xref:System.Windows.Media.RadialGradientBrush> para pintar un rectángulo con un degradado radial que realiza la transición de amarillo a rojo a azul para verde lima.  
  
 [!code-csharp[BrushesIntroduction_snip#SimpleRadialGradientExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/RadialGradientBrushSnippet.cs#simpleradialgradientexamplewholepage)]
 [!code-vb[BrushesIntroduction_snip#SimpleRadialGradientExampleWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/radialgradientbrushsnippet.vb#simpleradialgradientexamplewholepage)]
 [!code-xaml[BrushesIntroduction_snip#SimpleRadialGradientExampleWholePage](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/RadialGradientBrushSnippet.xaml#simpleradialgradientexamplewholepage)]  
  
 La siguiente ilustración muestra el degradado del ejemplo anterior. Se resaltan los delimitadores de degradado.  
  
 ![Delimitadores de degradado en un degradado radial](./media/wcpsdk-graphicsmm-4gradientstops-rg.png "wcpsdk_graphicsmm_4gradientstops_rg")  
  
> [!NOTE]
>  Los ejemplos de este tema usan el sistema de coordenadas predeterminado para establecer puntos de control. El sistema de coordenadas predeterminado está relacionado con un rectángulo: 0 indica 0 por ciento del rectángulo, y 1 indica un 100 por cien del rectángulo. Puede cambiar este sistema de coordenadas estableciendo el <xref:System.Windows.Media.GradientBrush.MappingMode%2A> valor para la propiedad <xref:System.Windows.Media.BrushMappingMode.Absolute>. Un sistema de coordenadas absoluto no está relacionado con un rectángulo de selección. Los valores se interpretan directamente en el espacio local.  
  
 Para más <xref:System.Windows.Media.RadialGradientBrush> ejemplos, vea el [Brushes Sample](https://go.microsoft.com/fwlink/?LinkID=159973). Para obtener más información acerca de los degradados y otros tipos de pinceles, vea [el dibujo con colores sólidos y degradados](painting-with-solid-colors-and-gradients-overview.md).
