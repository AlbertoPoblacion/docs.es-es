---
title: Procedimiento Enlazar a un origen de datos ADO.NET
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- data binding [WPF], binding to ADO.NET data sources
- ADO.NET data sources [WPF], binding to
- binding [WPF], to ADO.NET data sources
ms.assetid: a70c6d7b-7b38-4fdf-b655-4804db7c8315
ms.openlocfilehash: 08933e67c2cc4b7ccfb6ae0c9dfde34f40e4e5f5
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/06/2019
ms.locfileid: "57465554"
---
# <a name="how-to-bind-to-an-adonet-data-source"></a>Filtrar Enlazar a un origen de datos ADO.NET

En este ejemplo se muestra cómo enlazar un [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] <xref:System.Windows.Controls.ListBox> el control a un [!INCLUDE[TLA#tla_adonet](../../../../includes/tlasharptla-adonet-md.md)] `DataSet`.

## <a name="example"></a>Ejemplo

En este ejemplo, se utiliza un objeto `OleDbConnection` para conectar al origen de datos, que es un archivo `Access MDB` especificado en la cadena de conexión. Una vez establecida la conexión, se crea un objeto `OleDbDataAdapter`. El objeto `OleDbDataAdapter` ejecuta una instrucción select de [!INCLUDE[TLA#tla_sql](../../../../includes/tlasharptla-sql-md.md)] para recuperar el conjunto de registros de la base de datos. Los resultados del comando de [!INCLUDE[TLA2#tla_sql](../../../../includes/tla2sharptla-sql-md.md)] se almacenan en una `DataTable` de `DataSet` mediante una llamada al método `Fill` de `OleDbDataAdapter`. El elemento `DataTable` de este ejemplo se denomina `BookTable`. En el ejemplo, a continuación, Establece el <xref:System.Windows.FrameworkElement.DataContext%2A> propiedad de la <xref:System.Windows.Controls.ListBox> a la `DataSet` objeto.

[!code-csharp[ADODataSet#1](~/samples/snippets/csharp/VS_Snippets_Wpf/ADODataSet/CSharp/Window1.xaml.cs#1)]
[!code-vb[ADODataSet#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ADODataSet/VisualBasic/Window1.xaml.vb#1)]

A continuación, podemos enlazar el <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> propiedad de la <xref:System.Windows.Controls.ListBox> a `BookTable` de la `DataSet`:

[!code-xaml[ADODataSet#2](~/samples/snippets/csharp/VS_Snippets_Wpf/ADODataSet/CSharp/Window1.xaml#2)]

`BookItemTemplate` es el <xref:System.Windows.DataTemplate> que define cómo aparecen los datos:

[!code-xaml[ADODataSet#3](~/samples/snippets/csharp/VS_Snippets_Wpf/ADODataSet/CSharp/Window1.xaml#3)]

`IntColorConverter` convierte un valor `int` en un color. Con el uso de este convertidor, el <xref:System.Windows.Controls.TextBlock.Background%2A> color del tercer <xref:System.Windows.Controls.TextBlock> debe aparecer en verde si el valor de `NumPages` es inferior a 350 y rojo, en caso contrario. La implementación del convertidor no se muestra aquí.

## <a name="see-also"></a>Vea también

- <xref:System.Windows.Data.BindingListCollectionView>
- [Información general sobre el enlace de datos](data-binding-overview.md)
- [Temas "Cómo..."](data-binding-how-to-topics.md)
