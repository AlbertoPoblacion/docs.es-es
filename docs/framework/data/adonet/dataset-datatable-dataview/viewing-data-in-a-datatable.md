---
title: Ver datos en un objeto DataTable
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 1d26e0fb-f6e0-4afa-9a9c-b8d55b8f20dc
ms.openlocfilehash: fa8749550e10256ee0623714cc95e03a838655c8
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61607039"
---
# <a name="viewing-data-in-a-datatable"></a>Ver datos en un objeto DataTable

Puede acceder al contenido de un <xref:System.Data.DataTable> utilizando el **filas** y **columnas** colecciones de la **DataTable**. También puede usar el <xref:System.Data.DataTable.Select%2A> método para devolver subconjuntos de los datos en un **DataTable** según criterios, como criterios de búsqueda, ordenación y el estado de la fila. Además, puede usar el <xref:System.Data.DataRowCollection.Find%2A> método de la **DataRowCollection** al buscar una fila determinada mediante un valor de clave principal.

El **seleccione** método de la **DataTable** objeto devuelve un conjunto de <xref:System.Data.DataRow> objetos que coinciden con los criterios especificados. **Seleccione** toma argumentos opcionales de una expresión de filtro, expresión de ordenación, y **DataViewRowState**. La expresión de filtro identifica qué filas a devolver basándose en **DataColumn** los valores, como `LastName = 'Smith'`. La expresión de ordenación sigue convenciones SQL estándar para ordenar columnas, por ejemplo `LastName ASC, FirstName ASC`. Las reglas de escritura de expresiones, vea el <xref:System.Data.DataColumn.Expression%2A> propiedad de la **DataColumn** clase.

> [!TIP]
> Si va a realizar un número de llamadas a la **seleccione** método de un **DataTable**, puede aumentar el rendimiento creando primero un <xref:System.Data.DataView> para el **DataTable**. Crear el **DataView** índices de las filas de la tabla. El **seleccione** método, a continuación, utiliza ese índice, lo que reduce considerablemente el tiempo necesario para generar el resultado de la consulta. Para obtener información acerca de cómo crear un **DataView** para un **DataTable**, consulte [DataViews](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/dataviews.md).

El **seleccione** método determina qué versión de las filas para ver o manipular según un <xref:System.Data.DataViewRowState>. La tabla siguiente describen los posibles **DataViewRowState** valores de enumeración.

|Valor DataViewRowState|Descripción|
|----------------------------|-----------------|
|**CurrentRows**|Filas actuales, incluidas las filas sin modificar, agregadas y modificadas.|
|**Eliminado**|Una fila eliminada.|
|**ModifiedCurrent**|Una versión actual, que es una versión modificada de los datos originales. (Consulte **ModifiedOriginal**.)|
|**ModifiedOriginal**|Versión original de todas las filas modificadas. La versión actual está disponible con **ModifiedCurrent**.|
|**Added**|Una fila nueva.|
|**Ninguno**|Ninguno.|
|**OriginalRows**|Filas originales, incluidas las filas sin modificar y las eliminadas.|
|**Unchanged**|Una fila sin modificar.|

En el ejemplo siguiente, la **DataSet** objeto se filtra para que sólo trabaja con las filas cuyo **DataViewRowState** está establecido en **CurrentRows**.

```vb
Dim column As DataColumn
Dim row As DataRow

Dim currentRows() As DataRow = _
    workTable.Select(Nothing, Nothing, DataViewRowState.CurrentRows)

If (currentRows.Length < 1 ) Then
  Console.WriteLine("No Current Rows Found")
Else
  For Each column in workTable.Columns
    Console.Write(vbTab & column.ColumnName)
  Next

  Console.WriteLine(vbTab & "RowState")

  For Each row In currentRows
    For Each column In workTable.Columns
      Console.Write(vbTab & row(column).ToString())
    Next

    Dim rowState As String = _
        System.Enum.GetName(row.RowState.GetType(), row.RowState)
    Console.WriteLine(vbTab & rowState)
  Next
End If
```

```csharp
DataRow[] currentRows = workTable.Select(
    null, null, DataViewRowState.CurrentRows);

if (currentRows.Length < 1 )
  Console.WriteLine("No Current Rows Found");
else
{
  foreach (DataColumn column in workTable.Columns)
    Console.Write("\t{0}", column.ColumnName);

  Console.WriteLine("\tRowState");

  foreach (DataRow row in currentRows)
  {
    foreach (DataColumn column in workTable.Columns)
      Console.Write("\t{0}", row[column]);

    Console.WriteLine("\t" + row.RowState);
  }
}
```

El **seleccione** método puede utilizarse para devolver las filas con distintos **RowState** valores o valores de campo. El ejemplo siguiente devuelve un **DataRow** matriz que hace referencia a todas las filas que se han eliminado y devuelve otra **DataRow** matriz que hace referencia a todas las filas, ordenadas por **CustLName**, donde el **CustID** columna es mayor que 5. Para obtener información sobre cómo ver la información de la **Deleted** de fila, vea [Estados de fila y las versiones de fila](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/row-states-and-row-versions.md).

```vb
' Retrieve all deleted rows.
Dim deletedRows() As DataRow = workTable.Select(Nothing, Nothing, DataViewRowState.Deleted)

' Retrieve rows where CustID > 5, and order by CustLName.
Dim custRows() As DataRow = workTable.Select( _
    "CustID > 5", "CustLName ASC")
```

```csharp
// Retrieve all deleted rows.
DataRow[] deletedRows = workTable.Select(
    null, null, DataViewRowState.Deleted);

// Retrieve rows where CustID > 5, and order by CustLName.
DataRow[] custRows = workTable.Select("CustID > 5", "CustLName ASC");
```

## <a name="see-also"></a>Vea también

- <xref:System.Data.DataRow>
- <xref:System.Data.DataSet>
- <xref:System.Data.DataTable>
- <xref:System.Data.DataViewRowState>
- [Manipulación de datos en un objeto DataTable](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/manipulating-data-in-a-datatable.md)
- [Estados y versiones de filas](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/row-states-and-row-versions.md)
- [Proveedores administrados de ADO.NET y Centro para desarrolladores de DataSet](https://go.microsoft.com/fwlink/?LinkId=217917)
