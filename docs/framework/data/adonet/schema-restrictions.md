---
title: Restricciones de esquema
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 73d2980e-e73c-4987-913a-8ddc93d09144
ms.openlocfilehash: b5044d39d1dc5d2fa7d2ce691cdda7075fa0e32a
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2019
ms.locfileid: "59151208"
---
# <a name="schema-restrictions"></a>Restricciones de esquema
El segundo parámetro opcional de la **GetSchema** método es devuelven las restricciones que se usan para limitar la cantidad de información de esquema y se pasa a la **GetSchema** método como una matriz de cadenas . La posición en la matriz determina los valores que puede pasar, y es equivalente al número de restricciones.  
  
 Por ejemplo, en la tabla siguiente se describen las restricciones que admite la colección de esquemas "Tables" utilizando el proveedor de datos .NET Framework para SQL Server. Las restricciones adicionales para las colecciones de esquemas de SQL Server se muestran al final de este tema.  
  
|Nombre de la restricción|Nombre de parámetro|Valor predeterminado de la restricción|Número de restricciones|  
|----------------------|--------------------|-------------------------|------------------------|  
|Catálogo|@Catalog|TABLE_CATALOG|1|  
|Propietario|@Owner|TABLE_SCHEMA|2|  
|Tabla|@Name|TABLE_NAME|3|  
|TableType|@TableType|TABLE_TYPE|4|  
  
## <a name="specifying-restriction-values"></a>Especificación de los valores de restricción  
 Para utilizar una de las restricciones de la colección de esquemas "Tables", basta con crear una matriz de cadenas con cuatro elementos y, después, colocar un valor en el elemento que coincida con el número de restricción. Por ejemplo restringir las tablas devuelto por la **GetSchema** método sólo a esas tablas en el esquema "Sales", establezca el segundo elemento de la matriz en "Ventas" antes de pasarlo a la **GetSchema** método.  
  
> [!NOTE]
>  Las colecciones con restricciones para `SqlClient` y `OracleClient` tienen una columna `ParameterName` adicional. La columna de valor predeterminado de restricción sigue ahí para la compatibilidad con versiones anteriores, pero actualmente se omite. Para reducir el riesgo de un ataque de inyección de SQL al especificar valores de restricción, es necesario utilizar consultas parametrizadas en lugar de sustitución de cadenas.  
  
> [!NOTE]
>  El número de elementos de la matriz debe ser menor o igual que el número de restricciones admitidas en la colección de esquemas especificada o se iniciará una <xref:System.ArgumentException>. Puede haber un número de restricciones inferior al máximo. Se supone que las restricciones que faltan serán nulas (sin restricciones).  
  
 Puede consultar un proveedor administrado de .NET Framework para determinar la lista de restricciones admitidas mediante una llamada a la **GetSchema** método con el nombre de la colección de esquemas de restricciones, que es "Restrictions". Esto devolverá una <xref:System.Data.DataTable> con una lista de los nombres de colecciones, los nombres de restricciones, los valores predeterminados de restricción y los números de restricciones.  
  
### <a name="example"></a>Ejemplo  
 Los ejemplos siguientes muestran cómo usar el <xref:System.Data.SqlClient.SqlConnection.GetSchema%2A> método del proveedor de datos .NET Framework para SQL Server <xref:System.Data.SqlClient.SqlConnection> clase para recuperar información de esquema de todas las tablas contenidas en el **AdventureWorks**base de datos de ejemplo y restringir la información devuelta a sólo las tablas en el esquema "Sales":  
  
```vb  
Imports System.Data.SqlClient  
  
Module Module1  
Sub Main()  
  Dim connectionString As String = _  
    "Data Source=(local);Database=AdventureWorks;" & _  
       "Integrated Security=true;";  
  
  Dim restrictions(3) As String  
  Using connection As New SqlConnection(connectionString)  
    connection.Open()  
  
    'Specify the restrictions.  
    restrictions(1) = "Sales"  
    Dim table As DataTable = connection.GetSchema("Tables", _  
       restrictions)  
  
    ' Display the contents of the table.  
      For Each row As DataRow In table.Rows  
         For Each col As DataColumn In table.Columns  
            Console.WriteLine("{0} = {1}", col.ColumnName, row(col))  
         Next  
         Console.WriteLine("============================")  
      Next  
    Console.WriteLine("Press any key to continue.")  
    Console.ReadKey()  
  End Using  
End Sub  
End Module  
```  
  
```csharp  
using System;  
using System.Data;  
using System.Data.SqlClient;  
  
class Program  
{  
  static void Main()  
  {  
    string connectionString =   
       "Data Source=(local);Database=AdventureWorks;" +  
       "Integrated Security=true;";  
    using (SqlConnection connection =  
       new SqlConnection(connectionString))  
    {  
        connection.Open();  
  
        // Specify the restrictions.  
        string[] restrictions = new string[4];  
        restrictions[1] = "Sales";  
        System.Data.DataTable table = connection.GetSchema(  
          "Tables", restrictions);  
  
        // Display the contents of the table.  
        foreach (System.Data.DataRow row in table.Rows)  
        {  
            foreach (System.Data.DataColumn col in table.Columns)  
            {  
                Console.WriteLine("{0} = {1}",   
                  col.ColumnName, row[col]);  
            }  
            Console.WriteLine("============================");  
        }  
        Console.WriteLine("Press any key to continue.");  
        Console.ReadKey();  
    }  
  }  
  
  private static string GetConnectionString()  
  {  
     // To avoid storing the connection string in your code,  
     // you can retrieve it from a configuration file.  
     return "Data Source=(local);Database=AdventureWorks;" +  
        "Integrated Security=true;";  
  }  
  
  private static void DisplayData(System.Data.DataTable table)  
  {  
     foreach (System.Data.DataRow row in table.Rows)  
     {  
        foreach (System.Data.DataColumn col in table.Columns)  
        {  
           Console.WriteLine("{0} = {1}", col.ColumnName, row[col]);  
        }  
     Console.WriteLine("============================");  
     }  
  }  
}  
```  
  
## <a name="sql-server-schema-restrictions"></a>Restricciones de esquema de SQL Server  
 En la tabla siguiente se muestran las restricciones de las colecciones de esquemas de SQL Server.  
  
### <a name="users"></a>Usuarios  
  
|Nombre de la restricción|Nombre de parámetro|Valor predeterminado de la restricción|Número de restricciones|  
|----------------------|--------------------|-------------------------|------------------------|  
|User_Name|@Name|name|1|  
  
### <a name="databases"></a>Bases de datos  
  
|Nombre de la restricción|Nombre de parámetro|Valor predeterminado de la restricción|Número de restricciones|  
|----------------------|--------------------|-------------------------|------------------------|  
|Name|@Name|Name|1|  
  
### <a name="tables"></a>Tablas  
  
|Nombre de la restricción|Nombre de parámetro|Valor predeterminado de la restricción|Número de restricciones|  
|----------------------|--------------------|-------------------------|------------------------|  
|Catálogo|@Catalog|TABLE_CATALOG|1|  
|Propietario|@Owner|TABLE_SCHEMA|2|  
|Tabla|@Name|TABLE_NAME|3|  
|TableType|@TableType|TABLE_TYPE|4|  
  
### <a name="columns"></a>Columnas  
  
|Nombre de la restricción|Nombre de parámetro|Valor predeterminado de la restricción|Número de restricciones|  
|----------------------|--------------------|-------------------------|------------------------|  
|Catálogo|@Catalog|TABLE_CATALOG|1|  
|Propietario|@Owner|TABLE_SCHEMA|2|  
|Tabla|@Table|TABLE_NAME|3|  
|Columna|@Column|COLUMN_NAME|4|  
  
### <a name="structuredtypemembers"></a>StructuredTypeMembers  
  
|Nombre de la restricción|Nombre de parámetro|Valor predeterminado de la restricción|Número de restricciones|  
|----------------------|--------------------|-------------------------|------------------------|  
|Catálogo|@Catalog|TABLE_CATALOG|1|  
|Propietario|@Owner|TABLE_SCHEMA|2|  
|Tabla|@Table|TABLE_NAME|3|  
|Columna|@Column|COLUMN_NAME|4|  
  
### <a name="views"></a>Vistas  
  
|Nombre de la restricción|Nombre de parámetro|Valor predeterminado de la restricción|Número de restricciones|  
|----------------------|--------------------|-------------------------|------------------------|  
|Catálogo|@Catalog|TABLE_CATALOG|1|  
|Propietario|@Owner|TABLE_SCHEMA|2|  
|Tabla|@Table|TABLE_NAME|3|  
  
### <a name="viewcolumns"></a>ViewColumns  
  
|Nombre de la restricción|Nombre de parámetro|Valor predeterminado de la restricción|Número de restricciones|  
|----------------------|--------------------|-------------------------|------------------------|  
|Catálogo|@Catalog|VIEW_CATALOG|1|  
|Propietario|@Owner|VIEW_SCHEMA|2|  
|Tabla|@Table|VIEW_NAME|3|  
|Columna|@Column|COLUMN_NAME|4|  
  
### <a name="procedureparameters"></a>ProcedureParameters  
  
|Nombre de la restricción|Nombre de parámetro|Valor predeterminado de la restricción|Número de restricciones|  
|----------------------|--------------------|-------------------------|------------------------|  
|Catálogo|@Catalog|SPECIFIC_CATALOG|1|  
|Propietario|@Owner|SPECIFIC_SCHEMA|2|  
|Name|@Name|SPECIFIC_NAME|3|  
|Parámetro|@Parameter|PARAMETER_NAME|4|  
  
### <a name="procedures"></a>Procedimientos  
  
|Nombre de la restricción|Nombre de parámetro|Valor predeterminado de la restricción|Número de restricciones|  
|----------------------|--------------------|-------------------------|------------------------|  
|Catálogo|@Catalog|SPECIFIC_CATALOG|1|  
|Propietario|@Owner|SPECIFIC_SCHEMA|2|  
|Name|@Name|SPECIFIC_NAME|3|  
|Tipo|@Type|ROUTINE_TYPE|4|  
  
### <a name="indexcolumns"></a>IndexColumns  
  
|Nombre de la restricción|Nombre de parámetro|Valor predeterminado de la restricción|Número de restricciones|  
|----------------------|--------------------|-------------------------|------------------------|  
|Catálogo|@Catalog|db_name()|1|  
|Propietario|@Owner|user_name()|2|  
|Tabla|@Table|o.name|3|  
|ConstraintName|@ConstraintName|x.name|4|  
|Columna|@Column|c.name|5|  
  
### <a name="indexes"></a>Índices  
  
|Nombre de la restricción|Nombre de parámetro|Valor predeterminado de la restricción|Número de restricciones|  
|----------------------|--------------------|-------------------------|------------------------|  
|Catálogo|@Catalog|db_name()|1|  
|Propietario|@Owner|user_name()|2|  
|Tabla|@Table|o.name|3|  
  
### <a name="userdefinedtypes"></a>UserDefinedTypes  
  
|Nombre de la restricción|Nombre de parámetro|Valor predeterminado de la restricción|Número de restricciones|  
|----------------------|--------------------|-------------------------|------------------------|  
|assembly_name|@AssemblyName|assemblies.name|1|  
|udt_name|@UDTName|types.assembly_class|2|  
  
### <a name="foreignkeys"></a>ForeignKeys  
  
|Nombre de la restricción|Nombre de parámetro|Valor predeterminado de la restricción|Número de restricciones|  
|----------------------|--------------------|-------------------------|------------------------|  
|Catálogo|@Catalog|CONSTRAINT_CATALOG|1|  
|Propietario|@Owner|CONSTRAINT_SCHEMA|2|  
|Tabla|@Table|TABLE_NAME|3|  
|Name|@Name|CONSTRAINT_NAME|4|  
  
## <a name="sql-server-2008-schema-restrictions"></a>Restricciones de esquema de SQL Server 2008  
 En la tabla siguiente se muestran las restricciones de las colecciones de esquemas de SQL Server 2008. Estas restricciones son válidas a partir de la versión 3.5 SP1 de .NET Framework y SQL Server 2008. No se admiten en versiones anteriores de .NET Framework y SQL Server.  
  
### <a name="columnsetcolumns"></a>ColumnSetColumns  
  
|Nombre de la restricción|Nombre de parámetro|Valor predeterminado de la restricción|Número de restricciones|  
|----------------------|--------------------|-------------------------|------------------------|  
|Catálogo|@Catalog|TABLE_CATALOG|1|  
|Propietario|@Owner|TABLE_SCHEMA|2|  
|Tabla|@Table|TABLE_NAME|3|  
  
### <a name="allcolumns"></a>AllColumns  
  
|Nombre de la restricción|Nombre de parámetro|Valor predeterminado de la restricción|Número de restricciones|  
|----------------------|--------------------|-------------------------|------------------------|  
|Catálogo|@Catalog|TABLE_CATALOG|1|  
|Propietario|@Owner|TABLE_SCHEMA|2|  
|Tabla|@Table|TABLE_NAME|3|  
|Columna|@Column|COLUMN_NAME|4|  
  
## <a name="see-also"></a>Vea también

- [Proveedores administrados de ADO.NET y centro de desarrolladores de DataSet](https://go.microsoft.com/fwlink/?LinkId=217917)
