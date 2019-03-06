---
title: Información general sobre el control Popup
ms.date: 03/30/2017
helpviewer_keywords:
- controls [WPF], Popup
- Popup control [WPF], about Popup control
ms.assetid: 774f53ca-bff8-470e-9ce9-3928b4cf3d4c
ms.openlocfilehash: 4d480adbbd35084b30e2ca1c74d7392814b87783
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/05/2019
ms.locfileid: "57358475"
---
# <a name="popup-overview"></a>Información general sobre el control Popup
El <xref:System.Windows.Controls.Primitives.Popup> control proporciona una manera de mostrar el contenido de una ventana independiente que flota sobre la ventana de aplicación actual con respecto a una coordenada de pantalla o el elemento designada. Este tema se presentan los <xref:System.Windows.Controls.Primitives.Popup> controlar y proporciona información sobre su uso.  
  
 
  
<a name="What_Is_a_Popup_"></a>   
## <a name="what-is-a-popup"></a>¿Qué es un control Popup?  
 Un <xref:System.Windows.Controls.Primitives.Popup> control muestra el contenido en una ventana independiente con respecto a un elemento o un punto de la pantalla. Cuando el <xref:System.Windows.Controls.Primitives.Popup> está visible, el <xref:System.Windows.Controls.Primitives.Popup.IsOpen%2A> propiedad está establecida en `true`.  
  
> [!NOTE]
>  Un <xref:System.Windows.Controls.Primitives.Popup> no abre automáticamente cuando el puntero del mouse se mueve a través de su objeto primario. Si desea que un <xref:System.Windows.Controls.Primitives.Popup> para abrir automáticamente, use el <xref:System.Windows.Controls.ToolTip> o <xref:System.Windows.Controls.ToolTipService> clase. Para más información, consulte [Información general de información sobre herramientas](tooltip-overview.md).  
  
<a name="APopupExample"></a>   
## <a name="creating-a-popup"></a>Creación de un elemento emergente  
 El ejemplo siguiente muestra cómo definir un <xref:System.Windows.Controls.Primitives.Popup> control que es el elemento secundario de un <xref:System.Windows.Controls.Button> control. Porque un <xref:System.Windows.Controls.Button> puede tener solo un elemento secundario, este ejemplo coloca el texto para el <xref:System.Windows.Controls.Button> y <xref:System.Windows.Controls.Primitives.Popup> controles en un <xref:System.Windows.Controls.StackPanel>. El contenido de la <xref:System.Windows.Controls.Primitives.Popup> aparece en un <xref:System.Windows.Controls.TextBlock> control, que muestra el texto en una ventana independiente que flota sobre la ventana de la aplicación cerca relacionado <xref:System.Windows.Controls.Button> control.  
  
 [!code-xaml[PopupSimple#1](~/samples/snippets/csharp/VS_Snippets_Wpf/PopupSimple/CSharp/Window1.xaml#1)]  
  
 [!code-xaml[PopupSimple#CreatePopupCodeXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/PopupSimple/CSharp/Window1.xaml#createpopupcodexaml)]  
  
<a name="PopupUses"></a>   
## <a name="controls-that-implement-a-popup"></a>Controles que implementan un control Popup  
 Puede compilar <xref:System.Windows.Controls.Primitives.Popup> controles en otros controles. Los controles siguientes implementan el <xref:System.Windows.Controls.Primitives.Popup> control para usos específicos:  
  
-   <xref:System.Windows.Controls.ToolTip>. Si desea crear una información sobre herramientas para un elemento, utilice el <xref:System.Windows.Controls.ToolTip> y <xref:System.Windows.Controls.ToolTipService> clases. Para más información, consulte [Información general de información sobre herramientas](tooltip-overview.md).  
  
-   <xref:System.Windows.Controls.ContextMenu>. Si desea crear un menú contextual para un elemento, utilice el <xref:System.Windows.Controls.ContextMenu> control. Para más información, consulte [Información general sobre ContextMenu](contextmenu-overview.md).  
  
-   <xref:System.Windows.Controls.ComboBox>. Si desea crear un control de selección que tiene un cuadro de lista desplegable que puede estar oculta o, use el <xref:System.Windows.Controls.ComboBox> control.  
  
-   <xref:System.Windows.Controls.Expander>. Si desea crear un control que muestra un encabezado con un área contraíble que muestra contenido, use el <xref:System.Windows.Controls.Expander> control. Para más información, consulte [Información general sobre el control Expander](expander-overview.md).  
  
<a name="PopupBehaviorandAppearance"></a>   
## <a name="popup-behavior-and-appearance"></a>Comportamiento y apariencia del control Popup  
 El <xref:System.Windows.Controls.Primitives.Popup> control proporciona funcionalidad que le permite personalizar su comportamiento y apariencia. Por ejemplo, puede establecer el comportamiento de apertura y cierre, animación, opacidad y efectos de imagen, y <xref:System.Windows.Controls.Primitives.Popup> tamaño y posición.  
  
<a name="OpenandCloseBehavior"></a>   
### <a name="open-and-close-behavior"></a>Comportamiento de apertura y cierre  
 Un <xref:System.Windows.Controls.Primitives.Popup> control muestra su contenido cuando el <xref:System.Windows.Controls.Primitives.Popup.IsOpen%2A> propiedad está establecida en `true`. De forma predeterminada, <xref:System.Windows.Controls.Primitives.Popup> permanece abierta hasta que el <xref:System.Windows.Controls.Primitives.Popup.IsOpen%2A> propiedad está establecida en `false`. Sin embargo, puede cambiar el comportamiento predeterminado estableciendo la <xref:System.Windows.Controls.Primitives.Popup.StaysOpen%2A> propiedad `false`. Al establecer esta propiedad `false`, el <xref:System.Windows.Controls.Primitives.Popup> ventana de contenido tiene la captura del mouse. El <xref:System.Windows.Controls.Primitives.Popup> pierde el mouse captura y la ventana se cierra cuando se produce un evento del mouse fuera de la <xref:System.Windows.Controls.Primitives.Popup> ventana.  
  
 El <xref:System.Windows.Controls.Primitives.Popup.Opened> y <xref:System.Windows.Controls.Primitives.Popup.Closed> se generan eventos cuando el <xref:System.Windows.Controls.Primitives.Popup> ventana de contenido está abierto o cerrado.  
  
<a name="Animation"></a>   
### <a name="animation"></a>Animación  
 El <xref:System.Windows.Controls.Primitives.Popup> control tiene compatibilidad integrada para las animaciones que se asocian habitualmente con comportamientos como fundido y deslizamiento. Puede activar estas animaciones estableciendo el <xref:System.Windows.Controls.Primitives.Popup.PopupAnimation%2A> propiedad a un <xref:System.Windows.Controls.Primitives.PopupAnimation> valor de enumeración. Para <xref:System.Windows.Controls.Primitives.Popup> animaciones funcione correctamente, debe establecer el <xref:System.Windows.Controls.Primitives.Popup.AllowsTransparency%2A> propiedad `true`.  
  
 También puede aplicar animaciones como <xref:System.Windows.Media.Animation.Storyboard> a la <xref:System.Windows.Controls.Primitives.Popup> control.  
  
<a name="OpacityandBitmapEffects"></a>   
### <a name="opacity-and-bitmap-effects"></a>Opacidad y efectos de imagen  
 El <xref:System.Windows.UIElement.Opacity%2A> propiedad para un <xref:System.Windows.Controls.Primitives.Popup> control no tiene ningún efecto en su contenido. De forma predeterminada, el <xref:System.Windows.Controls.Primitives.Popup> ventana de contenido es opaco. Para crear un transparente <xref:System.Windows.Controls.Primitives.Popup>, establezca el <xref:System.Windows.Controls.Primitives.Popup.AllowsTransparency%2A> propiedad `true`.  
  
 El contenido de un <xref:System.Windows.Controls.Primitives.Popup> no hereda efectos de imagen, como <xref:System.Windows.Media.Effects.DropShadowBitmapEffect>, que se establecen directamente en el <xref:System.Windows.Controls.Primitives.Popup> control o en cualquier otro elemento en la ventana primaria. Para los efectos de imagen aparezcan en el contenido de un <xref:System.Windows.Controls.Primitives.Popup>, debe establecer el efecto de imagen directamente en su contenido. Por ejemplo, si el elemento secundario de un <xref:System.Windows.Controls.Primitives.Popup> es un <xref:System.Windows.Controls.StackPanel>, establecer el efecto de imagen en el <xref:System.Windows.Controls.StackPanel>.  
  
<a name="PopupSize"></a>   
### <a name="popup-size"></a>Tamaño del control Popup  
 De forma predeterminada, un <xref:System.Windows.Controls.Primitives.Popup> tamaño se ajusta automáticamente a su contenido. Cuando se produce el ajuste automático de tamaño, se pueden ocultar algunos efectos de mapa de bits porque el tamaño predeterminado del área de pantalla que se define para el <xref:System.Windows.Controls.Primitives.Popup> contenido no proporciona suficiente espacio para los efectos de imagen mostrar.  
  
 <xref:System.Windows.Controls.Primitives.Popup> También puede quedar tapado contenido al establecer un <xref:System.Windows.UIElement.RenderTransform%2A> en el contenido. En este escenario, podría estar oculto algún contenido si el contenido de transformado <xref:System.Windows.Controls.Primitives.Popup> se extiende más allá del área del original <xref:System.Windows.Controls.Primitives.Popup>. Si una transformación o un efecto de mapa de bits requiere más espacio, puede definir un margen alrededor del <xref:System.Windows.Controls.Primitives.Popup> contenido con el fin de proporcionar más área para el control.  
  
<a name="DefiningPopupPosition"></a>   
## <a name="defining-the-popup-position"></a>Definición de la posición del control Popup  
 Puede colocar un elemento emergente estableciendo el <xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A>, <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A>, <xref:System.Windows.Controls.Primitives.Popup.Placement%2A>, <xref:System.Windows.Controls.Primitives.Popup.HorizontalOffset%2A>, y <xref:System.Windows.Controls.Primitives.Popup.VerticalOffsetProperty> propiedades. Para más información, consulte [Posición de un control Popup](popup-placement-behavior.md). Cuando <xref:System.Windows.Controls.Primitives.Popup> se muestra en la pantalla, no cambia su posición si se cambia de posición su elemento primario.  
  
<a name="CustomizingPopupPlacement"></a>   
### <a name="customizing-popup-placement"></a>Personalización de la ubicación del elemento Popup  
 Puede personalizar la ubicación de un <xref:System.Windows.Controls.Primitives.Popup> control mediante la especificación de un conjunto de coordenadas que son relativas a la <xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A> donde desea que el <xref:System.Windows.Controls.Primitives.Popup> que aparezca.  
  
 Para personalizar la colocación, establezca el <xref:System.Windows.Controls.Primitives.Popup.Placement%2A> propiedad <xref:System.Windows.Controls.Primitives.PlacementMode.Custom>. A continuación, defina un <xref:System.Windows.Controls.Primitives.CustomPopupPlacementCallback> delegado que devuelve un conjunto de puntos de selección de ubicación posibles y los ejes principales (en orden de preferencia) para el <xref:System.Windows.Controls.Primitives.Popup>. El punto que muestra la mayor parte de la <xref:System.Windows.Controls.Primitives.Popup> se selecciona automáticamente. Para ver un ejemplo, consulte cómo [especificar una posición emergente personalizada](how-to-specify-a-custom-popup-position.md).  
  
<a name="PopupandtheVisualTree"></a>   
## <a name="popup-and-the-visual-tree"></a>Control Popup y árbol visual  
 Un <xref:System.Windows.Controls.Primitives.Popup> control no tiene su propio árbol visual; en su lugar devuelve un tamaño de 0 (cero) cuando el <xref:System.Windows.Controls.Primitives.Popup.MeasureOverride%2A> método para <xref:System.Windows.Controls.Primitives.Popup> se llama. Sin embargo, al establecer el <xref:System.Windows.Controls.Primitives.Popup.IsOpen%2A> propiedad de <xref:System.Windows.Controls.Primitives.Popup> a `true`, se crea una nueva ventana con su propio árbol visual. La nueva ventana contiene los <xref:System.Windows.Controls.Primitives.Popup.Child%2A> contenido de <xref:System.Windows.Controls.Primitives.Popup>. El ancho y el alto de la ventana nueva no pueden superar en más de un 75 por ciento el ancho o el alto de la pantalla.  
  
 El <xref:System.Windows.Controls.Primitives.Popup> control mantiene una referencia a su <xref:System.Windows.Controls.Primitives.Popup.Child%2A> contenido como un elemento secundario lógico. Cuando se crea la nueva ventana, el contenido de <xref:System.Windows.Controls.Primitives.Popup> se convierte en un elemento secundario visual de la ventana y sigue siendo el elemento secundario lógico de <xref:System.Windows.Controls.Primitives.Popup>. Por el contrario, <xref:System.Windows.Controls.Primitives.Popup> sigue siendo el elemento primario lógico de sus <xref:System.Windows.Controls.Primitives.Popup.Child%2A> contenido.  
  
## <a name="see-also"></a>Vea también
- <xref:System.Windows.Controls.Primitives.Popup>
- <xref:System.Windows.Controls.Primitives.PopupPrimaryAxis>
- <xref:System.Windows.Controls.Primitives.PlacementMode>
- <xref:System.Windows.Controls.Primitives.CustomPopupPlacement>
- <xref:System.Windows.Controls.Primitives.CustomPopupPlacementCallback>
- <xref:System.Windows.Controls.ToolTip>
- <xref:System.Windows.Controls.ToolTipService>
- [Temas "Cómo..."](popup-how-to-topics.md)
- [Temas "Cómo..."](tooltip-how-to-topics.md)
