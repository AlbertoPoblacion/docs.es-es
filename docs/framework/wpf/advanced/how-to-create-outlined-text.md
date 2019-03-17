---
title: Filtrar Crear texto con contorno
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- typography [WPF], linear gradient brush
- outlined text [WPF]
- gradient brush [WPF]
- linear gradient brush [WPF]
- typography [WPF], outline effects
ms.assetid: 4aa3cf6e-1953-4f26-8230-7c1409e5f28d
ms.openlocfilehash: 5de1068401dac61c5de5b86604da9417e18a94ae
ms.sourcegitcommit: 16aefeb2d265e69c0d80967580365fabf0c5d39a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/16/2019
ms.locfileid: "58125946"
---
# <a name="how-to-create-outlined-text"></a>Filtrar Crear texto con contorno
En la mayoría de los casos, cuando se agregan adorno a cadenas de texto en su [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] aplicación, que usa texto en términos de una colección de caracteres discretos, o glifos. Por ejemplo, podría crear un pincel de degradado lineal y se aplicará la <xref:System.Windows.Controls.Control.Foreground%2A> propiedad de un <xref:System.Windows.Controls.TextBox> objeto. Al mostrar o editar el cuadro de texto, el pincel de degradado lineal se aplica automáticamente al conjunto actual de caracteres de la cadena de texto.  
  
 ![Texto que se muestra con un pincel de degradado lineal](./media/how-to-create-outlined-text/text-linear-gradient.jpg)    
  
 Sin embargo, también puede convertir texto en <xref:System.Windows.Media.Geometry> objetos, lo que permite crear otros tipos de texto enriquecido visualmente. Por ejemplo, podría crear un <xref:System.Windows.Media.Geometry> objeto basado en el esquema de una cadena de texto.  
  
 ![Esquema de texto que usa un pincel de degradado lineal](./media/how-to-create-outlined-text/text-outline-linear-gradient.jpg)  
  
 Cuando el texto se convierte en un <xref:System.Windows.Media.Geometry> de objeto, ya no es una colección de caracteres, no se puede modificar los caracteres de la cadena de texto. Sin embargo, puede afectar a la apariencia del texto convertido modificando sus propiedades de trazo y relleno. El trazo se refiere al contorno del texto convertido; el relleno es el área dentro del contorno del texto convertido.  
  
 Los ejemplos siguientes ilustran varias maneras de crear efectos visuales modificando el trazo y el relleno del texto convertido.  
  
 ![Texto con colores diferentes para relleno y trazo](./media/how-to-create-outlined-text/fill-stroke-text-effect.jpg)  
  
 ![Texto con pincel de imagen aplicado a trazo](./media/how-to-create-outlined-text/image-brush-application.jpg)
  
 También es posible modificar el rectángulo delimitador, o el resaltado del texto convertido. El ejemplo siguiente muestra una manera de crear efectos visuales modificando el trazo y el resaltado del texto convertido.  
  
 ![Texto con pincel de imagen aplicado para trazar y resaltar](./media/how-to-create-outlined-text/image-brush-text-application.jpg)

## <a name="example"></a>Ejemplo  
 La clave para convertir texto a un <xref:System.Windows.Media.Geometry> objeto consiste en usar el <xref:System.Windows.Media.FormattedText> objeto. Una vez que ha creado este objeto, puede usar el <xref:System.Windows.Media.FormattedText.BuildGeometry%2A> y <xref:System.Windows.Media.FormattedText.BuildHighlightGeometry%2A> métodos para convertir el texto en <xref:System.Windows.Media.Geometry> objetos. El primer método devuelve la geometría del texto con formato; el segundo método devuelve que el cuadro de límite de la geometría del texto con formato. En el ejemplo de código siguiente se muestra cómo crear un <xref:System.Windows.Media.FormattedText> objeto y recuperar las geometrías de texto con formato y su rectángulo de selección.  
  
 [!code-csharp[OutlineTextControlViewer#CreateText](~/samples/snippets/csharp/VS_Snippets_Wpf/OutlineTextControlViewer/CSharp/OutlineTextControl.cs#createtext)]
 [!code-vb[OutlineTextControlViewer#CreateText](~/samples/snippets/visualbasic/VS_Snippets_Wpf/OutlineTextControlViewer/visualbasic/outlinetextcontrol.vb#createtext)]  
  
 Para mostrar el objeto recuperado el <xref:System.Windows.Media.Geometry> objetos, debe tener acceso a la <xref:System.Windows.Media.DrawingContext> del objeto que se muestra el texto convertido. En estos ejemplos de código, esto se hace mediante la creación de un objeto de control personalizado que se deriva de una clase que admite el procesamiento definido por el usuario.  
  
 Para mostrar <xref:System.Windows.Media.Geometry> objetos en el control personalizado, proporcione una invalidación para el <xref:System.Windows.UIElement.OnRender%2A> método. Debe usar el método invalidado la <xref:System.Windows.Media.DrawingContext.DrawGeometry%2A> método para dibujar el <xref:System.Windows.Media.Geometry> objetos.  
  
 [!code-csharp[OutlineTextControlViewer#OnRender](~/samples/snippets/csharp/VS_Snippets_Wpf/OutlineTextControlViewer/CSharp/OutlineTextControl.cs#onrender)]
 [!code-vb[OutlineTextControlViewer#OnRender](~/samples/snippets/visualbasic/VS_Snippets_Wpf/OutlineTextControlViewer/visualbasic/outlinetextcontrol.vb#onrender)]  
  
  Para el origen del objeto de control de usuario personalizado de ejemplo, vea [OutlineTextControl.cs para C# ](https://github.com/dotnet/samples/blob/master/snippets/csharp/VS_Snippets_Wpf/OutlineTextControlViewer/CSharp/OutlineTextControl.cs) y [OutlineTextControl.vb para Visual Basic](https://github.com/dotnet/samples/blob/master/snippets/visualbasic/VS_Snippets_Wpf/OutlineTextControlViewer/visualbasic/outlinetextcontrol.vb). 
  
## <a name="see-also"></a>Vea también
- [Dibujar texto con formato](drawing-formatted-text.md)
