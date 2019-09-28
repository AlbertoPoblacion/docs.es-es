---
title: Documentos en WPF
ms.date: 03/30/2017
helpviewer_keywords:
- documents [WPF], packaging
- documents [WPF], text layout
- documents [WPF], XPS
- 'XPS documents [WPF], , '
- documents [WPF], controls
- documents [WPF], types of
- documents [WPF], browser-viewable
ms.assetid: 6e8db7bc-050a-4070-aa72-bb8c46e87ff8
ms.openlocfilehash: e21abca4dd02a849d0240888f831125ab96aa8f1
ms.sourcegitcommit: da2dd2772fcf32b44eb18b1cbe8affd17b1753c9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/27/2019
ms.locfileid: "71393278"
---
# <a name="documents-in-wpf"></a>Documentos en WPF
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] ofrece una amplia gama de características de documento que permiten la creación de contenido de alta fidelidad diseñado para que se pueda obtener acceso a él y leer con mayor facilidad que en generaciones anteriores de Windows. Además de las capacidades y la calidad mejoradas, [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] también proporciona servicios integrados de presentación, empaquetado y seguridad de documentos. En este tema se proporciona una introducción a los tipos de documentos y el empaquetado de documentos de [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  

<a name="types_of_documents"></a>   
## <a name="types-of-documents"></a>Tipos de documentos  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] divide los documentos en dos categorías amplias según su uso previsto; estas categorías de documentos se denominan "documentos fijos" y "documentos dinámicos".  
  
 Los documentos fijos están diseñados para aplicaciones que requieren una presentación precisa de [!INCLUDE[TLA#tla_wys](../../../../includes/tlasharptla-wys-md.md)], independiente del hardware de pantalla o de impresora utilizado. Entre los usos típicos de los documentos fijos se incluyen la publicación de escritorio, el procesamiento de textos y el diseño de formularios, donde es fundamental no apartarse del diseño de página original. Como parte de su diseño, un documento fijo mantiene la colocación posicional precisa de los elementos de contenido, independientemente de la pantalla o el dispositivo de impresión en uso. Por ejemplo, una página de un documento fijo que se vea en una pantalla de 96 ppp, aparecerá exactamente igual cuando se imprima en una impresora láser de 600 ppp o en un fotocomponedor de 4800 ppp. El diseño de página sigue siendo el mismo en todos los casos, mientras que la calidad del documento se maximiza según las capacidades de cada dispositivo.  
  
 En comparación, los documentos dinámicos están diseñados para optimizar su presentación y legibilidad, y son óptimos para su uso cuando la facilidad de lectura es el escenario de consumo principal del documento. En lugar de establecer un diseño predefinido, los documentos dinámicos ajustan y redistribuyen dinámicamente su contenido basándose en variables en tiempo de ejecución, como el tamaño de la ventana, la resolución del dispositivo y las preferencias opcionales del usuario. Una página web es un ejemplo sencillo de un documento dinámico donde se da formato al contenido de la página de manera dinámica para ajustarse a la ventana actual. Los documentos dinámicos optimizan la experiencia de visualización y lectura para el usuario, según el entorno en tiempo de ejecución. Por ejemplo, el mismo documento dinámico cambiará de formato de manera dinámica para mejorar la legibilidad óptima en una pantalla de 19 pulgadas de alta resolución o en una pantalla de PDA pequeña de 2×3 pulgadas. Además, los documentos dinámicos tienen un número de características integradas, incluida búsqueda, modos de visualización que optimizan la legibilidad y la capacidad de cambiar el tamaño y el aspecto de las fuentes.  Consulte [Información general sobre documentos dinámicos](flow-document-overview.md) para ver ilustraciones, ejemplos e información detallada sobre los documentos dinámicos.  
  
<a name="document_viewer"></a>   
## <a name="document-controls-and-text-layout"></a>Controles de documentos y diseño del texto  
 El .NET Framework proporciona un conjunto de controles pregenerados que simplifican el uso de documentos fijos, documentos dinámicos y texto general dentro de la aplicación.  La presentación del contenido fijo del documento se admite mediante el control <xref:System.Windows.Controls.DocumentViewer>.  Tres controles diferentes admiten la presentación del contenido del documento dinámico: <xref:System.Windows.Controls.FlowDocumentReader>, <xref:System.Windows.Controls.FlowDocumentPageViewer> y <xref:System.Windows.Controls.FlowDocumentScrollViewer> que se asignan a distintos escenarios de usuario (consulte las secciones siguientes).  Otros controles de [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] proporcionan un diseño simplificado para admitir los usos de texto generales (consulte [Texto en la interfaz de usuario](#text_in_the_user_interface) más adelante).  
  
### <a name="fixed-document-control---documentviewer"></a>Control de documentos fijos: DocumentViewer  
 El control <xref:System.Windows.Controls.DocumentViewer> está diseñado para mostrar contenido de <xref:System.Windows.Documents.FixedDocument>. El control <xref:System.Windows.Controls.DocumentViewer> proporciona una interfaz de usuario intuitiva que proporciona compatibilidad integrada para las operaciones comunes, como la salida de impresión, las características copiar en el portapapeles, zoom y búsqueda de texto. El control proporciona acceso a las páginas de contenido a través de un mecanismo de desplazamiento conocido. Al igual que todos los controles [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], <xref:System.Windows.Controls.DocumentViewer> admite el reestilo completo o parcial, lo que permite integrar visualmente el control en prácticamente cualquier aplicación o entorno.  
  
 <xref:System.Windows.Controls.DocumentViewer> está diseñado para mostrar el contenido en modo de solo lectura. la edición o modificación del contenido no está disponible y no se admite.  
  
<a name="flow_document"></a>   
### <a name="flow-document-controls"></a>Controles de documentos dinámicos  

> [!NOTE]
> Para obtener información más detallada sobre las características de los documentos dinámicos y cómo crearlas, consulte [información general sobre documentos dinámicos](flow-document-overview.md).  
  
 Tres controles admiten la presentación del contenido del documento dinámico: <xref:System.Windows.Controls.FlowDocumentReader>, <xref:System.Windows.Controls.FlowDocumentPageViewer> y <xref:System.Windows.Controls.FlowDocumentScrollViewer>.  
  
#### <a name="flowdocumentreader"></a>FlowDocumentReader  
 <xref:System.Windows.Controls.FlowDocumentReader>incluye características que permiten al usuario elegir dinámicamente entre distintos modos de visualización, como el modo de visualización de una sola página (de una página a la vez), un modo de visualización de dos páginas a la vez (formato de lectura de libro) y un modo de visualización de desplazamiento continuo (sin límite).  Para obtener más información acerca de estos modos de <xref:System.Windows.Controls.FlowDocumentReaderViewingMode>visualización, vea.  Si no necesita la capacidad de cambiar dinámicamente entre distintos modos de visualización, <xref:System.Windows.Controls.FlowDocumentPageViewer> y <xref:System.Windows.Controls.FlowDocumentScrollViewer> proporciona visores de contenido dinámico más ligeros que se corrigen en un modo de visualización determinado.  
  
#### <a name="flowdocumentpageviewer-and-flowdocumentscrollviewer"></a>FlowDocumentPageViewer y FlowDocumentScrollViewer  
 <xref:System.Windows.Controls.FlowDocumentPageViewer>muestra el contenido en el modo de visualización de una página a la vez <xref:System.Windows.Controls.FlowDocumentScrollViewer> , mientras que muestra el contenido en modo de desplazamiento continuo.  <xref:System.Windows.Controls.FlowDocumentPageViewer> Y<xref:System.Windows.Controls.FlowDocumentScrollViewer> se corrigen en un modo de visualización determinado. Comparar con <xref:System.Windows.Controls.FlowDocumentReader>, que incluye características que permiten al usuario elegir dinámicamente entre distintos modos de visualización (tal y como lo <xref:System.Windows.Controls.FlowDocumentReaderViewingMode> proporciona la enumeración), a costa de que el uso <xref:System.Windows.Controls.FlowDocumentPageViewer> de <xref:System.Windows.Controls.FlowDocumentScrollViewer>más recursos sea mayor que o.  
  
 De manera predeterminada, siempre se muestra una barra de desplazamiento vertical y una barra de desplazamiento horizontal se vuelve visible cuando es necesario. El valor predeterminado [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] para <xref:System.Windows.Controls.FlowDocumentScrollViewer> no incluye una barra de herramientas; sin embargo, se puede usar la propiedad <xref:System.Windows.Controls.FlowDocumentScrollViewer.IsToolBarVisible%2A> para habilitar una barra de herramientas integrada.  
  
<a name="text_in_the_user_interface"></a>   
### <a name="text-in-the-user-interface"></a>Texto en la interfaz de usuario  
 Además de agregar texto a documentos, el texto, obviamente, puede usarse en la UI de una aplicación, como en formularios. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] incluye varios controles para dibujar texto en la pantalla. Cada control se destina a un escenario diferente y tiene su propia lista de características y limitaciones. En general, se debe usar el elemento <xref:System.Windows.Controls.TextBlock> cuando se requiere compatibilidad de texto limitada, como una frase breve en un [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)]. se puede usar <xref:System.Windows.Controls.Label> cuando se requiere compatibilidad de texto mínima. Para obtener más información, consulte [Información general sobre TextBlock](../controls/textblock-overview.md).  
  
<a name="packaging"></a>   
## <a name="document-packaging"></a>Empaquetado de documentos  
 Las API <xref:System.IO.Packaging> proporcionan un medio eficaz para organizar los datos de la aplicación, el contenido del documento y los recursos relacionados en un único contenedor que es fácil de acceder, portátil y fácil de distribuir. Un archivo ZIP es un ejemplo de un tipo <xref:System.IO.Packaging.Package> capaz de contener varios objetos como una sola unidad. Las API de empaquetado proporcionan una implementación predeterminada <xref:System.IO.Packaging.ZipPackage> diseñada con un estándar de convenciones de empaquetado abierto con la arquitectura de archivos XML y ZIP. Las API de empaquetado de [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] facilitan la creación de paquetes y el almacenamiento y el acceso a objetos dentro de ellos. Un objeto almacenado en un <xref:System.IO.Packaging.Package> se conoce como <xref:System.IO.Packaging.PackagePart> ("parte"). Los paquetes también pueden incluir certificados digitales firmados que pueden utilizarse para identificar al originador de un elemento y para validar que no se ha modificado el contenido de un paquete.  Los paquetes también incluyen una característica <xref:System.IO.Packaging.PackageRelationship> que permite agregar información adicional a un paquete o asociarla a partes específicas sin modificar realmente el contenido de los elementos existentes.  Los servicios de paquete también admiten Microsoft Windows Rights Management (RM).  
  
 La arquitectura de paquetes de [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] sirve como base para varias tecnologías clave:  
  
- Documentos XPS conforme a XML Paper Specification (XPS).  
  
- Documentos XML de formato abierto (.docx) de Microsoft Office "12".  
  
- Formatos de almacenamiento personalizados para su propio diseño de aplicaciones.  
  
 En función de las API de empaquetado, un <xref:System.Windows.Xps.Packaging.XpsDocument> está diseñado específicamente para almacenar documentos de contenido fijo de @no__t 1. Un <xref:System.Windows.Xps.Packaging.XpsDocument> es un documento independiente que se puede abrir en un visor, que se muestra en un control <xref:System.Windows.Controls.DocumentViewer>, se enruta a una cola de impresión o se envía directamente a una impresora compatible con XPS.  
  
 En las secciones siguientes se proporciona información adicional sobre las API <xref:System.IO.Packaging.Package> y <xref:System.Windows.Xps.Packaging.XpsDocument> proporcionadas con [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
<a name="packages"></a>   
### <a name="package-components"></a>Componentes de paquetes  
 Las API de empaquetado de [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] permiten organizar los datos de aplicación y documentos en una sola unidad portátil. Un archivo ZIP es uno de los tipos más comunes de paquetes y es el tipo de paquete predeterminado que se proporciona con [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  <xref:System.IO.Packaging.Package> es una clase abstracta de la que <xref:System.IO.Packaging.ZipPackage> se implementa mediante una arquitectura de archivo XML y ZIP estándar abierta.  El método <xref:System.IO.Packaging.Package.Open%2A> usa <xref:System.IO.Packaging.ZipPackage> para crear y usar archivos ZIP de forma predeterminada. Un paquete puede contener tres tipos básicos de elementos:  
  
|||  
|-|-|  
|<xref:System.IO.Packaging.PackagePart>|Archivos de contenido, datos, documentos y recursos de la aplicación.|  
|<xref:System.IO.Packaging.PackageDigitalSignature>|[Certificado X.509] para la identificación, autenticación y validación.|  
|<xref:System.IO.Packaging.PackageRelationship>|Información agregada relacionada con el paquete o un elemento concreto.|  
  
<a name="PackageParts"></a>   
#### <a name="packageparts"></a>PackageParts  
 Un <xref:System.IO.Packaging.PackagePart> ("parte") es una clase abstracta que hace referencia a un objeto almacenado en un <xref:System.IO.Packaging.Package>. En un archivo ZIP, los elementos del paquete corresponden a los archivos individuales almacenados en el archivo ZIP.  <xref:System.IO.Packaging.ZipPackagePart> proporciona la implementación predeterminada para los objetos serializables almacenados en un <xref:System.IO.Packaging.ZipPackage>.  Al igual que un sistema de archivos, los elementos incluidos en el paquete se almacenan en directorios jerárquicos o en una organización de "estilo de carpetas".  Con las API de empaquetado de [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], las aplicaciones pueden escribir, almacenar y leer varios objetos <xref:System.IO.Packaging.PackagePart> mediante un solo contenedor de archivos ZIP.  
  
<a name="PackageDigitalSignatures"></a>   
#### <a name="packagedigitalsignatures"></a>PackageDigitalSignatures  
 Por seguridad, se puede asociar un <xref:System.IO.Packaging.PackageDigitalSignature> ("firma digital") a los elementos de un paquete. Un <xref:System.IO.Packaging.PackageDigitalSignature> incorpora un [509] que proporciona dos características:  
  
1. Identifica y autentica al originador del elemento.  
  
2. Valida que no se haya modificado el elemento.  
  
 La firma digital no impide que se modifique un elemento, pero no se podrá realizar la comprobación de validación de la firma digital si el elemento se ha modificado de alguna manera. La aplicación, a continuación, puede emprender la acciones apropiadas: por ejemplo, bloquear la apertura del elemento o notificar al usuario que se ha modificado el elemento y que los datos no son seguros.  
  
<a name="PackageRelationships"></a>   
#### <a name="packagerelationships"></a>PackageRelationships  
 Un <xref:System.IO.Packaging.PackageRelationship> ("relación") proporciona un mecanismo para asociar información adicional al paquete o a un elemento dentro del paquete. Una relación es una función de nivel del paquete que puede asociar información adicional a un elemento sin modificar el contenido real del elemento. Insertar directamente nuevos datos en el contenido del elemento no suele ser práctico en muchos casos:  
  
- No se conocen el tipo real del elemento ni su esquema de contenido.  
  
- Incluso si se conocen, el esquema de contenido podría no proporcionar un medio para agregar nueva información.  
  
- El elemento puede estar firmado digitalmente o cifrado, impidiendo cualquier modificación.  
  
 Las relaciones de los paquetes proporcionan un medio reconocible para agregar y asociar información adicional a los elementos individuales o al paquete completo. Las relaciones de los paquetes se utilizan para dos funciones principales:  
  
1. Definir las relaciones de dependencia de un elemento con otro elemento.  
  
2. Definir las relaciones de información que agregan notas u otros datos relacionados con el elemento.  
  
 Un <xref:System.IO.Packaging.PackageRelationship> proporciona un medio rápido y reconocible para definir dependencias y agregar otra información asociada con una parte del paquete o el paquete en su conjunto.  
  
<a name="Dependency_Relationships"></a>   
##### <a name="dependency-relationships"></a>Relaciones de dependencia  
 Las relaciones de dependencia se utilizan para describir las dependencias que mantiene un elemento con otros elementos. Por ejemplo, un paquete puede contener un elemento HTML que incluya una o más etiquetas de imagen \<img>. Las etiquetas de imagen hacen referencia a imágenes que se encuentran en otros elementos internos del paquete o externos al paquete (por ejemplo, a los que se pueda acceder a través de Internet). La creación de un <xref:System.IO.Packaging.PackageRelationship> asociado con el archivo HTML facilita y agiliza la detección y el acceso a los recursos dependientes. Una aplicación de explorador o de visor puede tener acceso directamente a las relaciones entre los elementos y comenzar a ensamblar de inmediato los recursos dependientes sin conocer el esquema ni analizar el documento.  
  
<a name="Information_Relationships"></a>   
##### <a name="information-relationships"></a>Relaciones de información  
 De forma similar a una nota o anotación, un <xref:System.IO.Packaging.PackageRelationship> también puede usarse para almacenar otros tipos de información que se van a asociar a un elemento sin tener que modificar realmente el contenido del elemento.  
  
<a name="XPS_Documents"></a>   
## <a name="xps-documents"></a>Documentos XPS  
 El documento XML Paper Specification (XPS) es un paquete que contiene uno o varios documentos fijos junto con todos los recursos e información necesarios para la representación.  XPS es también el formato de archivo nativo de cola de impresión [!INCLUDE[TLA#tla_winvista](../../../../includes/tlasharptla-winvista-md.md)].  Un <xref:System.Windows.Xps.Packaging.XpsDocument> se almacena en un conjunto de elementos ZIP estándar y puede incluir una combinación de componentes XML y binarios, como archivos de imagen y fuente. Se utilizan [PackageRelationships](#PackageRelationships) para definir las dependencias entre el contenido y los recursos necesarios para representar totalmente el documento.  El diseño de <xref:System.Windows.Xps.Packaging.XpsDocument> proporciona una solución de documento única y de alta fidelidad que admite varios usos:  
  
- Lectura, escritura y almacenamiento de contenido y recursos de documentos fijos como un archivo único portátil y fácil de distribuir.  
  
- Mostrar documentos con la aplicación Visor de XPS.  
  
- Generación de documentos en el formato nativo de salida de cola de impresión de [!INCLUDE[TLA#tla_winvista](../../../../includes/tlasharptla-winvista-md.md)].  
  
- Enrutar documentos directamente a una impresora compatible con XPS.  
  
## <a name="see-also"></a>Vea también

- <xref:System.Windows.Documents.FixedDocument>
- <xref:System.Windows.Documents.FlowDocument>
- <xref:System.Windows.Xps.Packaging.XpsDocument>
- <xref:System.IO.Packaging.ZipPackage>
- <xref:System.IO.Packaging.ZipPackagePart>
- <xref:System.IO.Packaging.PackageRelationship>
- <xref:System.Windows.Controls.DocumentViewer>
- [Texto](optimizing-performance-text.md)
- [Información general sobre documentos dinámicos](flow-document-overview.md)
- [Información general sobre impresión](printing-overview.md)
- [Almacenamiento y serialización de documentos](document-serialization-and-storage.md)
