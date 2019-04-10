---
title: Filtrar para obtener acceso a objetos de una lista desplegable DataGridViewComboBoxCell en formularios Windows Forms
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- DataGridView control [Windows Forms], accessing objects in combo box cells
- combo boxes [Windows Forms], in DataGridView control
- combo boxes [Windows Forms], accessing objects in DataGridViewComboBoxCell drop-down lists
ms.assetid: bcbe794a-d1fa-47f8-b5a3-5f085b32097d
ms.openlocfilehash: 17b7c93effe9338a9e2d6cb207a948a956d9b666
ms.sourcegitcommit: 558d78d2a68acd4c95ef23231c8b4e4c7bac3902
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/09/2019
ms.locfileid: "59334281"
---
# <a name="how-to-access-objects-in-a-windows-forms-datagridviewcomboboxcell-drop-down-list"></a>Filtrar para obtener acceso a objetos de una lista desplegable DataGridViewComboBoxCell en formularios Windows Forms
Al igual que el <xref:System.Windows.Forms.ComboBox> (control), el <xref:System.Windows.Forms.DataGridViewComboBoxColumn> y <xref:System.Windows.Forms.DataGridViewComboBoxCell> tipos le permiten agregar objetos arbitrarios a las listas de la lista desplegable. Con esta característica, puede representar estados complejos en una lista desplegable sin tener que almacenar los objetos correspondientes en una colección independiente.  
  
 A diferencia de la <xref:System.Windows.Forms.ComboBox> (control), el <xref:System.Windows.Forms.DataGridView> tipos no tienen un <xref:System.Windows.Forms.ComboBox.SelectedItem%2A> propiedad para recuperar el objeto seleccionado actualmente. En su lugar, debe establecer el <xref:System.Windows.Forms.DataGridViewComboBoxColumn.ValueMember%2A?displayProperty=nameWithType> o <xref:System.Windows.Forms.DataGridViewComboBoxCell.ValueMember%2A?displayProperty=nameWithType> propiedad en el nombre de una propiedad en el objeto comercial. Cuando el usuario realiza una selección, la propiedad indicada del objeto comercial establece la celda <xref:System.Windows.Forms.DataGridViewCell.Value%2A> propiedad.  
  
 Para recuperar el objeto de negocios a través del valor de celda, el `ValueMember` propiedad debe indicar una propiedad que devuelve una referencia al propio objeto de negocios. Por lo tanto, si el tipo del objeto comercial no está bajo su control, debe agregar esa propiedad mediante la extensión de tipo a través de herencia.  
  
 Los procedimientos siguientes muestran cómo rellenar una lista desplegable con objetos de negocios y recuperar los objetos a través de la celda <xref:System.Windows.Forms.DataGridViewCell.Value%2A> propiedad.  
  
### <a name="to-add-business-objects-to-the-drop-down-list"></a>Para agregar objetos de negocios a la lista desplegable  
  
1. Cree un nuevo <xref:System.Windows.Forms.DataGridViewComboBoxColumn> y rellenar sus <xref:System.Windows.Forms.DataGridViewComboBoxColumn.Items%2A> colección. Como alternativa, puede establecer la columna <xref:System.Windows.Forms.DataGridViewComboBoxColumn.DataSource%2A> propiedad a la colección de objetos de negocios. En ese caso, sin embargo, no puede agregar "sin asignar" a la lista desplegable sin crear un objeto comercial correspondiente en la colección.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewComboBoxObjectBinding#110](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewComboBoxObjectBinding/CS/form1.cs#110)]
     [!code-vb[System.Windows.Forms.DataGridViewComboBoxObjectBinding#110](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewComboBoxObjectBinding/vb/form1.vb#110)]  
  
2. Establezca las propiedades <xref:System.Windows.Forms.DataGridViewComboBoxColumn.DisplayMember%2A> y <xref:System.Windows.Forms.DataGridViewComboBoxColumn.ValueMember%2A>. <xref:System.Windows.Forms.DataGridViewComboBoxColumn.DisplayMember%2A> indica la propiedad del objeto comercial que se muestra en la lista desplegable. <xref:System.Windows.Forms.DataGridViewComboBoxColumn.ValueMember%2A> indica la propiedad que devuelve una referencia al objeto de negocios.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewComboBoxObjectBinding#115](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewComboBoxObjectBinding/CS/form1.cs#115)]
     [!code-vb[System.Windows.Forms.DataGridViewComboBoxObjectBinding#115](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewComboBoxObjectBinding/vb/form1.vb#115)]  
  
3. Asegúrese de que el tipo de objeto de negocios contiene una propiedad que devuelve una referencia a la instancia actual. Esta propiedad se debe denominar con el valor asignado a <xref:System.Windows.Forms.DataGridViewComboBoxColumn.ValueMember%2A> en el paso anterior.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewComboBoxObjectBinding#310](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewComboBoxObjectBinding/CS/form1.cs#310)]
     [!code-vb[System.Windows.Forms.DataGridViewComboBoxObjectBinding#310](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewComboBoxObjectBinding/vb/form1.vb#310)]  
  
### <a name="to-retrieve-the-currently-selected-business-object"></a>Para recuperar el objeto de negocios seleccionada actualmente  
  
-   Obtenga la celda <xref:System.Windows.Forms.DataGridViewCell.Value%2A> propiedad y convertirlo en el tipo de objeto de negocios.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewComboBoxObjectBinding#120](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewComboBoxObjectBinding/CS/form1.cs#120)]
     [!code-vb[System.Windows.Forms.DataGridViewComboBoxObjectBinding#120](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewComboBoxObjectBinding/vb/form1.vb#120)]  
  
## <a name="example"></a>Ejemplo  
 El ejemplo completo muestra el uso de objetos comerciales en una lista desplegable. En el ejemplo, un <xref:System.Windows.Forms.DataGridView> está enlazado a una colección de `Task` objetos. Cada `Task` objeto tiene un `AssignedTo` propiedad que indica la `Employee` objeto asignado actualmente a esa tarea. El `Assigned To` columna muestra el `Name` asigna el valor de propiedad para cada empleado, o "no asignado" si el `Task.AssignedTo` es el valor de propiedad `null`.  
  
 Para ver el comportamiento de este ejemplo, realice los pasos siguientes:  
  
1. Cambiar las asignaciones en el `Assigned To` columna seleccionando valores diferentes en las listas desplegables o presionar CTRL + 0 en una celda de cuadro combinado.  
  
2. Haga clic en `Generate Report` para mostrar las asignaciones actuales. Esto demuestra que un cambio en el `Assigned To` columna se actualiza automáticamente el `tasks` colección.  
  
3. Haga clic en un `Request Status` botón para llamar a la `RequestStatus` método del actual `Employee` objeto para esa fila. Esto demuestra que el objeto seleccionado se ha recuperado correctamente.  
  
 [!code-csharp[System.Windows.Forms.DataGridViewComboBoxObjectBinding#000](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewComboBoxObjectBinding/CS/form1.cs#000)]
 [!code-vb[System.Windows.Forms.DataGridViewComboBoxObjectBinding#000](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewComboBoxObjectBinding/vb/form1.vb#000)]  
  
## <a name="compiling-the-code"></a>Compilar el código  
 Para este ejemplo se necesita:  
  
-   Referencias a los ensamblados System y System.Windows.Forms.  
  
## <a name="see-also"></a>Vea también

- <xref:System.Windows.Forms.DataGridView>
- <xref:System.Windows.Forms.DataGridViewComboBoxColumn>
- <xref:System.Windows.Forms.DataGridViewComboBoxColumn.Items%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewComboBoxColumn.DataSource%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewComboBoxColumn.ValueMember%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewComboBoxCell>
- <xref:System.Windows.Forms.DataGridViewComboBoxCell.Items%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewComboBoxCell.DataSource%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewComboBoxCell.ValueMember%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewCell.Value%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.ComboBox>
- [Mostrar datos en el control DataGridView de formularios Windows Forms](displaying-data-in-the-windows-forms-datagridview-control.md)
