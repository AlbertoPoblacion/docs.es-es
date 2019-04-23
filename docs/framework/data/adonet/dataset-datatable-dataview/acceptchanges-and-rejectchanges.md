---
title: Objetos AcceptChange y RejectChange
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: e2d1a6fe-31f9-4b83-9728-06c406a3394e
ms.openlocfilehash: bbcc666b99c2bade479e5ee51750b043c820845d
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59172905"
---
# <a name="acceptchanges-and-rejectchanges"></a>Objetos AcceptChange y RejectChange
Después de comprobar la exactitud de los cambios realizados a los datos en un <xref:System.Data.DataTable>, puede aceptar los cambios mediante el <xref:System.Data.DataRow.AcceptChanges%2A> método de la <xref:System.Data.DataRow>, <xref:System.Data.DataTable>, o <xref:System.Data.DataSet>, que establecerá el **actual** fila los valores sean los **Original** valores y establecerá el **RowState** propiedad **Unchanged**. Aceptar o rechazar cambios, se elimina **RowError** información y establece el **HasErrors** propiedad **false**. Aceptar o rechazar cambios también puede afectar a la actualización de datos en el origen de datos. Para obtener más información, consulte [actualizar orígenes de datos con objetos DataAdapter](../../../../../docs/framework/data/adonet/updating-data-sources-with-dataadapters.md).  
  
 Si existen restricciones de clave externa en el **DataTable**, los cambios se aceptan o rechazan mediante **AcceptChanges** y **RejectChanges** se propagan a las filas secundarias de la  **DataRow** según la **ForeignKeyConstraint.AcceptRejectRule**. Para obtener más información, consulte [restricciones de DataTable](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/datatable-constraints.md).  
  
 En el ejemplo siguiente se comprueba si hay filas con errores, se resuelven los errores que haya y se rechazan las filas en las que no se puede resolver el error. Tenga en cuenta que, para resolver errores, el **RowError** valor se restablece en una cadena vacía, provocando la **HasErrors** propiedad se establece en **false**. Cuando todas las filas con errores se han resuelto o rechazado, **AcceptChanges** se llama para aceptar todos los cambios para toda la **DataTable**.  
  
```vb  
If workTable.HasErrors Then  
  Dim errRow As DataRow  
  
  For Each errRow in workTable.GetErrors()  
  
    If errRow.RowError = "Total cannot exceed 1000." Then  
      errRow("Total") = 1000  
      errRow.RowError = ""    ' Clear the error.  
    Else  
      errRow.RejectChanges()  
    End If  
  Next  
End If  
  
workTable.AcceptChanges()  
```  
  
```csharp  
if (workTable.HasErrors)  
{  
  
  foreach (DataRow errRow in workTable.GetErrors())  
  {  
    if (errRow.RowError == "Total cannot exceed 1000.")  
    {  
      errRow["Total"] = 1000;  
      errRow.RowError = "";    // Clear the error.  
    }  
    else  
      errRow.RejectChanges();  
  }  
}  
  
workTable.AcceptChanges();  
```  
  
## <a name="see-also"></a>Vea también

- <xref:System.Data.DataRow>
- <xref:System.Data.DataSet>
- <xref:System.Data.DataTable>
- [Manipulación de datos en un objeto DataTable](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/manipulating-data-in-a-datatable.md)
- [Proveedores administrados de ADO.NET y Centro para desarrolladores de DataSet](https://go.microsoft.com/fwlink/?LinkId=217917)
