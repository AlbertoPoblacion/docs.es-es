---
title: Información general sobre alineación, márgenes y relleno
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- margins [WPF]
- padding [WPF]
- aligning [WPF]
ms.assetid: 9c6a2009-9b86-4e40-8605-0a2664dc3973
ms.openlocfilehash: 58af8848a6b8a5e4ded453831f5a7ef985548492
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59209169"
---
# <a name="alignment-margins-and-padding-overview"></a>Información general sobre alineación, márgenes y relleno
La <xref:System.Windows.FrameworkElement> clase expone varias propiedades que se usan para posicionar elementos secundarios. En este tema se analiza cuatro de las propiedades más importantes: <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A>, <xref:System.Windows.FrameworkElement.Margin%2A>, <xref:System.Windows.Controls.Border.Padding%2A>, y <xref:System.Windows.FrameworkElement.VerticalAlignment%2A>. Es importante comprender los efectos de estas propiedades, ya que proporcionan la base para controlar la posición de los elementos de las aplicaciones de [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)].  

<a name="wcpsdk_layout_amp_introduction"></a>   
## <a name="introduction-to-element-positioning"></a>Introducción al posicionamiento de elementos  
 Existen numerosas maneras de posicionar elementos mediante [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]. Sin embargo, lograr el diseño ideal va más allá de simplemente elegir el derecho <xref:System.Windows.Controls.Panel> elemento. Control exhaustivo del posicionamiento requiere una comprensión de la <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A>, <xref:System.Windows.FrameworkElement.Margin%2A>, <xref:System.Windows.Controls.Border.Padding%2A>, y <xref:System.Windows.FrameworkElement.VerticalAlignment%2A> propiedades.  
  
 La siguiente ilustración muestra un escenario de diseño que usa varias propiedades de posicionamiento.  
  
 ![Ejemplo de propiedades de posicionamiento de WPF](./media/layout-margins-padding-alignment-graphic1.PNG "layout_margins_padding_alignment_graphic1")  
  
 A primera vista, el <xref:System.Windows.Controls.Button> pueden parecer que los elementos en esta ilustración colocados de forma aleatoria. Sin embargo, sus posiciones se controlan realmente de forma precisa mediante una combinación de márgenes, alineaciones y relleno.  
  
 En el ejemplo siguiente se describe cómo crear el diseño de la ilustración anterior. Un <xref:System.Windows.Controls.Border> encapsula un elemento primario <xref:System.Windows.Controls.StackPanel>, con un <xref:System.Windows.Controls.Border.Padding%2A> valor de 15 píxeles independientes del dispositivo. Esto representa el estrecho <xref:System.Windows.Media.Brushes.LightBlue%2A> que rodea el elemento secundario <xref:System.Windows.Controls.StackPanel>. Los elementos secundarios de la <xref:System.Windows.Controls.StackPanel> sirven para ilustrar cada una de las distintas propiedades de posicionamiento que se detallan en este tema. Tres <xref:System.Windows.Controls.Button> elementos se usan para mostrar tanto el <xref:System.Windows.FrameworkElement.Margin%2A> y <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> propiedades.  
  
 [!code-csharp[MPALayoutSampleIntro#1](~/samples/snippets/csharp/VS_Snippets_Wpf/MPALayoutSampleIntro/CSharp/MPA_Layout_Sample_Intro.cs#1)]
 [!code-vb[MPALayoutSampleIntro#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/MPALayoutSampleIntro/VisualBasic/MPALayoutIntro.vb#1)]  
  
 En el siguiente diagrama se proporciona una vista de primer plano de las distintas propiedades de posicionamiento que se usan en el ejemplo anterior. En las siguientes secciones de este tema se describe con más detalle cómo usar cada propiedad de posicionamiento.  
  
 ![Propiedades de posicionamiento con llamadas de pantalla](./media/layout-margins-padding-alignment-graphic2.PNG "layout_margins_padding_alignment_graphic2")  
  
<a name="wcpsdk_layout_amp_alignment_properties"></a>   
## <a name="understanding-alignment-properties"></a>Explicación de las propiedades Alignment  
 El <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> y <xref:System.Windows.FrameworkElement.VerticalAlignment%2A> propiedades describen cómo se debería colocar un elemento secundario dentro del espacio de diseño asignado del elemento de un elemento primario. Al usar estas propiedades juntas, puede posicionar los elementos secundarios con precisión. Por ejemplo, los elementos secundarios de un <xref:System.Windows.Controls.DockPanel> puede especificar cuatro alineaciones horizontales: <xref:System.Windows.HorizontalAlignment.Left>, <xref:System.Windows.HorizontalAlignment.Right>, o <xref:System.Windows.HorizontalAlignment.Center>, o a <xref:System.Windows.HorizontalAlignment.Stretch> para rellenar el espacio disponible. Para el posicionamiento vertical existen valores similares.  
  
> [!NOTE]
>  Establecidas de forma explícita <xref:System.Windows.FrameworkElement.Height%2A> y <xref:System.Windows.FrameworkElement.Width%2A> propiedades en un elemento tienen prioridad sobre la <xref:System.Windows.HorizontalAlignment.Stretch> valor de propiedad. Al intentar establecer <xref:System.Windows.FrameworkElement.Height%2A>, <xref:System.Windows.FrameworkElement.Width%2A>y un <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> valor `Stretch` da como resultado la `Stretch` solicitar que se omiten.  
  
<a name="wcpsdk_layout_amp_horizontalalignment_properties"></a>   
### <a name="horizontalalignment-property"></a>Propiedad HorizontalAlignment  
 El <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> propiedad declara las características de alineación horizontal para aplicar a los elementos secundarios. La siguiente tabla muestra cada uno de los valores posibles de la <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> propiedad.  
  
|Miembro|Descripción|  
|------------|-----------------|  
|<xref:System.Windows.HorizontalAlignment.Left>|Los elementos secundarios se alinean a la izquierda del espacio de diseño asignado del elemento primario.|  
|<xref:System.Windows.HorizontalAlignment.Center>|Los elementos secundarios se alinean en el centro del espacio de diseño asignado del elemento primario.|  
|<xref:System.Windows.HorizontalAlignment.Right>|Los elementos secundarios se alinean a la derecha del espacio de diseño asignado del elemento primario.|  
|<xref:System.Windows.HorizontalAlignment.Stretch> (Valor predeterminado)|Los elementos secundarios se ajustan para rellenar el espacio de diseño asignado del elemento primario. Explícita <xref:System.Windows.FrameworkElement.Width%2A> y <xref:System.Windows.FrameworkElement.Height%2A> valores tienen prioridad.|  
  
 El ejemplo siguiente muestra cómo aplicar el <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> propiedad <xref:System.Windows.Controls.Button> elementos. Se muestran todos los valores de atributo para ilustrar mejor los distintos comportamientos de representación.  
  
 [!code-csharp[MPALayoutHorizontalAlignment#2](~/samples/snippets/csharp/VS_Snippets_Wpf/MPALayoutHorizontalAlignment/CSharp/MPA_Layout_HorizontalAlignment.cs#2)]
 [!code-vb[MPALayoutHorizontalAlignment#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/MPALayoutHorizontalAlignment/VisualBasic/MPA_Layout_HorizontalAlignment.vb#2)]  
  
 El código anterior produce un diseño similar al de la siguiente imagen. Los efectos de posicionamiento de cada <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> valor están visibles en la ilustración.  
  
 ![Ejemplo HorizontalAlignment](./media/layout-horizontal-alignment-graphic.PNG "layout_horizontal_alignment_graphic")  
  
<a name="wcpsdk_layout_amp_verticalalignment_properties"></a>   
### <a name="verticalalignment-property"></a>Propiedad VerticalAlignment  
 El <xref:System.Windows.FrameworkElement.VerticalAlignment%2A> propiedad describe las características de alineación vertical para aplicar a los elementos secundarios. La siguiente tabla muestra cada uno de los valores posibles para el <xref:System.Windows.FrameworkElement.VerticalAlignment%2A> propiedad.  
  
|Miembro|Descripción|  
|------------|-----------------|  
|<xref:System.Windows.VerticalAlignment.Top>|Los elementos secundarios se alinean en la parte superior del espacio de diseño asignado del elemento primario.|  
|<xref:System.Windows.VerticalAlignment.Center>|Los elementos secundarios se alinean en el centro del espacio de diseño asignado del elemento primario.|  
|<xref:System.Windows.VerticalAlignment.Bottom>|Los elementos secundarios se alinean en la parte inferior del espacio de diseño asignado del elemento primario.|  
|<xref:System.Windows.VerticalAlignment.Stretch> (Valor predeterminado)|Los elementos secundarios se ajustan para rellenar el espacio de diseño asignado del elemento primario. Explícita <xref:System.Windows.FrameworkElement.Width%2A> y <xref:System.Windows.FrameworkElement.Height%2A> valores tienen prioridad.|  
  
 El ejemplo siguiente muestra cómo aplicar el <xref:System.Windows.FrameworkElement.VerticalAlignment%2A> propiedad <xref:System.Windows.Controls.Button> elementos. Se muestran todos los valores de atributo para ilustrar mejor los distintos comportamientos de representación. Para fines de este ejemplo, un <xref:System.Windows.Controls.Grid> elemento con las líneas de cuadrícula visibles se usa como el elemento primario, para ilustrar mejor el comportamiento de diseño de cada valor de propiedad.  
  
 [!code-csharp[MPALayoutVerticalAlignment#2](~/samples/snippets/csharp/VS_Snippets_Wpf/MPALayoutVerticalAlignment/CSharp/MPA_Layout_VerticalAlignment.cs#2)]
 [!code-vb[MPALayoutVerticalAlignment#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/MPALayoutVerticalAlignment/VisualBasic/MPA_Layout_VerticalAlignment.vb#2)]
 [!code-xaml[MPALayoutVerticalAlignment#2](~/samples/snippets/xaml/VS_Snippets_Wpf/MPALayoutVerticalAlignment/XAML/default.xaml#2)]  
  
 El código anterior produce un diseño similar al de la siguiente imagen. Los efectos de posicionamiento de cada <xref:System.Windows.FrameworkElement.VerticalAlignment%2A> valor están visibles en la ilustración.  
  
 ![Ejemplo de propiedad VerticalAlignment](./media/layout-vertical-alignment-graphic.PNG "layout_vertical_alignment_graphic")  
  
<a name="wcpsdk_layout_amp_margin_properties"></a>   
## <a name="understanding-margin-properties"></a>Explicación de las propiedades Margin  
 El <xref:System.Windows.FrameworkElement.Margin%2A> propiedad describe la distancia entre un elemento y sus secundarios o elementos del mismo nivel. <xref:System.Windows.FrameworkElement.Margin%2A> los valores pueden ser uniformes, con una sintaxis similar `Margin="20"`. Con esta sintaxis, un uniforme <xref:System.Windows.FrameworkElement.Margin%2A> del dispositivo 20 píxeles independientes se aplicaría al elemento. <xref:System.Windows.FrameworkElement.Margin%2A> los valores pueden también adoptan la forma de cuatro valores distintos, cada valor que describe un margen distinto para aplicar a la izquierda, superior, derecha e inferior (en ese orden), como `Margin="0,10,5,25"`. El uso correcto de la <xref:System.Windows.FrameworkElement.Margin%2A> propiedad permite un control muy preciso de la posición de representación de un elemento y la posición de representación de sus elementos contiguos y secundarios.  
  
> [!NOTE]
>  Un margen distinto de cero aplica espacio fuera del elemento <xref:System.Windows.FrameworkElement.ActualWidth%2A> y <xref:System.Windows.FrameworkElement.ActualHeight%2A>.  
  
 El ejemplo siguiente muestra cómo aplicar márgenes uniformes alrededor de un grupo de <xref:System.Windows.Controls.Button> elementos. El <xref:System.Windows.Controls.Button> elementos se espacian uniformemente con un búfer de margen de diez píxeles en cada dirección.  
  
 [!code-cpp[MarginPaddingAlignmentSample#1](~/samples/snippets/cpp/VS_Snippets_Wpf/MarginPaddingAlignmentSample/CPP/Margin_Padding_Alignment_Sample.cpp#1)]
 [!code-csharp[MarginPaddingAlignmentSample#1](~/samples/snippets/csharp/VS_Snippets_Wpf/MarginPaddingAlignmentSample/CSharp/Margin_Padding_Alignment_Sample.cs#1)]
 [!code-vb[MarginPaddingAlignmentSample#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/MarginPaddingAlignmentSample/VisualBasic/MarginPaddingAlignment.vb#1)]
 [!code-xaml[MarginPaddingAlignmentSample#1](~/samples/snippets/xaml/VS_Snippets_Wpf/MarginPaddingAlignmentSample/XAML/default.xaml#1)]  
  
 En muchos casos, un margen uniforme no resulta apropiado. En estos casos, se puede aplicar un espaciado no uniforme. En el ejemplo siguiente se muestra cómo aplicar un espaciado de margen no uniforme a los elementos secundarios. Los márgenes se describen en este orden: izquierdo, superior, derecho e inferior.  
  
 [!code-cpp[MarginPaddingAlignmentSample#2](~/samples/snippets/cpp/VS_Snippets_Wpf/MarginPaddingAlignmentSample/CPP/Margin_Padding_Alignment_Sample.cpp#2)]
 [!code-csharp[MarginPaddingAlignmentSample#2](~/samples/snippets/csharp/VS_Snippets_Wpf/MarginPaddingAlignmentSample/CSharp/Margin_Padding_Alignment_Sample.cs#2)]
 [!code-vb[MarginPaddingAlignmentSample#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/MarginPaddingAlignmentSample/VisualBasic/MarginPaddingAlignment.vb#2)]
 [!code-xaml[MarginPaddingAlignmentSample#2](~/samples/snippets/xaml/VS_Snippets_Wpf/MarginPaddingAlignmentSample/XAML/default.xaml#2)]  
  
<a name="wcpsdk_layout_amp_padding_properties"></a>   
## <a name="understanding-the-padding-property"></a>Descripción de la propiedad Padding  
 Padding es similar a <xref:System.Windows.FrameworkElement.Margin%2A> en todos los sentidos. La propiedad Padding se expone solo en algunas clases, principalmente por comodidad: <xref:System.Windows.Documents.Block>, <xref:System.Windows.Controls.Border>, <xref:System.Windows.Controls.Control>, y <xref:System.Windows.Controls.TextBlock> son ejemplos de clases que exponen una propiedad Padding. El <xref:System.Windows.Controls.Border.Padding%2A> propiedad amplía el tamaño efectivo de un elemento secundario por especificado <xref:System.Windows.Thickness> valor.  
  
 El ejemplo siguiente muestra cómo aplicar <xref:System.Windows.Controls.Border.Padding%2A> a un elemento primario <xref:System.Windows.Controls.Border> elemento.  
  
 [!code-cpp[MarginPaddingAlignmentSample#3](~/samples/snippets/cpp/VS_Snippets_Wpf/MarginPaddingAlignmentSample/CPP/Margin_Padding_Alignment_Sample.cpp#3)]
 [!code-csharp[MarginPaddingAlignmentSample#3](~/samples/snippets/csharp/VS_Snippets_Wpf/MarginPaddingAlignmentSample/CSharp/Margin_Padding_Alignment_Sample.cs#3)]
 [!code-vb[MarginPaddingAlignmentSample#3](~/samples/snippets/visualbasic/VS_Snippets_Wpf/MarginPaddingAlignmentSample/VisualBasic/MarginPaddingAlignment.vb#3)]
 [!code-xaml[MarginPaddingAlignmentSample#3](~/samples/snippets/xaml/VS_Snippets_Wpf/MarginPaddingAlignmentSample/XAML/default.xaml#3)]  
  
<a name="wcpsdk_layout_amp_summary"></a>   
## <a name="using-alignment-margins-and-padding-in-an-application"></a>Uso de las propiedades Alignment, Margin y Padding en una aplicación  
 <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A>, <xref:System.Windows.FrameworkElement.Margin%2A>, <xref:System.Windows.Controls.Border.Padding%2A>, y <xref:System.Windows.FrameworkElement.VerticalAlignment%2A> proporcionan el control de posicionamiento necesario para crear un complejo [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)]. Puede usar los efectos de cada propiedad para cambiar el posicionamiento de los elementos secundarios, lo que ofrece flexibilidad en la creación de aplicaciones dinámicas y experiencias de usuario.  
  
 En el ejemplo siguiente se muestra cada uno de los conceptos que se detallan en este tema. Partiendo de la infraestructura se encuentra en el primer ejemplo de este tema, este ejemplo se agrega un <xref:System.Windows.Controls.Grid> como elemento secundario de la <xref:System.Windows.Controls.Border> en el primer ejemplo. <xref:System.Windows.Controls.Border.Padding%2A> se aplica al elemento primario <xref:System.Windows.Controls.Border> elemento. El <xref:System.Windows.Controls.Grid> se utiliza para dividir el espacio entre los tres secundarios <xref:System.Windows.Controls.StackPanel> elementos. <xref:System.Windows.Controls.Button> los elementos se vuelven a utilizar para mostrar los distintos efectos de <xref:System.Windows.FrameworkElement.Margin%2A> y <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A>. <xref:System.Windows.Controls.TextBlock> los elementos se agregan a cada <xref:System.Windows.Controls.ColumnDefinition> para definir mejor las distintas propiedades aplicadas a la <xref:System.Windows.Controls.Button> elementos en cada columna.  
  
 [!code-cpp[MarginPaddingAlignmentSample#4](~/samples/snippets/cpp/VS_Snippets_Wpf/MarginPaddingAlignmentSample/CPP/Margin_Padding_Alignment_Sample.cpp#4)]
 [!code-csharp[MarginPaddingAlignmentSample#4](~/samples/snippets/csharp/VS_Snippets_Wpf/MarginPaddingAlignmentSample/CSharp/Margin_Padding_Alignment_Sample.cs#4)]
 [!code-vb[MarginPaddingAlignmentSample#4](~/samples/snippets/visualbasic/VS_Snippets_Wpf/MarginPaddingAlignmentSample/VisualBasic/MarginPaddingAlignment.vb#4)]
 [!code-xaml[MarginPaddingAlignmentSample#4](~/samples/snippets/xaml/VS_Snippets_Wpf/MarginPaddingAlignmentSample/XAML/default.xaml#4)]  
  
 Cuando se compila, la aplicación anterior produce una [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] similar a la de la siguiente ilustración. Los efectos de los distintos valores de propiedad son evidentes en el espacio entre los elementos y valores de propiedad significativos para los elementos de cada columna se muestran entre <xref:System.Windows.Controls.TextBlock> elementos.  
  
 ![Varias propiedades de posicionamiento en una aplicación](./media/layout-margins-padding-aligment-graphic3.PNG "layout_margins_padding_aligment_graphic3")  
  
<a name="wcpsdk_layout_amp_alignment_whatsnext"></a>   
## <a name="whats-next"></a>Pasos adicionales  
 Propiedades de posición definidas por el <xref:System.Windows.FrameworkElement> clase permiten un control preciso de la ubicación del elemento dentro de [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] aplicaciones. Ahora dispone de varias técnicas que puede usar para posicionar mejor los elementos mediante [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
 Existen recursos adicionales que explican el diseño de [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] con mayor detalle. El [información general sobre](../controls/panels-overview.md) tema contiene información más detallada sobre los distintos <xref:System.Windows.Controls.Panel> elementos. El tema [Tutorial: Mi primera aplicación de escritorio de WPF](../getting-started/walkthrough-my-first-wpf-desktop-application.md) presenta técnicas avanzadas que usan elementos de diseño para posicionar componentes y enlazar sus acciones a orígenes de datos.  
  
## <a name="see-also"></a>Vea también

- <xref:System.Windows.FrameworkElement>
- <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A>
- <xref:System.Windows.FrameworkElement.VerticalAlignment%2A>
- <xref:System.Windows.FrameworkElement.Margin%2A>
- [Información general sobre elementos Panel](../controls/panels-overview.md)
- [Diseño](layout.md)
- [Ejemplo WPF Layout Gallery](https://go.microsoft.com/fwlink/?LinkID=160054)
