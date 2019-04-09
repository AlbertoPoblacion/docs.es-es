---
title: Filtrar Enlazar a los resultados de una consulta LINQ to XML, XDocument o XElement
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- data binding [WPF], binding to XDocument
- data binding [WPF], binding to XElement
ms.assetid: 6a629a49-fe1c-465d-b76a-3dcbf4307b64
ms.openlocfilehash: afecb87dcfce1a8c48f1b2108edeae3cfd2aa16f
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2019
ms.locfileid: "59209663"
---
# <a name="how-to-bind-to-xdocument-xelement-or-linq-for-xml-query-results"></a>Filtrar Enlazar a los resultados de una consulta LINQ to XML, XDocument o XElement
En este ejemplo muestra cómo enlazar datos XML a un <xref:System.Windows.Controls.ItemsControl> mediante <xref:System.Xml.Linq.XDocument>.  
  
## <a name="example"></a>Ejemplo  
 El código XAML siguiente define un <xref:System.Windows.Controls.ItemsControl> e incluye una plantilla de datos para los datos de tipo `Planet` en el `http://planetsNS` espacio de nombres XML. Un tipo de datos XML que ocupa un espacio de nombres debe incluir el espacio de nombres entre llaves y, si aparece donde podría aparecer una extensión de marcado XAML, debe preceder al espacio de nombres con una secuencia de escape de llaves. Este código enlaza a las propiedades dinámicas que corresponden a la <xref:System.Xml.Linq.XContainer.Element%2A> y <xref:System.Xml.Linq.XElement.Attribute%2A> métodos de la <xref:System.Xml.Linq.XElement> clase. Las propiedades dinámicas permiten a XAML enlazar a las propiedades dinámicas que comparten los nombres de los métodos. Para más información, consulte [Propiedades dinámicas de LINQ to XML](/visualstudio/designers/linq-to-xml-dynamic-properties). Tenga en cuenta cómo la declaración de espacio de nombres predeterminada para XML no se aplica a los nombres de atributo.  
  
 [!code-xaml[XLinqExample#StackPanelResources](~/samples/snippets/csharp/VS_Snippets_Wpf/XLinqExample/CSharp/Window1.xaml#stackpanelresources)]  
[!code-xaml[XLinqExample#ItemsControl](~/samples/snippets/csharp/VS_Snippets_Wpf/XLinqExample/CSharp/Window1.xaml#itemscontrol)]  
  
 Las siguientes llamadas de código de C# <xref:System.Xml.Linq.XDocument.Load%2A> y establece el contexto de datos del panel de pila en todos los subelementos del elemento denominado `SolarSystemPlanets` en el `http://planetsNS` espacio de nombres XML.  
  
 [!code-csharp[XLinqExample#LoadDCFromFile](~/samples/snippets/csharp/VS_Snippets_Wpf/XLinqExample/CSharp/Window1.xaml.cs#loaddcfromfile)]
 [!code-vb[XLinqExample#LoadDCFromFile](~/samples/snippets/visualbasic/VS_Snippets_Wpf/XLinqExample/visualbasic/window1.xaml.vb#loaddcfromfile)]  
  
 Datos XML pueden almacenarse como recurso XAML mediante <xref:System.Windows.Data.ObjectDataProvider>. Para obtener un ejemplo completo, vea [código fuente de L2DBForm.xaml](/visualstudio/designers/l2dbform-xaml-source-code). En el ejemplo siguiente se muestra cómo el código puede establecer el contexto de datos en un recurso de objetos.  
  
 [!code-csharp[XLinqExample#LoadDCFromXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/XLinqExample/CSharp/Window1.xaml.cs#loaddcfromxaml)]
 [!code-vb[XLinqExample#LoadDCFromXAML](~/samples/snippets/visualbasic/VS_Snippets_Wpf/XLinqExample/visualbasic/window1.xaml.vb#loaddcfromxaml)]  
  
 Las propiedades dinámicas que se asignan a <xref:System.Xml.Linq.XContainer.Element%2A> y <xref:System.Xml.Linq.XElement.Attribute%2A> proporcionan flexibilidad dentro de XAML. El código también puede enlazar a los resultados de una consulta LINQ to XML. Este ejemplo enlaza a los resultados de la consulta ordenados por un valor de elemento.  
  
 [!code-csharp[XLinqExample#BindToResults](~/samples/snippets/csharp/VS_Snippets_Wpf/XLinqExample/CSharp/Window1.xaml.cs#bindtoresults)]
 [!code-vb[XLinqExample#BindToResults](~/samples/snippets/visualbasic/VS_Snippets_Wpf/XLinqExample/visualbasic/window1.xaml.vb#bindtoresults)]  
  
## <a name="see-also"></a>Vea también

- [Información general sobre orígenes de enlaces](binding-sources-overview.md)
- [Información general de enlace de datos WPF con LINQ to XML](/visualstudio/designers/wpf-data-binding-with-linq-to-xml-overview)
- [Ejemplo de enlace de datos WPF utilizando LINQ to XML](/visualstudio/designers/wpf-data-binding-using-linq-to-xml-example)
- [Propiedades dinámicas de LINQ to XML](/visualstudio/designers/linq-to-xml-dynamic-properties)
