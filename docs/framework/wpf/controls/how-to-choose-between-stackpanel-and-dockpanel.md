---
title: Procedimiento Elegir entre StackPanel y DockPanel
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- controls [WPF], DockPanel
- DockPanel control [WPF], StackPanel control compared to
- StackPanel control [WPF], DockPanel control compared to
- controls [WPF], StackPanel
ms.assetid: f9239086-451f-42e6-81f7-ef89ef349742
ms.openlocfilehash: 8338421dfb1bea856c15edf9d324cec955584f9f
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59206972"
---
# <a name="how-to-choose-between-stackpanel-and-dockpanel"></a>Procedimiento Elegir entre StackPanel y DockPanel
En este ejemplo se muestra cómo elegir entre usar un <xref:System.Windows.Controls.StackPanel> o un <xref:System.Windows.Controls.DockPanel> cuando apilar el contenido en un <xref:System.Windows.Controls.Panel>.  
  
## <a name="example"></a>Ejemplo  
 Aunque puede usar cualquiera <xref:System.Windows.Controls.DockPanel> o <xref:System.Windows.Controls.StackPanel> para apilar los elementos secundarios, los dos controles no siempre producen los mismos resultados. Por ejemplo, el orden que colocar los elementos secundarios puede afectar al tamaño de los elementos secundarios en un <xref:System.Windows.Controls.DockPanel> , pero no en un <xref:System.Windows.Controls.StackPanel>. Se produce un comportamiento diferente porque <xref:System.Windows.Controls.StackPanel> medidas en la dirección del apilado en <xref:System.Double>.<xref:System.Double.PositiveInfinity>; sin embargo, <xref:System.Windows.Controls.DockPanel> mide solo el tamaño disponible.  
  
 En el ejemplo siguiente se muestra esta diferencia clave entre <xref:System.Windows.Controls.DockPanel> y <xref:System.Windows.Controls.StackPanel>.  
  
 [!code-cpp[StackPanelOvw4#1](~/samples/snippets/cpp/VS_Snippets_Wpf/StackPanelOvw4/CPP/StackPanel_Ovw_Sample4.cpp#1)]
 [!code-csharp[StackPanelOvw4#1](~/samples/snippets/csharp/VS_Snippets_Wpf/StackPanelOvw4/CSharp/StackPanel_Ovw_Sample4.cs#1)]
 [!code-vb[StackPanelOvw4#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/StackPanelOvw4/VisualBasic/StackPanelSamp.vb#1)]
 [!code-xaml[StackPanelOvw4#1](~/samples/snippets/xaml/VS_Snippets_Wpf/StackPanelOvw4/XAML/default.xaml#1)]  
  
## <a name="see-also"></a>Vea también

- <xref:System.Windows.Controls.StackPanel>
- <xref:System.Windows.Controls.DockPanel>
- [Información general sobre elementos Panel](panels-overview.md)
