---
title: Conectarse a un origen de datos en ADO.NET
ms.date: 03/30/2017
ms.assetid: 9abc3f92-1be3-4e1a-b360-762dc689650e
ms.openlocfilehash: c04624be758e4bc7c8b1981ad6a9dc44430d62b5
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2019
ms.locfileid: "59083717"
---
# <a name="connecting-to-a-data-source-in-adonet"></a>Conectarse a un origen de datos en ADO.NET
En ADO.NET utilizará un **conexión** objetos para conectarse a un origen de datos específica, proporcionando la información de autenticación necesaria en una cadena de conexión. El **conexión** objeto que se usa depende del tipo de origen de datos.  
  
 Cada proveedor de datos .NET Framework incluye un objeto <xref:System.Data.Common.DbConnection>: el proveedor de datos .NET Framework para OLE DB incluye un objeto <xref:System.Data.OleDb.OleDbConnection>, el proveedor de datos .NET Framework para SQL Server incluye un objeto <xref:System.Data.SqlClient.SqlConnection>, el proveedor de datos .NET Framework para ODBC incluye un objeto <xref:System.Data.Odbc.OdbcConnection> y el proveedor de datos .NET Framework para Oracle incluye un objeto <xref:System.Data.OracleClient.OracleConnection>.  
  
## <a name="in-this-section"></a>En esta sección  
 [Establecer la conexión](../../../../docs/framework/data/adonet/establishing-the-connection.md)  
 Describe cómo utilizar un **conexión** objeto para establecer una conexión a un origen de datos.  
  
 [Eventos de Connection](../../../../docs/framework/data/adonet/connection-events.md)  
 Describe cómo utilizar un **InfoMessage** event para recuperar mensajes informativos de un origen de datos.  
  
## <a name="see-also"></a>Vea también

- [Cadenas de conexión](../../../../docs/framework/data/adonet/connection-strings.md)
- [Agrupación de conexiones](../../../../docs/framework/data/adonet/connection-pooling.md)
- [Comandos y parámetros](../../../../docs/framework/data/adonet/commands-and-parameters.md)
- [Objetos DataAdapter y DataReader](../../../../docs/framework/data/adonet/dataadapters-and-datareaders.md)
- [Transacciones y simultaneidad](../../../../docs/framework/data/adonet/transactions-and-concurrency.md)
- [Proveedores administrados de ADO.NET y centro de desarrolladores de DataSet](https://go.microsoft.com/fwlink/?LinkId=217917)
