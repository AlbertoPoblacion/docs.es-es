---
title: Gráficos y multimedia
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- media [WPF], features
- video effects [WPF]
- sound effects [WPF]
- animation [WPF], features
- graphics features [WPF]
- transition effects [WPF]
ms.assetid: 1817d9dc-3d6c-46cb-afc8-63b0bae35e37
ms.openlocfilehash: 150b742c2195c07abf2b2823871627b0ba827580
ms.sourcegitcommit: 82f94a44ad5c64a399df2a03fa842db308185a76
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/25/2019
ms.locfileid: "72919987"
---
# <a name="graphics-and-multimedia"></a>Gráficos y multimedia

<a name="introduction"></a>
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] proporciona compatibilidad con multimedia, gráficos vectoriales, animación y composición de contenido, lo que facilita a los desarrolladores la creación de interfaces de usuario y contenido interesantes. Con Visual Studio, puede crear gráficos vectoriales o animaciones complejas e integrar los elementos multimedia en las aplicaciones.

En este tema se presentan las características de gráficos, animaciones y elementos multimedia de [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], que le permiten agregar gráficos, efectos de transición, sonido y vídeo a las aplicaciones.

> [!NOTE]
> Se recomienda encarecidamente no usar los tipos WPF en un servicio de Windows. Si intenta usar tipos WPF en un servicio de Windows, puede que el servicio no funcione como se espera.

<a name="whats_new_with_graphics_and_multimedia_in_wpf_4"></a>

## <a name="whats-new-with-graphics-and-multimedia-in-wpf-4"></a>Novedades de gráficos y multimedia en WPF 4

Se han efectuado varios cambios relacionados con los gráficos y animaciones.

- Redondeo del diseño

  Cuando el borde de un objeto queda en medio de un dispositivo de píxeles, el sistema de gráficos independiente de los ppp puede crear artefactos de representación tales como bordes borrosos o semitransparentes. Versiones anteriores de WPF incluían el ajuste de píxeles para ayudar a controlar este caso. Silverlight 2 introdujo el redondeo del diseño, que es otra manera de mover elementos para que los bordes queden dentro de límites de píxeles enteros. WPF admite ahora el redondeo del diseño con la <xref:System.Windows.FrameworkElement.UseLayoutRounding%2A> propiedad adjunta en <xref:System.Windows.FrameworkElement>.

- Composición almacenada en caché

  Mediante el uso de las nuevas clases <xref:System.Windows.Media.BitmapCache> y <xref:System.Windows.Media.BitmapCacheBrush>, puede almacenar en caché una parte compleja del árbol visual como un mapa de bits y mejorar considerablemente el tiempo de representación. El mapa de bits sigue respondiendo a la entrada del usuario, como clics del mouse, y se puede pintar en otros elementos, exactamente igual que cualquier pincel.

- Compatibilidad con el sombreador de píxeles 3

  WPF 4 se basa en la compatibilidad de <xref:System.Windows.Media.Effects.ShaderEffect> introducida en WPF 3,5 SP1 al permitir que las aplicaciones escriban efectos mediante el sombreador de píxeles (PS) versión 3,0. El modelo de sombreador PS 3.0 es más sofisticado que el PS 2.0, lo que permite incluso crear más efectos en hardware compatible.

- Funciones de aceleración

  Puede mejorar las animaciones con funciones de aceleración que proporcionan mayor control sobre el comportamiento de las animaciones. Por ejemplo, puede aplicar una <xref:System.Windows.Media.Animation.ElasticEase> a una animación para dar un comportamiento elástico a la animación. Para obtener más información, vea los tipos de aceleración en el espacio de nombres <xref:System.Windows.Media.Animation>.

<a name="graphics_and_rendering"></a>

## <a name="graphics-and-rendering"></a>Gráficos y representación

WPF incluye compatibilidad con gráficos 2D de alta calidad. La funcionalidad incluye pinceles, geometrías, imágenes, formas y transformaciones. Para más información, consulte [Graphics](graphics.md) (Gráficos). La representación de elementos gráficos se basa en la clase <xref:System.Windows.Media.Visual>. La estructura de objetos visuales en la pantalla se describe en el árbol visual. Para más información, vea [Información general sobre la representación de gráficos en WPF](wpf-graphics-rendering-overview.md).

### <a name="2-d-shapes"></a>Formas 2D

[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] proporciona una biblioteca de formas bidimensionales de uso frecuente, como rectángulos y elipses, que se muestra en la siguiente ilustración.

![Diagrama que muestra puntos suspensivos y rectángulos.](./media/index/two-deminsional-shapes-ellipses-rectangles.png)

Estas formas intrínsecas de [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] no son solo formas: son elementos programables que implementan muchas de las características que se esperan de los controles más comunes, entre los que se incluyen la entrada por mouse y teclado. En el ejemplo siguiente se muestra cómo controlar el evento de <xref:System.Windows.UIElement.MouseUp> que se produce al hacer clic en un elemento <xref:System.Windows.Shapes.Ellipse>.

```xaml
<Window
  xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
  xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
  x:Class="Window1" >
  <Ellipse Fill="LightBlue" MouseUp="ellipseButton_MouseUp" />
</Window>
```

```csharp
public partial class Window1  : Window
{
    void ellipseButton_MouseUp(object sender, MouseButtonEventArgs e)
    {
        MessageBox.Show("You clicked the ellipse!");
    }
}
```

```vb
Partial Public Class Window1
    Inherits Window
    Private Sub ellipseButton_MouseUp(ByVal sender As Object, ByVal e As MouseButtonEventArgs)
        MessageBox.Show("You clicked the ellipse!")
    End Sub
End Class
```

En la ilustración siguiente se muestra el resultado del anterior marcado y código [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] subyacente.

![Un cuadro de mensaje que indica "hizo clic en la elipse!"](./media/index/messagebox-text-output.png)

Para obtener más información, consulte [Información general sobre formas y dibujo básico en WPF](shapes-and-basic-drawing-in-wpf-overview.md). Para obtener un ejemplo introductorio, vea [Shape Elements Sample](https://go.microsoft.com/fwlink/?LinkID=160037) (Ejemplo de elementos de forma).

### <a name="2-d-geometries"></a>Geometrías 2D

Cuando las formas 2D que [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] proporciona no son suficientes, puede usar [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] compatibilidad con las geometrías y las rutas de acceso para crear las suyas propias. En la ilustración siguiente se muestra cómo se pueden usar geometrías para crear formas, por ejemplo, un pincel de dibujo, y para recortar otros elementos [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)].

![Captura de pantalla que muestra cómo se pueden usar las geometrías para crear formas.](./media/index/use-geometries-create-shapes.png)

Para más información, consulte [Información general sobre geometría](geometry-overview.md). Para obtener un ejemplo introductorio, vea [Ejemplo de geometrías](https://go.microsoft.com/fwlink/?LinkID=159989).

### <a name="2-d-effects"></a>Efectos 2D

[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] proporciona una biblioteca de clases 2D que puede usar para crear una variedad de efectos. La capacidad de representación en 2D de [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] proporciona la capacidad de pintar [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] elementos que tienen degradados, mapas de bits, dibujos y vídeos; y para manipularlos mediante la rotación, el escalado y el sesgo. En la ilustración siguiente se ofrece un ejemplo de los muchos efectos que puede lograr mediante pinceles de [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)].

![Ilustración que muestra los diferentes pinceles y elementos de dibujo de WPF.](./media/index/brushes-paint-elements.png)

Para obtener más información, consulte [Información general sobre pinceles de WPF](wpf-brushes-overview.md). Para obtener un ejemplo introductorio, vea [Ejemplo de pinceles](https://go.microsoft.com/fwlink/?LinkID=159973).

<a name="rendering"></a>

## <a name="3-d-rendering"></a>Representación 3D

[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] proporciona un conjunto de capacidades de representación 3D que se integran con la compatibilidad con gráficos 2D en [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] para que pueda crear un diseño, un [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]y una visualización de datos más interesantes. En un extremo del espectro, [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] le permite representar imágenes 2D en las superficies de las formas 3D, que se muestran en la siguiente ilustración.

![Captura de pantalla de un ejemplo en el que se muestran formas 3D con texturas diferentes.](./media/index/visual-three-dimensional-shape.png)

Para obtener más información, consulte [Información general sobre gráficos 3D](3-d-graphics-overview.md). Para obtener un ejemplo introductorio, vea [3-D Solids Sample](https://go.microsoft.com/fwlink/?LinkID=159964) (Ejemplo de sólidos 3D).

<a name="animation"></a>

## <a name="animation"></a>Animación

Use la animación para hacer que los controles y elementos crezcan, vibren, giren o se desvanezcan, crear atractivas transiciones de página y mucho más. Dado que [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] le permite animar la mayoría de las propiedades, no solo podrá animar la mayoría de los objetos [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)], también podrá usar [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] para animar objetos personalizados que haya creado.

![Captura de pantalla de un cubo animado.](./media/index/animate-custom-objects.png)

Para obtener más información, consulte [Información general sobre animaciones](animation-overview.md). Para obtener un ejemplo introductorio, vea [Animation Example Gallery](https://go.microsoft.com/fwlink/?LinkID=159969) (Galería de ejemplos de animación).

<a name="media"></a>

## <a name="media"></a>Multimedia

Las imágenes, el vídeo y el audio son maneras de ofrecer experiencias de usuario e información con mucho contenido multimedia.

### <a name="images"></a>Imágenes

Las imágenes, que incluyen iconos, fondos e incluso partes de animaciones, constituyen una pieza esencial de la mayoría de las aplicaciones. Dado que frecuentemente tendrá que usar imágenes, [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] presenta la posibilidad de trabajar con ellas de diversas maneras. En la ilustración siguiente se muestra tan solo una de esas maneras.

![Captura de pantalla de ejemplo de estilo](../controls/./media/stylingintro-eventtriggers.png "StylingIntro_EventTriggers")

Para obtener más información, consulte [Información general sobre imágenes](imaging-overview.md).

### <a name="video-and-audio"></a>Vídeo y audio

Una característica fundamental de la funcionalidad de gráficos de [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] es que ofrece compatibilidad nativa para trabajar con multimedia, lo que incluye vídeo y audio. En el siguiente ejemplo se muestra cómo insertar un reproductor multimedia en una aplicación.

```xaml
<MediaElement Source="media\numbers.wmv" Width="450" Height="250" />
```

<xref:System.Windows.Controls.MediaElement> es capaz de reproducir vídeo y audio, y es lo suficientemente extensible como para permitir la creación sencilla de interfaces de IU personalizadas.

Para más información, consulte [Información general sobre multimedia](multimedia-overview.md).

## <a name="see-also"></a>Vea también

- <xref:System.Windows.Media>
- <xref:System.Windows.Media.Animation>
- <xref:System.Windows.Media.Media3D>
- [Imágenes y gráficos 2D](../advanced/optimizing-performance-2d-graphics-and-imaging.md)
- [Información general sobre formas y dibujo básico en WPF](shapes-and-basic-drawing-in-wpf-overview.md)
- [Información general sobre el dibujo con colores sólidos y degradados](painting-with-solid-colors-and-gradients-overview.md)
- [Pintar con imágenes, dibujos y elementos visuales](painting-with-images-drawings-and-visuals.md)
- [Temas de procedimientos de animación y control de tiempo](animation-and-timing-how-to-topics.md)
- [Información general sobre gráficos 3D](3-d-graphics-overview.md)
- [Información general sobre multimedia](multimedia-overview.md)
