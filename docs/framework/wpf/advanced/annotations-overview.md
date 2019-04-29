---
title: Información general sobre anotaciones
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- highlights [WPF]
- documents [WPF], annotations
- sticky notes [WPF]
ms.assetid: 716bf474-29bd-4c74-84a4-8e0744bdad62
ms.openlocfilehash: faf2e9bbe23acfd46ee98e1f0fca01b7563ede73
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61777344"
---
# <a name="annotations-overview"></a>Información general sobre anotaciones
Escribir notas o comentarios en documentos impresos es una actividad tan habitual que prácticamente la subestimamos. Las notas o los comentarios son "anotaciones" que se agregan a un documento para marcar información o resaltar elementos de interés para su posterior referencia. Aunque escribir notas en documentos impresos es fácil y habitual, la capacidad de agregar comentarios personales a documentos electrónicos, si la hay, suele ser muy limitada.  
  
 En este tema se revisan varios tipos comunes de anotaciones, en particular las notas rápidas y el resaltado y se muestra cómo el [!INCLUDE[TLA#tla_caf](../../../../includes/tlasharptla-caf-md.md)] facilita estos tipos de anotaciones en las aplicaciones a través de los documentos de Windows Presentation Foundation (WPF) los controles de visualización.  [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] los controles de visualización del documento que admiten las anotaciones incluyen <xref:System.Windows.Controls.FlowDocumentReader> y <xref:System.Windows.Controls.FlowDocumentScrollViewer>, así como controles derivados de <xref:System.Windows.Controls.Primitives.DocumentViewerBase> como <xref:System.Windows.Controls.DocumentViewer> y <xref:System.Windows.Controls.FlowDocumentPageViewer>.  

<a name="caf1_type_stickynotes"></a>   
## <a name="sticky-notes"></a>Notas rápidas  
 Una nota rápida típica contiene la información escrita en un pequeño trozo de papel de color que se "pega" en un documento. Las notas rápidas digitales proporcionan una funcionalidad similar para los documentos electrónicos, pero con la flexibilidad agregada de incluir muchos otros tipos de contenido, como texto escrito, notas manuscritas (por ejemplo, trazos de "lápiz" de [!INCLUDE[TLA#tla_tpc](../../../../includes/tlasharptla-tpc-md.md)]) o vínculos web.  
  
 La siguiente ilustración muestra algunos ejemplos de anotaciones de resaltado, notas rápidas de texto y notas rápidas de lápiz.  
  
 ![Anotaciones de resaltado, notas rápidas de texto y notas rápidas de lápiz.](./media/caf-stickynote.jpg "CAF_StickyNote")  
  
 En el ejemplo siguiente se muestra el método que puede usar para habilitar la compatibilidad con las anotaciones de la aplicación.  
  
 [!code-csharp[DocViewerAnnotationsXml#DocViewXmlStartAnnotations](~/samples/snippets/csharp/VS_Snippets_Wpf/DocViewerAnnotationsXml/CSharp/Window1.xaml.cs#docviewxmlstartannotations)]
 [!code-vb[DocViewerAnnotationsXml#DocViewXmlStartAnnotations](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DocViewerAnnotationsXml/visualbasic/window1.xaml.vb#docviewxmlstartannotations)]  
  
<a name="caf1_type_callouts"></a>   
## <a name="highlights"></a>Resaltados  
 Las personas usan métodos creativos para atraer la atención a los elementos de interés cuando marcan un documento impreso, como subrayar, resaltar, rodear palabras de una frase con un círculo o dibujar marcas o notaciones en el margen.  Las anotaciones de resaltado de [!INCLUDE[TLA#tla_caf](../../../../includes/tlasharptla-caf-md.md)] ofrecen una característica similar para marcar la información que se muestra en los controles de visualización de documentos de [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)].  
  
 En la ilustración siguiente se muestra un ejemplo de una anotación de resaltado.  
  
 ![Anotación de resaltado](./media/caf-callouts.png "CAF_Callouts")  
  
 Los usuarios suelen crear anotaciones, seleccione primero algún texto o un elemento de interés y, a continuación, con el botón secundario para mostrar un <xref:System.Windows.Controls.ContextMenu> de opciones de anotación.  El ejemplo siguiente se muestra el [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] puede utilizar para declarar un <xref:System.Windows.Controls.ContextMenu> con comandos enrutados que pueden tener acceso los usuarios para crear y administrar anotaciones.  
  
 [!code-xaml[DocViewerAnnotationsXps#CreateDeleteAnnotations](~/samples/snippets/csharp/VS_Snippets_Wpf/DocViewerAnnotationsXps/CSharp/Window1.xaml#createdeleteannotations)]  
  
<a name="caf1_framework_data_anchoring"></a>   
## <a name="data-anchoring"></a>Delimitación de datos  
 [!INCLUDE[TLA2#tla_caf](../../../../includes/tla2sharptla-caf-md.md)] enlaza las anotaciones a los datos que el usuario selecciona, no solo a una posición en la vista de presentación. Por lo tanto, si la vista del documento cambia, por ejemplo cuando el usuario se desplaza por la ventana de presentación o cambia su tamaño, la anotación permanece con la selección de datos a la que está enlazada. Por ejemplo, el siguiente gráfico ilustra una anotación que el usuario realizó en una selección de texto. Cuando el documento observa cambios (desplazamiento, cambio de tamaño, escalado u otros movimientos), la anotación de resaltado se mueve con la selección de datos original.  
  
 ![Delimitación de datos de anotación](./media/caf-dataanchoring.png "CAF_DataAnchoring")  
  
<a name="matching_annotations_with_annotated_objects"></a>   
## <a name="matching-annotations-with-annotated-objects"></a>Coincidencia de anotaciones con objetos anotados  
 Puede hacer coincidir las anotaciones con los objetos anotados correspondientes. Por ejemplo, considere una aplicación de lector de documentos simple que tiene un panel de comentarios. El panel de comentarios podría ser un cuadro de lista que muestra el texto de una lista de anotaciones ancladas a un documento. Si el usuario selecciona un elemento en el cuadro de lista, la aplicación muestra el párrafo del documento al que está anclado el objeto de anotación correspondiente.  
  
 En el ejemplo siguiente se muestra cómo implementar el controlador de eventos de un cuadro de lista como este que sirve de panel de comentarios.  
  
 [!code-csharp[FlowDocumentAnnotatedViewer#Handler](~/samples/snippets/csharp/VS_Snippets_Wpf/FlowDocumentAnnotatedViewer/CSharp/Window1.xaml.cs#handler)]
 [!code-vb[FlowDocumentAnnotatedViewer#Handler](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FlowDocumentAnnotatedViewer/visualbasic/window1.xaml.vb#handler)]  
  
 Otro ejemplo de escenario implica las aplicaciones que permiten el intercambio de anotaciones y notas rápidas entre los lectores de documentos por correo electrónico. Esta característica permite que estas aplicaciones naveguen en el lector hasta la página que contiene la anotación que se está intercambiando.  
  
## <a name="see-also"></a>Vea también

- <xref:System.Windows.Controls.Primitives.DocumentViewerBase>
- <xref:System.Windows.Controls.DocumentViewer>
- <xref:System.Windows.Controls.FlowDocumentPageViewer>
- <xref:System.Windows.Controls.FlowDocumentScrollViewer>
- <xref:System.Windows.Controls.FlowDocumentReader>
- <xref:System.Windows.Annotations.IAnchorInfo>
- [Esquema en anotaciones](annotations-schema.md)
- [Información general sobre ContextMenu](../controls/contextmenu-overview.md)
- [Información general sobre comandos](commanding-overview.md)
- [Información general sobre documentos dinámicos](flow-document-overview.md)
- [Cómo: Agregar un comando a un elemento de menú](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms741839(v=vs.90))
