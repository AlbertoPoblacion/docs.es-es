---
title: Filtrar para implementar la validación con el control DataGrid
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- DataGrid [WPF], validation
- validation [WPF], DataGrid
ms.assetid: ec6078a8-1e42-4648-b414-f4348e81bda1
ms.openlocfilehash: 00d09c62aae67e3438816409c95ccf96050b3206
ms.sourcegitcommit: 558d78d2a68acd4c95ef23231c8b4e4c7bac3902
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/09/2019
ms.locfileid: "59305963"
---
# <a name="how-to-implement-validation-with-the-datagrid-control"></a>Filtrar para implementar la validación con el control DataGrid
El <xref:System.Windows.Controls.DataGrid> control le permite realizar la validación en el nivel de la celda y la fila. Con la validación de nivel de celda, validar propiedades individuales de un objeto de datos enlazados cuando un usuario actualiza un valor. Con la validación de nivel de fila, validar los objetos de datos completo cuando un usuario confirma los cambios realizados en una fila. También puede proporcionar comentarios visuales personalizados para los errores de validación, o usar los comentarios visuales predeterminados que el <xref:System.Windows.Controls.DataGrid> proporciona el control.  
  
 Los procedimientos siguientes describen cómo se aplican las reglas de validación <xref:System.Windows.Controls.DataGrid> enlaces y personalizar los comentarios visuales.  
  
### <a name="to-validate-individual-cell-values"></a>Para validar los valores de celda individual  
  
-   Especifique una o varias reglas de validación en el enlace utilizado con una columna. Esto es similar a la validación de datos en controles simples, como se describe en [Data Binding Overview](../data/data-binding-overview.md).  
  
     El ejemplo siguiente se muestra un <xref:System.Windows.Controls.DataGrid> control con cuatro columnas enlazadas a distintas propiedades de un objeto de negocios. Tres de las columnas de especifican el <xref:System.Windows.Controls.ExceptionValidationRule> estableciendo el <xref:System.Windows.Data.Binding.ValidatesOnExceptions%2A> propiedad `true`.  
  
     [!code-xaml[DataGrid_Validation#BasicXaml](~/samples/snippets/csharp/VS_Snippets_Wpf/datagrid_validation/cs/window1.xaml#basicxaml)]  
  
     Cuando un usuario escribe un valor no válido (por ejemplo, un no entero en la columna de Id. de curso), aparece un borde rojo alrededor de la celda. Puede cambiar estos comentarios de validación predeterminado como se describe en el siguiente procedimiento.  
  
### <a name="to-customize-cell-validation-feedback"></a>Para personalizar los comentarios de validación de celda  
  
-   Establezca la columna <xref:System.Windows.Controls.DataGridBoundColumn.EditingElementStyle%2A> propiedad a un estilo apropiado para la columna del control de edición. Dado que los controles de edición se crean en tiempo de ejecución, no puede usar el <xref:System.Windows.Controls.Validation.ErrorTemplate%2A?displayProperty=nameWithType> como lo haría con los controles simples de propiedad adjunta.  
  
     El ejemplo siguiente actualiza en el ejemplo anterior mediante la adición de un estilo de error compartido por las tres columnas con reglas de validación. Cuando un usuario escribe un valor no válido, el estilo cambia el color de fondo de celda y agrega información sobre herramientas. Tenga en cuenta el uso de un desencadenador para determinar si hay un error de validación. Esto es necesario porque actualmente no hay ninguna plantilla de error dedicada para las celdas.  
  
     [!code-xaml[DataGrid_Validation#CellValidationXaml](~/samples/snippets/csharp/VS_Snippets_Wpf/datagrid_validation/cs/mainwindow.xaml#cellvalidationxaml)]  
  
     Puede implementar una personalización más extensa reemplazando el <xref:System.Windows.Controls.DataGridColumn.CellStyle%2A> usada por la columna.  
  
### <a name="to-validate-multiple-values-in-a-single-row"></a>Para validar varios valores en una sola fila  
  
1. Implemente un <xref:System.Windows.Controls.ValidationRule> subclase que comprueba varias propiedades del objeto de datos enlazado. En su <xref:System.Windows.Controls.ValidationRule.Validate%2A> implementación del método, puede convertir el `value` valor de parámetro para un <xref:System.Windows.Data.BindingGroup> instancia. A continuación, puede tener acceso a un objeto de datos a través de la <xref:System.Windows.Data.BindingGroup.Items%2A> propiedad.  
  
     En el ejemplo siguiente se muestra este proceso para validar si la `StartDate` valor de propiedad para un `Course` objeto es anterior a su `EndDate` valor de propiedad.  
  
     [!code-csharp[DataGrid_Validation#CourseValidationRule](~/samples/snippets/csharp/VS_Snippets_Wpf/datagrid_validation/cs/mainwindow.xaml.cs#coursevalidationrule)]
     [!code-vb[DataGrid_Validation#CourseValidationRule](~/samples/snippets/visualbasic/VS_Snippets_Wpf/datagrid_validation/vb/mainwindow.xaml.vb#coursevalidationrule)]  
  
2. Agregar la regla de validación para el <xref:System.Windows.Controls.DataGrid.RowValidationRules%2A?displayProperty=nameWithType> colección. El <xref:System.Windows.Controls.DataGrid.RowValidationRules%2A> propiedad proporciona acceso directo a la <xref:System.Windows.Data.BindingGroup.ValidationRules%2A> propiedad de un <xref:System.Windows.Data.BindingGroup> instancia que agrupa todos los enlaces utilizados por el control.  
  
     El ejemplo siguiente se establece la <xref:System.Windows.Controls.DataGrid.RowValidationRules%2A> propiedad en XAML. El <xref:System.Windows.Controls.ValidationRule.ValidationStep%2A> propiedad está establecida en <xref:System.Windows.Controls.ValidationStep.UpdatedValue> para que la validación se produce después de que el objeto de datos enlazado se actualiza.  
  
     [!code-xaml[DataGrid_Validation#RowValidationRulesXaml](~/samples/snippets/csharp/VS_Snippets_Wpf/datagrid_validation/cs/mainwindow.xaml#rowvalidationrulesxaml)]  
  
     Cuando un usuario especifica una fecha de finalización es anterior a la fecha de inicio, aparece una marca de exclamación rojo (!) en el encabezado de fila. Puede cambiar estos comentarios de validación predeterminado como se describe en el siguiente procedimiento.  
  
### <a name="to-customize-row-validation-feedback"></a>Para personalizar los comentarios de validación de fila  
  
-   Establecer la propiedad <xref:System.Windows.Controls.DataGrid.RowValidationErrorTemplate%2A?displayProperty=nameWithType>. Esta propiedad le permite personalizar los comentarios de validación de filas individuales <xref:System.Windows.Controls.DataGrid> controles. También puede afectar a varios controles mediante un estilo de filas implícitas para establecer el <xref:System.Windows.Controls.DataGridRow.ValidationErrorTemplate%2A?displayProperty=nameWithType> propiedad.  
  
     El siguiente ejemplo reemplaza los comentarios de validación de fila predeterminados con un indicador más visible. Cuando un usuario escribe un valor no válido, aparece un círculo rojo con un signo de exclamación blanco en el encabezado de fila. Esto se produce para los errores de validación de fila y celda. El mensaje de error asociado se muestra en una información sobre herramientas.  
  
     [!code-xaml[DataGrid_Validation#RowValidationFeedbackXaml](~/samples/snippets/csharp/VS_Snippets_Wpf/datagrid_validation/cs/mainwindow.xaml#rowvalidationfeedbackxaml)]  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente proporciona una demostración completa para la validación de celdas y filas. El `Course` clase proporciona un objeto de datos de ejemplo que implementa <xref:System.ComponentModel.IEditableObject> para admitir transacciones. El <xref:System.Windows.Controls.DataGrid> control interactúa con <xref:System.ComponentModel.IEditableObject> para permitir que los usuarios revertir los cambios presionando la tecla ESC.  
  
> [!NOTE]
>  Si utiliza Visual Basic, en la primera línea de MainWindow.xaml, reemplace `x:Class="DataGridValidation.MainWindow"` con `x:Class="MainWindow"`.  
  
 Para probar la validación, intente lo siguiente:  
  
-   En la columna de identificador, escriba un valor no entero.  
  
-   En la columna de fecha de finalización, escriba una fecha anterior a la fecha de inicio.  
  
-   Elimine el valor de identificador del curso, fecha de inicio o fecha de finalización.  
  
-   Para deshacer un valor de celda no válido, coloque el cursor en la celda y presione la tecla ESC.  
  
-   Para deshacer los cambios para una fila completa cuando la celda actual está en modo de edición, presione la tecla ESC dos veces.  
  
-   Cuando se produce un error de validación, mueva el puntero del mouse sobre el indicador en el encabezado de fila para ver el mensaje de error asociado.  
  
 [!code-csharp[DataGrid_Validation#FullCode](~/samples/snippets/csharp/VS_Snippets_Wpf/datagrid_validation/cs/mainwindow.xaml.cs#fullcode)]
 [!code-vb[DataGrid_Validation#FullCode](~/samples/snippets/visualbasic/VS_Snippets_Wpf/datagrid_validation/vb/mainwindow.xaml.vb#fullcode)]  
  
 [!code-xaml[DataGrid_Validation#FullXaml](~/samples/snippets/csharp/VS_Snippets_Wpf/datagrid_validation/cs/mainwindow.xaml#fullxaml)]  
  
## <a name="see-also"></a>Vea también

- <xref:System.Windows.Controls.DataGrid>
- [DataGrid](datagrid.md)
- [Enlace de datos](../data/data-binding-wpf.md)
- [Implementar la validación de enlaces](../data/how-to-implement-binding-validation.md)
- [Implementar lógica de validación en objetos personalizados](../data/how-to-implement-validation-logic-on-custom-objects.md)
