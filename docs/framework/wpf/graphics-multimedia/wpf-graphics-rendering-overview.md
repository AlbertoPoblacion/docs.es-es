---
title: Información general sobre la representación de gráficos en WPF
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- graphics [WPF], rendering
- rendering graphics [WPF]
ms.assetid: 6dec9657-4d8c-4e46-8c54-40fb80008265
ms.openlocfilehash: 09f5f026ed320aaa253d8cdf6e0b271235aff604
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/07/2019
ms.locfileid: "72004167"
---
# <a name="wpf-graphics-rendering-overview"></a>Información general sobre la representación de gráficos en WPF
En este tema se ofrece información de la capa de objeto visual de [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]. Se centra en el rol de la clase <xref:System.Windows.Media.Visual> para la compatibilidad de representación en el modelo [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  

<a name="role_of_visual_object"></a>   
## <a name="role-of-the-visual-object"></a>Rol del objeto visual  
 La clase <xref:System.Windows.Media.Visual> es la abstracción básica desde la que se derivan todos los objetos <xref:System.Windows.FrameworkElement>. También sirve como punto de entrada para escribir controles nuevos en [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], y en muchos sentidos se puede considerar el identificador de ventana (HWND) del modelo de aplicación de Win32.  
  
 El objeto <xref:System.Windows.Media.Visual> es un objeto Core [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], cuyo rol principal es proporcionar compatibilidad con la representación. Los controles de interfaz de usuario, como <xref:System.Windows.Controls.Button> y <xref:System.Windows.Controls.TextBox>, derivan de la clase <xref:System.Windows.Media.Visual> y lo usan para conservar los datos de representación. El objeto <xref:System.Windows.Media.Visual> proporciona compatibilidad con:  
  
- Presentación de salida: Representar el contenido de dibujo almacenado y serializado de un visual.  
  
- Transformaciones Realizar transformaciones en un visual.  
  
- Salte Proporcionar compatibilidad con la región de recorte para un visual.  
  
- Prueba de posicionamiento: Determinar si una coordenada o geometría está contenida dentro de los límites de un objeto visual.  
  
- Cálculos del cuadro de límite: Determinar el rectángulo delimitador de un visual.  
  
 Sin embargo, el objeto <xref:System.Windows.Media.Visual> no incluye compatibilidad con las características que no son de representación, como:  
  
- Control de eventos  
  
- Diseño  
  
- Estilos  
  
- Enlace de datos  
  
- Globalización  
  
 <xref:System.Windows.Media.Visual> se expone como una clase abstracta pública desde la que se deben derivar las clases secundarias. La siguiente ilustración muestra la jerarquía de los objetos visuales que se exponen en [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
 ![Diagrama de clases derivadas del objeto Visual](./media/wpf-graphics-rendering-overview/classes-derived-visual-object.png)    
  
### <a name="drawingvisual-class"></a>Clase DrawingVisual  
 El <xref:System.Windows.Media.DrawingVisual> es una clase de dibujo ligera que se utiliza para representar formas, imágenes o texto. Esta clase se considera ligera porque no proporciona control de diseño ni control de eventos, lo que mejora su rendimiento en tiempo de ejecución. Por esta razón, los dibujos son ideales para fondos e imágenes prediseñadas. @No__t-0 se puede usar para crear un objeto visual personalizado. Para más información, consulte [Usar objetos DrawingVisual](using-drawingvisual-objects.md).  
  
### <a name="viewport3dvisual-class"></a>Clase Viewport3DVisual  
 El <xref:System.Windows.Media.Media3D.Viewport3DVisual> proporciona un puente entre los objetos 2D <xref:System.Windows.Media.Visual> y <xref:System.Windows.Media.Media3D.Visual3D>. La clase <xref:System.Windows.Media.Media3D.Visual3D> es la clase base para todos los elementos visuales 3D. El <xref:System.Windows.Media.Media3D.Viewport3DVisual> requiere definir un valor <xref:System.Windows.Media.Media3D.Viewport3DVisual.Camera%2A> y un valor <xref:System.Windows.Media.Media3D.Viewport3DVisual.Viewport%2A>. La cámara permite ver la escena. La ventanilla establece el lugar en que se asigna la proyección a la superficie 2D. Para más información acerca de 3D en [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], consulte [Información general sobre gráficos 3D](3-d-graphics-overview.md).  
  
### <a name="containervisual-class"></a>Clase ContainerVisual  
 La clase <xref:System.Windows.Media.ContainerVisual> se utiliza como contenedor para una colección de objetos <xref:System.Windows.Media.Visual>. La clase <xref:System.Windows.Media.DrawingVisual> deriva de la clase <xref:System.Windows.Media.ContainerVisual>, lo que permite que contenga una colección de objetos visuales.  
  
### <a name="drawing-content-in-visual-objects"></a>Dibujo de contenido en objetos visuales  
 Un objeto <xref:System.Windows.Media.Visual> almacena sus datos de representación como una **lista de instrucciones de gráficos vectoriales**. Cada elemento de la lista de instrucciones representa un conjunto de bajo nivel de datos gráficos y recursos asociados en un formato serializado. Hay cuatro tipos diferentes de datos de representación que pueden incluir contenido de dibujo.  
  
|Tipo de contenido de dibujo|Descripción|  
|--------------------------|-----------------|  
|Gráficos vectoriales|Representa los datos de gráficos vectoriales y cualquier información asociada <xref:System.Windows.Media.Brush> y <xref:System.Windows.Media.Pen>.|  
|Image|Representa una imagen dentro de una región definida por un <xref:System.Windows.Rect>.|  
|Glifo|Representa un dibujo que representa un <xref:System.Windows.Media.GlyphRun>, que es una secuencia de glifos de un recurso de fuente especificado. Así es como se representa el texto.|  
|Vídeo|Representa un dibujo que representa vídeo.|  
  
 El <xref:System.Windows.Media.DrawingContext> le permite rellenar un <xref:System.Windows.Media.Visual> con contenido visual. Cuando se usa el comando Draw de un objeto <xref:System.Windows.Media.DrawingContext>, en realidad se almacena un conjunto de datos de representación que el sistema de gráficos usará más adelante; no está dibujando en la pantalla en tiempo real.  
  
 Cuando se crea un control [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], como un <xref:System.Windows.Controls.Button>, el control genera implícitamente los datos de representación para dibujarse. Por ejemplo, al establecer la propiedad <xref:System.Windows.Controls.ContentControl.Content%2A> del <xref:System.Windows.Controls.Button>, el control almacena una representación de representación de un glifo.  
  
 Un <xref:System.Windows.Media.Visual> describe su contenido como uno o varios objetos <xref:System.Windows.Media.Drawing> contenidos dentro de un <xref:System.Windows.Media.DrawingGroup>. Un <xref:System.Windows.Media.DrawingGroup> también describe las máscaras de opacidad, las transformaciones, los efectos de imagen y otras operaciones que se aplican a su contenido. las operaciones <xref:System.Windows.Media.DrawingGroup> se aplican en el siguiente orden cuando se representa el contenido: <xref:System.Windows.Media.DrawingGroup.OpacityMask%2A>, <xref:System.Windows.Media.DrawingGroup.Opacity%2A>, <xref:System.Windows.Media.DrawingGroup.BitmapEffect%2A>, <xref:System.Windows.Media.DrawingGroup.ClipGeometry%2A>, <xref:System.Windows.Media.DrawingGroup.GuidelineSet%2A> y, a continuación, <xref:System.Windows.Media.DrawingGroup.Transform%2A>.  
  
 En la ilustración siguiente se muestra el orden en que se aplican las operaciones <xref:System.Windows.Media.DrawingGroup> durante la secuencia de representación.  
  
 ![Orden de las operaciones de DrawingGroup](./media/graphcismm-drawinggroup-order.png "graphcismm_drawinggroup_order")  
Orden de las operaciones de DrawingGroup  
  
 Para más información, consulte [Información general sobre objetos Drawing](drawing-objects-overview.md).  
  
#### <a name="drawing-content-at-the-visual-layer"></a>Contenido de dibujo en la capa de Visual  
 Nunca se crean instancias directamente de un <xref:System.Windows.Media.DrawingContext>; sin embargo, puede adquirir un contexto de dibujo de determinados métodos, como <xref:System.Windows.Media.DrawingGroup.Open%2A?displayProperty=nameWithType> y <xref:System.Windows.Media.DrawingVisual.RenderOpen%2A?displayProperty=nameWithType>. En el ejemplo siguiente se recupera un <xref:System.Windows.Media.DrawingContext> de un <xref:System.Windows.Media.DrawingVisual> y se usa para dibujar un rectángulo.  
  
 [!code-csharp[drawingvisualsample#101](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingVisualSample/CSharp/Window1.xaml.cs#101)]
 [!code-vb[drawingvisualsample#101](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DrawingVisualSample/visualbasic/window1.xaml.vb#101)]  
  
#### <a name="enumerating-drawing-content-at-the-visual-layer"></a>Enumeración de contenido de dibujo en la capa de Visual  
 Además de sus otros usos, los objetos <xref:System.Windows.Media.Drawing> también proporcionan un modelo de objetos para enumerar el contenido de un <xref:System.Windows.Media.Visual>.  
  
> [!NOTE]
> Cuando se enumera el contenido del objeto visual, se recuperan los objetos <xref:System.Windows.Media.Drawing> y no la representación subyacente de los datos de representación como una lista de instrucciones de gráficos vectoriales.  
  
 En el ejemplo siguiente se usa el método <xref:System.Windows.Media.VisualTreeHelper.GetDrawing%2A> para recuperar el valor <xref:System.Windows.Media.DrawingGroup> de un <xref:System.Windows.Media.Visual> y enumerarlo.  
  
 [!code-csharp[DrawingMiscSnippets_snip#GraphicsMMRetrieveDrawings](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/EnumerateDrawingsExample.xaml.cs#graphicsmmretrievedrawings)]  
  
<a name="how_visual_objects_are_used_to_build_controls"></a>   
## <a name="how-visual-objects-are-used-to-build-controls"></a>Uso de los objetos visuales para compilar controles  
 Muchos de los objetos de [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] están formados por otros objetos visuales, lo que significa que pueden contener diversas jerarquías de objetos descendientes. Muchos de los elementos de la interfaz de usuario de [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], como los controles, constan de varios objetos visuales, que representan diferentes tipos de representación de elementos. Por ejemplo, el control <xref:System.Windows.Controls.Button> puede contener varios objetos, como <xref:Microsoft.Windows.Themes.ClassicBorderDecorator>, <xref:System.Windows.Controls.ContentPresenter> y <xref:System.Windows.Controls.TextBlock>.  
  
 En el código siguiente se muestra un control <xref:System.Windows.Controls.Button> definido en el marcado.  
  
 [!code-xaml[VisualsOverview#VisualsOverviewSnippet1](~/samples/snippets/csharp/VS_Snippets_Wpf/VisualsOverview/CSharp/Window1.xaml#visualsoverviewsnippet1)]  
  
 Si tuviera que enumerar los objetos visuales que componen el control <xref:System.Windows.Controls.Button> predeterminado, encontraría la jerarquía de objetos visuales que se ilustra a continuación:  
  
 ![Diagrama de jerarquía de árbol visual](./media/wpf-graphics-rendering-overview/visual-object-diagram.gif) 
  
 El control <xref:System.Windows.Controls.Button> contiene un elemento <xref:Microsoft.Windows.Themes.ClassicBorderDecorator>, que, a su vez, contiene un elemento @no__t 2. El elemento <xref:Microsoft.Windows.Themes.ClassicBorderDecorator> es responsable de dibujar un borde y un fondo para el <xref:System.Windows.Controls.Button>. El elemento <xref:System.Windows.Controls.ContentPresenter> es responsable de mostrar el contenido del <xref:System.Windows.Controls.Button>. En este caso, como se muestra texto, el elemento <xref:System.Windows.Controls.ContentPresenter> contiene un elemento <xref:System.Windows.Controls.TextBlock>. El hecho de que el control <xref:System.Windows.Controls.Button> Use un <xref:System.Windows.Controls.ContentPresenter> significa que el contenido podría estar representado por otros elementos, como un <xref:System.Windows.Controls.Image> o una geometría, como un <xref:System.Windows.Media.EllipseGeometry>.  
  
### <a name="control-templates"></a>Plantillas de control  
 La clave para la expansión de un control en una jerarquía de controles es la <xref:System.Windows.Controls.ControlTemplate>. Una plantilla de control especifica la jerarquía visual predeterminada de un control. Al hacer referencia explícitamente a un control, implícitamente también se hace referencia a su jerarquía visual. Puede reemplazar los valores predeterminados de una plantilla de control para crear una apariencia visual personalizada para un control. Por ejemplo, puede modificar el valor de color de fondo del control <xref:System.Windows.Controls.Button> para que use un valor de color de degradado lineal en lugar de un valor de color sólido. Para más información, consulte [Button ControlTemplate Example](../controls/button-styles-and-templates.md) (Ejemplo de ControlTemplate de Button).  
  
 Un elemento de la interfaz de usuario, como un control <xref:System.Windows.Controls.Button>, contiene varias listas de instrucciones de gráficos vectoriales que describen toda la definición de representación de un control. En el código siguiente se muestra un control <xref:System.Windows.Controls.Button> definido en el marcado.  
  
 [!code-xaml[VisualsOverview#VisualsOverviewSnippet2](~/samples/snippets/csharp/VS_Snippets_Wpf/VisualsOverview/CSharp/Window1.xaml#visualsoverviewsnippet2)]  
  
 Si tuviera que enumerar los objetos visuales y las listas de instrucciones de gráficos vectoriales que componen el control <xref:System.Windows.Controls.Button>, encontraría la jerarquía de objetos que se ilustra a continuación:  
  
 ![Diagrama de árbol visual y datos de representación](./media/wpf-graphics-rendering-overview/visual-tree-rendering-data.png)  
  
 El control <xref:System.Windows.Controls.Button> contiene un elemento <xref:Microsoft.Windows.Themes.ClassicBorderDecorator>, que, a su vez, contiene un elemento @no__t 2. El elemento <xref:Microsoft.Windows.Themes.ClassicBorderDecorator> es responsable de dibujar todos los elementos gráficos discretos que componen el borde y el fondo de un botón. El elemento <xref:System.Windows.Controls.ContentPresenter> es responsable de mostrar el contenido del <xref:System.Windows.Controls.Button>. En este caso, como se muestra una imagen, el elemento <xref:System.Windows.Controls.ContentPresenter> contiene un elemento <xref:System.Windows.Controls.Image>.  
  
 Hay que tener en cuenta varios aspectos de la jerarquía de objetos visuales y las listas de instrucciones de gráficos vectoriales:  
  
- El orden de la jerarquía representa el orden de procesamiento de la información de dibujo. Desde el elemento del objeto visual raíz, se atraviesa a los elementos secundarios de izquierda a derecha y de arriba a abajo. Si un elemento tiene elementos visuales secundarios, se atraviesan antes que los relacionados del elemento.  
  
- Los elementos de nodo no hoja de la jerarquía, como <xref:System.Windows.Controls.ContentPresenter>, se usan para contener elementos secundarios; no contienen listas de instrucciones.  
  
- Si un elemento visual contiene una lista de instrucciones de gráficos vectoriales y elementos secundarios visuales, la lista de instrucciones del elemento visual primario se representa antes que los dibujos en cualquiera de los objetos visuales secundarios.  
  
- Los elementos de la lista de instrucciones de gráficos vectoriales se representan de izquierda a derecha.  
  
<a name="visual_tree"></a>   
## <a name="visual-tree"></a>Árbol visual  
 El árbol visual contiene todos los elementos visuales que se usan en la interfaz de usuario de una aplicación. Puesto que un elemento visual contiene información guardada del dibujo, el árbol visual se puede considerar un gráfico de la escena, que contiene toda la información de representación necesaria para componer la salida de la pantalla. Este árbol es la acumulación de todos los elementos visuales creados directamente por la aplicación, ya sea a través de código o de marcación. El árbol visual también contiene todos los elementos visuales que ha creado la expansión de la plantilla de elementos, como controles y objetos de datos.  
  
 En el código siguiente se muestra un elemento <xref:System.Windows.Controls.StackPanel> definido en el marcado.  
  
 [!code-xaml[VisualsOverview#VisualsOverviewSnippet3](~/samples/snippets/csharp/VS_Snippets_Wpf/VisualsOverview/CSharp/Window1.xaml#visualsoverviewsnippet3)]  
  
 Si tuviera que enumerar los objetos visuales que componen el elemento <xref:System.Windows.Controls.StackPanel> en el ejemplo de marcación, encontraría la jerarquía de objetos visuales que se ilustra a continuación:  
  
 ![Diagrama de jerarquía de árbol visual](./media/wpf-graphics-rendering-overview/visual-tree-hierarchy.gif)  
  
### <a name="rendering-order"></a>Orden de representación  
 El árbol visual determina el orden de representación de objetos visuales y de dibujo de [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]. El orden del recorrido comienza con el objeto visual raíz, que es el nodo de nivel superior del árbol visual. A continuación, se atraviesan los elementos secundarios del objeto visual raíz, de izquierda a derecha. Si un objeto visual tiene elementos secundarios, estos se atraviesan antes que los elementos del mismo nivel del objeto visual. Esto significa que el contenido de un objeto visual secundario se representa delante del contenido propio del objeto visual.  
  
 ![Diagrama del orden de representación del árbol visual](./media/wpf-graphics-rendering-overview/visual-tree-rendering-order.gif) 
  
### <a name="root-visual"></a>Objeto visual raíz  
 El **objeto visual raíz** es el elemento de nivel superior de una jerarquía de árbol visual. En la mayoría de las aplicaciones, la clase base del valor visual raíz es <xref:System.Windows.Window> o <xref:System.Windows.Navigation.NavigationWindow>. Sin embargo, si se hospedaran objetos visuales en una aplicación Win32, el objeto visual raíz sería el objeto visual de nivel superior que se hospeda en la ventana de Win32. Para obtener más información, consulte [Tutorial: Hospedar objetos visuales en una aplicación Win32 @ no__t-0.  
  
### <a name="relationship-to-the-logical-tree"></a>Relación con el árbol lógico  
 El árbol lógico de [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] representa los elementos de una aplicación en tiempo de ejecución. Aunque no manipula directamente este árbol, esta vista de la aplicación es útil para entender la herencia de propiedades y el enrutamiento de eventos. A diferencia del árbol visual, el árbol lógico puede representar objetos de datos no visuales, como <xref:System.Windows.Documents.ListItem>. En muchos casos, el árbol lógico se asigna muy estrechamente con las definiciones de marcación de una aplicación. En el código siguiente se muestra un elemento <xref:System.Windows.Controls.DockPanel> definido en el marcado.  
  
 [!code-xaml[VisualsOverview#VisualsOverviewSnippet5](~/samples/snippets/csharp/VS_Snippets_Wpf/VisualsOverview/CSharp/Window1.xaml#visualsoverviewsnippet5)]  
  
 Si tuviera que enumerar los objetos lógicos que componen el elemento <xref:System.Windows.Controls.DockPanel> en el ejemplo de marcación, encontraría la jerarquía de objetos lógicos que se ilustra a continuación:  
  
 ![Diagrama de árbol](./media/tree1-wcp.gif "Tree1_wcp")  
Diagrama de árbol lógico  
  
 El árbol visual y el árbol lógico se sincronizan con el conjunto actual de elementos de la aplicación, que refleja cualquier adición, eliminación o modificación de elementos. Sin embargo, los árboles presentan distintas vistas de la aplicación. A diferencia del árbol visual, el árbol lógico no expande el elemento <xref:System.Windows.Controls.ContentPresenter> de un control. Esto significa que no hay una correspondencia uno a uno directa entre un árbol lógico y un árbol visual del mismo conjunto de objetos. De hecho, al invocar el método <xref:System.Windows.LogicalTreeHelper.GetChildren%2A> del objeto **LogicalTreeHelper** y el método <xref:System.Windows.Media.VisualTreeHelper.GetChild%2A> del objeto **VisualTreeHelper** con el mismo elemento que un parámetro, se generan resultados diferentes.  
  
 Para más información acerca del árbol lógico, consulte [Árboles en WPF](../advanced/trees-in-wpf.md).  
  
### <a name="viewing-the-visual-tree-with-xamlpad"></a>Visualización del árbol visual con XamlPad  
 La herramienta [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], XamlPad, proporciona una opción para ver y explorar el árbol visual que corresponde al contenido XAML definido actualmente. Haga clic en el botón **Show Visual Tree** (Mostrar árbol visual) de la barra de menús para mostrar el árbol visual. A continuación se muestra la expansión de contenido XAML en nodos de árbol visual en el panel del **Explorador de árbol visual** de XamlPad:  
  
 ![Panel del explorador de árbol visual en XamlPad](./media/wpf-graphics-rendering-overview/visual-tree-explorer.png)  

 Observe cómo los controles <xref:System.Windows.Controls.Label>, <xref:System.Windows.Controls.TextBox> y <xref:System.Windows.Controls.Button> muestran una jerarquía de objetos visuales independiente en el panel del **Explorador de árbol visual** de XamlPad. Esto se debe a que los controles [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] tienen un <xref:System.Windows.Controls.ControlTemplate> que contiene el árbol visual de ese control. Al hacer referencia explícitamente a un control, implícitamente también se hace referencia a su jerarquía visual.  
  
### <a name="profiling-visual-performance"></a>Generación de perfiles de rendimiento visual  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] ofrece un conjunto de herramientas de generación de perfiles de rendimiento que le permiten analizar el comportamiento en tiempo de ejecución de la aplicación y determinar los tipos de optimizaciones de rendimiento que puede aplicar. La herramienta Generador de perfiles visuales proporciona una vista gráfica completa de los datos de rendimiento mediante la asignación al árbol visual de la aplicación. En esta captura de pantalla, la sección **Uso de CPU** del generador de perfiles visuales proporciona un desglose preciso del uso que un objeto realiza de los servicios de [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], como la representación y el diseño.  
  
 (./media/wpfperf-visualprofiler-04.png "WPFPerf_VisualProfiler_04") de ![salida de visualización de Visual Profiler]  
Resultados del generador de perfiles visuales  
  
<a name="visual_rendering_behavior"></a>   
## <a name="visual-rendering-behavior"></a>Comportamiento de la representación visual  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] presenta varias características que afectan al comportamiento de la representación de los objetos visuales: gráficos en modo retenido, gráficos vectoriales y gráficos independientes del dispositivo.  
  
### <a name="retained-mode-graphics"></a>Gráficos en modo retenido  
 Una de las claves para conocer el rol del objeto visual es conocer la diferencia entre los sistemas de gráficos del **modo inmediato** y del **modo retenido**. Una aplicación Win32 estándar basada en GDI o GDI + utiliza un sistema de gráficos de modo inmediato. Esto significa que la aplicación es responsable de volver a dibujar la parte del área de cliente que se ha invalidado, debido a una acción, como el cambio de tamaño de una ventana o al cambio de la apariencia visual de un objeto.  
  
 ![Diagrama de secuencia de representación de Win32](./media/wpf-graphics-rendering-overview/win32-rendering-squence.png)  
  
 En cambio, [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] utiliza un sistema de modo retenido. Esto significa que los objetos de la aplicación que tienen una apariencia visual definen un conjunto de datos de dibujo serializados. Una vez que se definen los datos de dibujo, el sistema es responsable de responder a todas las solicitudes de repetición del dibujo para representar los objetos de la aplicación. Incluso en tiempo de ejecución, puede modificar o crear objetos de la aplicación y seguir confiando en que el sistema responderá a las solicitudes de dibujo. La eficacia de un sistema de gráficos en modo retenido es que la aplicación guarda siempre la información de dibujo en un estado serializado, pero la responsabilidad de la representación se deja al sistema. El siguiente diagrama muestra la forma en que la aplicación usa [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] para responder a las solicitudes de dibujo.  
  
 ![Diagrama de secuencia de representación de WPF](./media/wpf-graphics-rendering-overview/wpf-rendering-sequence.png)  

#### <a name="intelligent-redrawing"></a>Volver a dibujar de forma inteligente  
 Una de las mayores ventajas de utilizar gráficos en modo retenido es que [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] puede optimizar eficazmente lo que hay que volver a dibujar en la aplicación. Aunque tenga una escena compleja con diferentes niveles de opacidad, por lo general no es preciso escribir código especial para optimizar el redibujado. Compárelo esto con la programación de Win32, en la que se puede dedicar mucho esfuerzo a optimizar la aplicación mediante la minimización de la cantidad de redibujado que se realiza en la región de actualización. Consulte [Redrawing in the Update Region](/windows/desktop/gdi/redrawing-in-the-update-region) (Redibujado en la región de actualización) para obtener un ejemplo del tipo de complejidad implicado en la optimización del redibujado en las aplicaciones de Win32.  
  
### <a name="vector-graphics"></a>Gráficos vectoriales  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] usa **gráficos vectoriales** como formato de los datos de representación. Los gráficos vectoriales, que incluyen Scalable Vector Graphics (SVG), metarchivos de Windows (.wmf) y fuentes TrueType, almacenan datos de representación y los transmiten como una lista de instrucciones que describen cómo volver a crear una imagen mediante primitivas de gráficos. Por ejemplo, las fuentes TrueType son fuentes de esquema que describen un conjunto de líneas, curvas y comandos, en lugar de una matriz de píxeles. Una de las ventajas principales de los gráficos vectoriales es su capacidad para escalar a cualquier tamaño y resolución.  
  
 A diferencia de los gráficos vectoriales, los gráficos de mapa de bits almacenan los datos de representación como una representación píxel a píxel de una imagen, previamente representada para una resolución específica. Una de las principales diferencias entre los formatos de gráficos vectoriales y de mapa de bits es la fidelidad con la imagen original. Por ejemplo, cuando se modifica el tamaño de una imagen de origen, los sistemas de gráficos de mapa de bits ajustan la imagen, mientras que los sistemas de gráficos vectoriales la escalan, lo que mantiene su fidelidad.  
  
 La ilustración siguiente muestra una imagen de origen cuyo tamaño se ha cambiado en un 300 %. Observe las distorsiones que aparecen cuando la imagen de origen es un gráfico de mapa de bits y se ajusta, en lugar de escalarse como imagen de gráfico vectorial.  
  
 ![Diferencias entre gráficos de trama y vectoriales](./media/wpf-graphics-rendering-overview/raster-vector-differences.png)  
  
 El marcado siguiente muestra dos elementos <xref:System.Windows.Shapes.Path> definidos. El segundo elemento usa un <xref:System.Windows.Media.ScaleTransform> para cambiar el tamaño de las instrucciones de dibujo del primer elemento en un 300%. Observe que las instrucciones de dibujo de los elementos <xref:System.Windows.Shapes.Path> permanecen sin cambios.  
  
 [!code-xaml[VectorGraphicsSnippets#VectorGraphicsSnippet1](~/samples/snippets/csharp/VS_Snippets_Wpf/VectorGraphicsSnippets/CS/PageOne.xaml#vectorgraphicssnippet1)]  
  
### <a name="about-resolution-and-device-independent-graphics"></a>Acerca de los gráficos independientes de la resolución y del dispositivo  
 Hay dos factores del sistema que determinan el tamaño tanto del texto como de los gráficos en la pantalla: la resolución y los puntos por pulgada. La resolución describe el número de píxeles que aparecen en la pantalla. A medida que aumenta la resolución, disminuye el tamaño de los píxeles, lo que provoca que tanto los gráficos como el texto parezcan menores. Un gráfico que se muestre en un monitor cuya resolución se haya configurado en 1024 x 768 píxeles parecerá mucho más pequeño cuando dicha resolución se cambie a 1600 x 1200.  
  
 La otra configuración del sistema, los puntos por pulgada (ppp), describe el tamaño de una pulgada de pantalla, en píxeles. La mayoría de los sistemas de Windows tienen un PPP de 96, lo que significa que una pulgada de pantalla es de 96 píxeles. El aumento de la configuración de PPP aumenta el tamaño de la pulgada de la pantalla; mientras que su disminución lo reduce, lo que significa que una pulgada de la pantalla no es el mismo tamaño que una pulgada real; en la mayoría de los sistemas, es probable que no lo sea. A medida que se aumente el valor de PPP, tanto el texto como los gráficos con reconocimiento de PPP serán mayores, ya que se ha incrementado el tamaño de la pulgada de pantalla. El aumento del valor de PPP puede facilitar la lectura del texto, especialmente en resoluciones altas.  
  
 No todas las aplicaciones reconocen el PPP: algunas utilizan los píxeles de hardware como unidad de medida principal; por consiguiente, el cambio de los PPP del sistema no tiene ningún efecto en dichas aplicaciones. Muchas otras aplicaciones utilizan unidades con reconocimiento de PPP para describir los tamaños de fuente, pero usan píxeles para describir todo lo demás. Un valor de PPP es demasiado pequeño o demasiado grande puede provocar problemas de diseño en estas aplicaciones, ya que el texto de las aplicaciones se escala con la configuración de PPP del sistema, mientras que su interfaz de usuario no lo hace. Este problema se ha eliminado en las aplicaciones desarrolladas mediante [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] admite el escalado automático mediante el uso del píxel independiente del dispositivo como unidad de medida principal, en lugar de los píxeles de hardware; tanto el texto como los gráficos se escalan correctamente sin que el desarrollador de la aplicación tenga que realizar ningún trabajo adicional. La siguiente ilustración muestra un ejemplo de cómo aparecen tanto el texto como los gráficos de [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] con diferentes configuraciones de PPP.  
  
 ![Gráficos y texto con diferentes configuraciones de PPP](./media/graphicsmm-dpi-setting-examples.png "graphicsmm_dpi_setting_examples")  
Gráficos y texto con diferentes configuraciones de PPP  
  
<a name="visualtreehelper_class"></a>   
## <a name="visualtreehelper-class"></a>Clase VisualTreeHelper  
 La clase <xref:System.Windows.Media.VisualTreeHelper> es una clase auxiliar estática que proporciona funcionalidad de bajo nivel para programar en el nivel de objeto visual, lo que resulta útil en escenarios muy concretos, como el desarrollo de controles personalizados de alto rendimiento. En la mayoría de los casos, los objetos de .NET Framework de nivel superior [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], como <xref:System.Windows.Controls.Canvas> y <xref:System.Windows.Controls.TextBlock>, ofrecen mayor flexibilidad y facilidad de uso.  
  
### <a name="hit-testing"></a>Pruebas de posicionamiento  
 La clase <xref:System.Windows.Media.VisualTreeHelper> proporciona métodos para realizar pruebas de posicionamiento en objetos visuales cuando la compatibilidad con la prueba de posicionamiento predeterminada no satisface sus necesidades. Puede usar los métodos <xref:System.Windows.Media.VisualTreeHelper.HitTest%2A> de la clase <xref:System.Windows.Media.VisualTreeHelper> para determinar si una geometría o un valor de coordenadas de punto está dentro del límite de un objeto determinado, como un control o un elemento gráfico. Por ejemplo, las pruebas de posicionamiento se pueden utilizar para determinar si un clic del mouse dentro del rectángulo delimitador de un objeto pertenece a la geometría de un círculo. También puede elegir invalidar la implementación predeterminada de las pruebas de posicionamiento para realizar sus propios cálculos de las pruebas de posicionamiento.  
  
 Para más información acerca de las pruebas de posicionamiento, consulte [Hit Testing in the Visual Layer](hit-testing-in-the-visual-layer.md) (Pruebas de posicionamiento en la capa visual).  
  
### <a name="enumerating-the-visual-tree"></a>Enumeración del árbol visual  
 La clase <xref:System.Windows.Media.VisualTreeHelper> proporciona la funcionalidad para enumerar los miembros de un árbol visual. Para recuperar un elemento primario, llame al método <xref:System.Windows.Media.VisualTreeHelper.GetParent%2A>. Para recuperar un elemento secundario o un descendiente directo de un objeto visual, llame al método <xref:System.Windows.Media.VisualTreeHelper.GetChild%2A>. Este método devuelve un elemento secundario <xref:System.Windows.Media.Visual> del elemento primario en el índice especificado.  
  
 En el ejemplo siguiente se muestra cómo enumerar todos los descendientes de un objeto visual, que es una técnica que se puede utilizar si se desea serializar toda la información de representación de una jerarquía de objetos visuales.  
  
 [!code-csharp[VisualsOverview#101](~/samples/snippets/csharp/VS_Snippets_Wpf/VisualsOverview/CSharp/Window1.xaml.cs#101)]
 [!code-vb[VisualsOverview#101](~/samples/snippets/visualbasic/VS_Snippets_Wpf/VisualsOverview/visualbasic/window1.xaml.vb#101)]  
  
 En la mayoría de los casos, el árbol lógico es una representación más útil de los elementos de una aplicación de [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]. Aunque no se modifique directamente el árbol lógico, esta vista de la aplicación es útil para entender la herencia de propiedades y el enrutamiento de eventos. A diferencia del árbol visual, el árbol lógico puede representar objetos de datos no visuales, como <xref:System.Windows.Documents.ListItem>. Para más información acerca del árbol lógico, consulte [Árboles en WPF](../advanced/trees-in-wpf.md).  
  
 La clase <xref:System.Windows.Media.VisualTreeHelper> proporciona métodos para devolver el rectángulo delimitador de objetos visuales. Puede devolver el rectángulo delimitador de un objeto visual llamando a <xref:System.Windows.Media.VisualTreeHelper.GetContentBounds%2A>. Puede devolver el rectángulo delimitador de todos los descendientes de un objeto visual, incluido el propio objeto visual, llamando a <xref:System.Windows.Media.VisualTreeHelper.GetDescendantBounds%2A>. El código siguiente muestra cómo se calcularía el rectángulo delimitador de un objeto visual y todos sus descendientes.  
  
 [!code-csharp[VisualsOverview#102](~/samples/snippets/csharp/VS_Snippets_Wpf/VisualsOverview/CSharp/Window1.xaml.cs#102)]
 [!code-vb[VisualsOverview#102](~/samples/snippets/visualbasic/VS_Snippets_Wpf/VisualsOverview/visualbasic/window1.xaml.vb#102)]  
  
## <a name="see-also"></a>Vea también

- <xref:System.Windows.Media.Visual>
- <xref:System.Windows.Media.VisualTreeHelper>
- <xref:System.Windows.Media.DrawingVisual>
- [Imágenes y gráficos 2D](../advanced/optimizing-performance-2d-graphics-and-imaging.md)
- [Realizar pruebas de posicionamiento en la capa visual](hit-testing-in-the-visual-layer.md)
- [Usar objetos DrawingVisual](using-drawingvisual-objects.md)
- [Tutorial: Hospedar objetos visuales en una aplicación Win32 @ no__t-0
- [Optimizar WPF: Rendimiento de aplicaciones](../advanced/optimizing-wpf-application-performance.md)
