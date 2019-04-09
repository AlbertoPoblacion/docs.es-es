---
title: Filtrar Controlar una animación mediante From, To y By
ms.date: 03/30/2017
helpviewer_keywords:
- animation [WPF], From/to/by
- basic animation [WPF]
- animation [WPF], basic animation
- From/to/by animation
ms.assetid: 59afba57-6fc1-44c8-987e-8a5f4142adad
ms.openlocfilehash: 56522ee5bd4391e43c261558b2fa622234c9ea3b
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2019
ms.locfileid: "59073277"
---
# <a name="how-to-control-an-animation-using-from-to-and-by"></a>Filtrar Controlar una animación mediante From, To y By
Un "From/To/By" o "animación básica" crea una transición entre dos valores de destino (consulte [información general sobre animaciones](animation-overview.md) para obtener una introducción a distintos tipos de animaciones). Para establecer los valores de destino de una animación básica, use su <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A>, <xref:System.Windows.Media.Animation.DoubleAnimation.To%2A>, y <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A> propiedades.  La tabla siguiente resume cómo el <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A>, <xref:System.Windows.Media.Animation.DoubleAnimation.To%2A>, y <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A> propiedades pueden usarse conjuntamente o por separado los valores determinar el destino de una animación.  
  
|Propiedades especificadas|Comportamiento resultante|  
|--------------------------|------------------------|  
|<xref:System.Windows.Media.Animation.DoubleAnimation.From%2A>|La animación progresa desde el valor especificado por el <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> propiedad al valor base de la propiedad que se anima o hasta una animación previa de salida de valor, según cómo esté configurada la animación anterior.|  
|<xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> y <xref:System.Windows.Media.Animation.DoubleAnimation.To%2A>|La animación progresa desde el valor especificado por el <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> propiedad en el valor especificado por el <xref:System.Windows.Media.Animation.DoubleAnimation.To%2A> propiedad.|  
|<xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> y <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A>|La animación progresa desde el valor especificado por el <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> propiedad en el valor especificado por la suma de los <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> y <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A> propiedades.|  
|<xref:System.Windows.Media.Animation.DoubleAnimation.To%2A>|La animación progresa desde el valor base de la propiedad animada o de salida de una animación previa del valor en el valor especificado por el <xref:System.Windows.Media.Animation.DoubleAnimation.To%2A> propiedad.|  
|<xref:System.Windows.Media.Animation.DoubleAnimation.By%2A>|La animación progresa desde el valor base de la propiedad que se anima o una animación previa del valor de salida a la suma de ese valor y el valor especificado por el <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A> propiedad.|  
  
> [!NOTE]
>  No establezca la <xref:System.Windows.Media.Animation.DoubleAnimation.To%2A> propiedad y el <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A> propiedad en la misma animación.  
  
 Para usar otros métodos de interpolación o animar entre más de dos valores de destino, use una animación de fotogramas clave. Consulte [información general sobre animaciones de fotogramas clave](key-frame-animations-overview.md) para obtener más información.  
  
 Para obtener información acerca de cómo aplicar varias animaciones a una sola propiedad, vea [información general sobre animaciones de fotogramas clave](key-frame-animations-overview.md).  
  
 El ejemplo siguiente muestra los efectos diferentes de configuración <xref:System.Windows.Media.Animation.DoubleAnimation.To%2A>, <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A>, y <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> las propiedades de las animaciones.  
  
## <a name="example"></a>Ejemplo  
 [!code-xaml[BasicAnimations_snippet#AnimationTargetValuesWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/BasicAnimations_snippet/CS/AnimationTargetValuesExample.xaml#animationtargetvalueswholepage)]  
  
## <a name="see-also"></a>Vea también

- [Información general sobre animaciones](animation-overview.md)
- [Información general sobre animaciones de fotogramas clave](key-frame-animations-overview.md)
- [FROM, To y por el ejemplo de valores de destino de animación](https://go.microsoft.com/fwlink/?LinkID=159988)
