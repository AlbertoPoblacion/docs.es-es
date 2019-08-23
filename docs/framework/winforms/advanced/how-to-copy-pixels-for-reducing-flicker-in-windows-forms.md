---
title: Procedimiento para copiar píxeles para reducir el parpadeo en formularios Windows Forms
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- bitblt
- graphics [Windows Forms], copying
- flicker [Windows Forms], reducing in Windows Forms
- graphics [Windows Forms], reducing flicker
- pixels [Windows Forms], copying
- flicker
- bit-block transfer
ms.assetid: 33b76910-13a3-4521-be98-5c097341ae3b
ms.openlocfilehash: 5a18539153c64a5059d8079f6e245115b026bb91
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/22/2019
ms.locfileid: "69950146"
---
# <a name="how-to-copy-pixels-for-reducing-flicker-in-windows-forms"></a>Procedimiento para copiar píxeles para reducir el parpadeo en formularios Windows Forms
Al animar un gráfico simple, a veces los usuarios pueden encontrar parpadeo u otros efectos visuales no deseados. Una manera de limitar este problema es utilizar un proceso "bitblt" en el gráfico. Bitblt es la "transferencia de bloque de bits" de los datos de color de un rectángulo de origen de píxeles a un rectángulo de destino de píxeles.  
  
 Con Windows Forms, bitblt se consigue mediante el <xref:System.Drawing.Graphics.CopyFromScreen%2A> método de la <xref:System.Drawing.Graphics> clase. En los parámetros del método, se especifican el origen y el destino (como puntos), el tamaño del área que se va a copiar y el objeto gráfico que se usa para dibujar la nueva forma.  
  
 En el ejemplo siguiente, se dibuja una forma en el formulario en su <xref:System.Windows.Forms.Control.Paint> controlador de eventos. A continuación, <xref:System.Drawing.Graphics.CopyFromScreen%2A> se usa el método para duplicar la forma.  
  
> [!NOTE]
> El establecimiento de la <xref:System.Windows.Forms.Control.DoubleBuffered%2A> propiedad del `true` formulario en hará que el <xref:System.Windows.Forms.Control.Paint> código basado en gráficos del evento tenga doble búfer. Aunque esto no tendrá ningún aumento de rendimiento de la información al usar el código siguiente, es algo que debe tener en cuenta al trabajar con código de manipulación de gráficos más complejo.  
  
## <a name="example"></a>Ejemplo  
  
```vb  
Private Sub Form1_Paint(ByVal sender As Object, ByVal e As _  
    System.Windows.Forms.PaintEventArgs) Handles MyBase.Paint  
    ' Draw a circle with a bar on top.  
        e.Graphics.FillEllipse(Brushes.DarkBlue, New Rectangle _  
             (10, 10, 60, 60))  
        e.Graphics.FillRectangle(Brushes.Khaki, New Rectangle _  
             (20, 30, 60, 10))  
    ' Copy the graphic to a new location.  
        e.Graphics.CopyFromScreen(New Point(10, 10), New Point _  
             (100, 100), New Size(70, 70))  
End Sub  
```  
  
```csharp  
private void Form1_Paint(System.Object sender,  
    System.Windows.Forms.PaintEventArgs e)  
        {  
        e.Graphics.FillEllipse(Brushes.DarkBlue, new  
            Rectangle(10,10,60,60));  
        e.Graphics.FillRectangle(Brushes.Khaki, new  
            Rectangle(20,30,60,10));  
        e.Graphics.CopyFromScreen(new Point(10, 10), new Point(100, 100),   
            new Size(70, 70));  
}  
```  
  
## <a name="compiling-the-code"></a>Compilar el código  
 El código anterior se ejecuta en el controlador de <xref:System.Windows.Forms.Control.Paint> eventos del formulario para que los gráficos se conserven cuando se vuelva a dibujar el formulario. Como tal, no llame a los métodos relacionados con gráficos en <xref:System.Windows.Forms.Form.Load> el controlador de eventos, ya que el contenido dibujado no se volverá a dibujar si el formulario cambia de tamaño o está oculto por otro formulario.  
  
## <a name="see-also"></a>Vea también

- <xref:System.Drawing.CopyPixelOperation>
- <xref:System.Drawing.Graphics.FillRectangle%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.Control.OnPaint%2A?displayProperty=nameWithType>
- [Gráficos y dibujos en Windows Forms](graphics-and-drawing-in-windows-forms.md)
- [Utilizar lápiz para dibujar líneas y formas](using-a-pen-to-draw-lines-and-shapes.md)
