---
title: Realizar operaciones de catálogo
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: e60f542f-6271-495b-a9e4-48553481c2a3
ms.openlocfilehash: beb5d2db898df1c98662d53190ac1432acc746e7
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61878233"
---
# <a name="performing-catalog-operations"></a>Realizar operaciones de catálogo
Para ejecutar un comando que modifique una base de datos o catálogo, por ejemplo, la instrucción CREATE TABLE o CREATE PROCEDURE, debe crear un **comando** objeto mediante las instrucciones SQL adecuadas y un **conexión** objeto. Ejecute el comando con el **ExecuteNonQuery** método de la **comando** objeto.  
  
 En el ejemplo de código siguiente se crea un procedimiento almacenado en una base de datos de Microsoft SQL Server.  
  
```vb  
' Assumes connection is a valid SqlConnection.  
Dim queryString As String = "CREATE PROCEDURE InsertCategory " & _  
    "@CategoryName nchar(15), " & _  
    "@Identity int OUT " & _  
    "AS " & _  
    "INSERT INTO Categories (CategoryName) VALUES(@CategoryName) " & _  
    "SET @Identity = @@Identity " & _  
    "RETURN @@ROWCOUNT"  
  
Dim command As SqlCommand = New SqlCommand(queryString, connection)  
command.ExecuteNonQuery()  
```  
  
```csharp  
// Assumes connection is a valid SqlConnection.  
string queryString = "CREATE PROCEDURE InsertCategory  " +   
    "@CategoryName nchar(15), " +  
    "@Identity int OUT " +  
    "AS " +   
    "INSERT INTO Categories (CategoryName) VALUES(@CategoryName) " +   
    "SET @Identity = @@Identity " +  
    "RETURN @@ROWCOUNT";  
  
SqlCommand command = new SqlCommand(queryString, connection);  
command.ExecuteNonQuery();  
```  
  
## <a name="see-also"></a>Vea también

- [Uso de comandos para modificar datos](../../../../docs/framework/data/adonet/using-commands-to-modify-data.md)
- [Comandos y parámetros](../../../../docs/framework/data/adonet/commands-and-parameters.md)
- [Proveedores administrados de ADO.NET y Centro para desarrolladores de DataSet](https://go.microsoft.com/fwlink/?LinkId=217917)
