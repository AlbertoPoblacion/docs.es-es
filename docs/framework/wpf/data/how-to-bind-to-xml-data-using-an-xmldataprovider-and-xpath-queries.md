---
title: 'Cómo: Enlazar a datos XML mediante XMLDataProvider y consultas XPath'
ms.date: 03/30/2017
helpviewer_keywords:
- XmlDataProvider [WPF], binding to XML data
- data binding [WPF], binding to XML data using XmlDataProvider queries
- binding [WPF], to XML data using XmlDataProvider queries
ms.assetid: 7dcd018f-16aa-4870-8e47-c1b4ea31e574
ms.openlocfilehash: 0f39c9d42abfaba1327f2c189ac6ce3d40db6e89
ms.sourcegitcommit: 944ddc52b7f2632f30c668815f92b378efd38eea
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/03/2019
ms.locfileid: "73459213"
---
# <a name="how-to-bind-to-xml-data-using-an-xmldataprovider-and-xpath-queries"></a>Cómo: Enlazar a datos XML mediante XMLDataProvider y consultas XPath
En este ejemplo se muestra cómo enlazar a datos de [!INCLUDE[TLA#tla_xml](../../../../includes/tlasharptla-xml-md.md)] mediante un <xref:System.Windows.Data.XmlDataProvider>.  
  
 Con un <xref:System.Windows.Data.XmlDataProvider>, los datos subyacentes a los que se puede tener acceso a través del enlace de datos de la aplicación pueden ser cualquier árbol de nodos [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)]. En otras palabras, una <xref:System.Windows.Data.XmlDataProvider> proporciona una manera cómoda de usar cualquier árbol de nodos [!INCLUDE[TLA#tla_xml](../../../../includes/tlasharptla-xml-md.md)] como un origen de enlace.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente, los datos se incrustan directamente como una [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] *isla de datos* dentro de la sección <xref:System.Windows.FrameworkElement.Resources%2A>. Una isla de datos [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] se debe encapsular entre etiquetas `<x:XData>` y tener siempre un nodo raíz único, que se corresponde con *Inventory* en este ejemplo.  
  
> [!NOTE]
> El nodo raíz de los datos [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] tiene un atributo **xmlns** que establece el espacio de nombres de [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] en una cadena vacía. Se trata de un requisito para aplicar las consultas XPath a una isla de datos insertada dentro de la página de [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]. En este caso en línea, el [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]y, por tanto, la isla de datos, hereda el espacio de nombres de <xref:System.Windows>. Por este motivo, debe establecer el espacio de nombres en blanco para mantener las consultas XPath calificadas por el espacio de nombres <xref:System.Windows>, que dirigirá erróneamente a las consultas.  
  
 [!code-xaml[XMLDataSource#1](~/samples/snippets/csharp/VS_Snippets_Wpf/XmlDataSource/CS/Window1.xaml#1)]  
  
 Como se muestra en este ejemplo, para crear la misma declaración de enlace en la sintaxis de atributo es preciso crear caracteres de escape correctos para los caracteres especiales. Para más información, consulte [XML Character Entities and XAML](../../xaml-services/xml-character-entities-and-xaml.md) (Entidades de caracteres XML y XAML).  
  
 El <xref:System.Windows.Controls.ListBox> mostrará los siguientes elementos cuando se ejecute este ejemplo. Se trata de los elementos *Title* de todos los elementos que se encuentran bajo *Books* cuyo valor de *Stock* sea "*out*" o cuyo valor de *Number* sea 3 o mayor o igual que 8. Tenga en cuenta que no se devuelve ningún elemento de *CD* porque el valor de <xref:System.Windows.Data.XmlDataProvider.XPath%2A> establecido en el <xref:System.Windows.Data.XmlDataProvider> indica que solo se deben exponer los elementos de los *libros* (estableciendo un filtro en esencia).  
  
 ![Captura de pantalla del ejemplo de XPath que muestra el título de cuatro libros.](./media/how-to-bind-to-xml-data-using-an-xmldataprovider-and-xpath-queries/xpath-example-listbox-details.png)  
  
 En este ejemplo, se muestran los títulos de los libros porque el <xref:System.Windows.Data.Binding.XPath%2A> del enlace de <xref:System.Windows.Controls.TextBlock> en el <xref:System.Windows.DataTemplate> se establece en "*title*". Si desea mostrar el valor de un atributo, como el *ISBN*, debe establecer ese <xref:System.Windows.Data.Binding.XPath%2A> valor en "`@ISBN`".  
  
 El método XmlNode.SelectNodes administra las propiedades **XPath** en [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]. Puede modificar las consultas **XPath** para obtener resultados distintos. Estos son algunos ejemplos de la consulta de <xref:System.Windows.Data.Binding.XPath%2A> en la <xref:System.Windows.Controls.ListBox> enlazada del ejemplo anterior:  
  
- `XPath="Book[1]"` devolverá el primer elemento de libro ("XML in Action"). Tenga en cuenta que los índices de **XPath** se basan en 1, no en 0.  
  
- `XPath="Book[@*]"` devolverá todos los elementos con cualquier atributo.  
  
- `XPath="Book[last()-1]"` devolverá los elementos de libro del segundo al último ("Introducing Microsoft .NET").  
  
- `XPath="*[position()>3]"` devolverá todos los elementos de libro excepto los 3 primeros.  
  
 Al ejecutar una consulta **XPath** , devuelve una <xref:System.Xml.XmlNode> o una lista de XMLNodes. <xref:System.Xml.XmlNode> es un objeto Common Language Runtime (CLR), lo que significa que puede usar la propiedad <xref:System.Windows.Data.Binding.Path%2A> para enlazar a las propiedades Common Language Runtime (CLR). Remítase de nuevo al ejemplo anterior. Si el resto del ejemplo permanece igual y cambia la <xref:System.Windows.Controls.TextBlock> enlace a lo siguiente, verá los nombres de la XmlNodes devuelta en el <xref:System.Windows.Controls.ListBox>. En este caso, el nombre de todos los nodos devueltos es "*Book*".  
  
 [!code-xaml[XmlDataSourceVariation#XmlNodePath](~/samples/snippets/csharp/VS_Snippets_Wpf/XmlDataSourceVariation/CS/Page1.xaml#xmlnodepath)]  
  
 En algunas aplicaciones, puede que no sea conveniente incrustar [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] como una isla de datos dentro del código fuente de la página [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], ya que es imprescindible conocer el contenido exacto de los datos en tiempo de compilación. Por lo tanto, también se admite la obtención de los datos de un archivo [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] externo, como en el ejemplo siguiente:  
  
 [!code-xaml[XMLDataSource2#XmlFileExample](~/samples/snippets/csharp/VS_Snippets_Wpf/XmlDataSource2/CS/Window1.xaml#xmlfileexample)]  
  
 Si los datos de [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] residen en un archivo de [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] remoto, debe definir el acceso a los datos asignando una dirección URL adecuada al atributo <xref:System.Windows.Data.XmlDataProvider.Source%2A> como se indica a continuación:  
  
```xml  
<XmlDataProvider x:Key="BookData" Source="http://MyUrl" XPath="Books"/>  
```  
  
## <a name="see-also"></a>Vea también

- <xref:System.Windows.Data.ObjectDataProvider>
- [Enlazar a los resultados de una consulta LINQ to XML, XDocument o XElement](how-to-bind-to-xdocument-xelement-or-linq-for-xml-query-results.md)
- [Usar el patrón principal-detalle con datos XML jerárquicos](how-to-use-the-master-detail-pattern-with-hierarchical-xml-data.md)
- [Información general sobre orígenes de enlaces](binding-sources-overview.md)
- [Información general sobre el enlace de datos](../../../desktop-wpf/data/data-binding-overview.md)
- [Temas "Cómo..."](data-binding-how-to-topics.md)
