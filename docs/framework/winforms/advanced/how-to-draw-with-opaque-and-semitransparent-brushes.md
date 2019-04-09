---
title: Filtrar para dibujar con pinceles opacos y semitransparentes
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- semi-transparent shapes [Windows Forms], drawing
- transparency [Windows Forms], semi-transparent shapes
- alpha blending [Windows Forms], brush
- brushes [Windows Forms], using semi-transparent
ms.assetid: a4f6f6b8-3bc8-440a-84af-d62ef0f8ff40
ms.openlocfilehash: a302b8bf978afcead5768fadeb6336c1ece986ec
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2019
ms.locfileid: "59100940"
---
# <a name="how-to-draw-with-opaque-and-semitransparent-brushes"></a>Filtrar para dibujar con pinceles opacos y semitransparentes
Cuando se rellena una forma, se debe pasar un objeto <xref:System.Drawing.Brush> en uno de los métodos de relleno de la clase <xref:System.Drawing.Graphics>. El único parámetro del constructor <xref:System.Drawing.SolidBrush.%23ctor%2A> es un objeto <xref:System.Drawing.Color>. Para rellenar una forma opaca, establezca el componente alfa del color en 255. Para rellenar una forma semitransparente, establezca el componente alfa en cualquier valor entre 1 y 254.  
  
 Cuando se rellena una forma semitransparente, el color de la forma se mezcla con los colores del fondo. El componente alfa especifica cómo se mezclan los colores de la forma y del fondo; los valores alfa cercanos a 0 dan más importancia a los colores de fondo y los cercanos a 255 dan más importancia al color de la forma.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se dibuja un mapa de bits y después se rellenan tres elipses que se superponen al mapa de bits. La primera elipse usa un componente alfa de 255, por lo que es opaca. La segunda y tercera elipses usan un componente alfa de 128, por lo que son semitransparentes; puede ver la imagen de fondo a través de las elipses. La instrucción que establece la propiedad <xref:System.Drawing.Graphics.CompositingQuality%2A> hace que la mezcla de la tercera elipse se realice conjuntamente con la corrección gamma.  

 [!code-csharp[System.Drawing.AlphaBlending#31](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.AlphaBlending/CS/Class1.cs#31)]
 [!code-vb[System.Drawing.AlphaBlending#31](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.AlphaBlending/VB/Class1.vb#31)]  

 La siguiente ilustración muestra la salida del código siguiente: 
  
 ![Ilustración que muestra la salida opaca y semitransparente.](./media/how-to-draw-with-opaque-and-semitransparent-brushes/compositingquality-ellipse-semitransparent.png)  
  
## <a name="compiling-the-code"></a>Compilar el código  
 El ejemplo anterior está diseñado para su uso con Windows Forms y requiere <xref:System.Windows.Forms.PaintEventArgs>`e`, que es un parámetro de <xref:System.Windows.Forms.PaintEventHandler>.  
  
## <a name="see-also"></a>Vea también

- [Gráficos y dibujos en Windows Forms](graphics-and-drawing-in-windows-forms.md)
- [Líneas y rellenos con mezcla alfa](alpha-blending-lines-and-fills.md)
- [Filtrar para proporcionar un fondo transparente a un control](../controls/how-to-give-your-control-a-transparent-background.md)
- [Filtrar para dibujar líneas opacas y semitransparentes](how-to-draw-opaque-and-semitransparent-lines.md)
