---
title: Procedimiento Invalidar el método OnRender de un objeto Panel
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
f1_keywords:
- overriding OnRender method
- Panel control, overriding OnRender method
- OnRender method
- controls, Panel, overriding OnRender method
helpviewer_keywords:
- overriding OnRender method of Panel control [WPF]
- OnRender method [WPF], overriding
- Panel control [WPF], overriding OnRender method
ms.assetid: 57397834-a085-4e36-90ab-416fad98f341
ms.openlocfilehash: c4539847368c1a5789e99ec92106d17077ed5943
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61770843"
---
# <a name="how-to-override-the-panel-onrender-method"></a>Procedimiento Invalidar el método OnRender de un objeto Panel
En este ejemplo se muestra cómo invalidar el <xref:System.Windows.Controls.Panel.OnRender%2A> método <xref:System.Windows.Controls.Panel> con el fin de agregar efectos gráficos personalizados a un elemento de diseño.  
  
## <a name="example"></a>Ejemplo  
 Use el <xref:System.Windows.Controls.Panel.OnRender%2A> método para agregar efectos gráficos a un elemento panel representado. Por ejemplo, puede usar este método para agregar un borde personalizado o efectos en segundo plano. Un <xref:System.Windows.Media.DrawingContext> objeto se pasa como argumento, que proporciona métodos para dibujar formas, texto, imágenes o vídeos. Como resultado, este método es útil para la personalización de un objeto de panel.  
  
 [!code-csharp[LightWeightCustomPanel#1](~/samples/snippets/csharp/VS_Snippets_Wpf/LightWeightCustomPanel/CSharp/OffsetPanel.cs#1)]
 [!code-vb[LightWeightCustomPanel#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/LightWeightCustomPanel/visualbasic/offsetpanel.vb#1)]  
  
## <a name="see-also"></a>Vea también

- <xref:System.Windows.Controls.Panel>
- [Información general sobre elementos Panel](panels-overview.md)
- [Ejemplo de Panel Radial personalizado](https://go.microsoft.com/fwlink/?LinkID=159982)
- [Temas "Cómo..."](panel-how-to-topics.md)
