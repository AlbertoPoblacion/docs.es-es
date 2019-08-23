---
title: Operaciones de copia masiva en SQL Server
ms.date: 03/30/2017
ms.assetid: 83a7a0d2-8018-4354-97b9-0b1d99f8342b
ms.openlocfilehash: efa13eb1633fce3b59040ef8da79dba0f6ea81d5
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/22/2019
ms.locfileid: "69918065"
---
# <a name="bulk-copy-operations-in-sql-server"></a>Operaciones de copia masiva en SQL Server
Microsoft SQL Server incluye una conocida utilidad de línea de comandos denominada **BCP** para la copia masiva rápida de archivos grandes en tablas o vistas en bases de datos de SQL Server. La clase <xref:System.Data.SqlClient.SqlBulkCopy> permite escribir soluciones de código administrado que ofrecen una funcionalidad similar. Aunque existen otras formas de cargar datos en una tabla SQL Server (por ejemplo, mediante instrucciones INSERT), <xref:System.Data.SqlClient.SqlBulkCopy> tiene la ventaja sobre las demás de un rendimiento significativo.  
  
 La clase <xref:System.Data.SqlClient.SqlBulkCopy> sólo se puede utilizar para escribir datos en tablas SQL Server. Sin embargo, el origen de datos no está limitado a SQL Server; se puede utilizar cualquier origen de datos siempre y cuando pueda cargarse en una instancia <xref:System.Data.DataTable> o leerse con una instancia <xref:System.Data.IDataReader>.  
  
 El uso de la clase <xref:System.Data.SqlClient.SqlBulkCopy> le permite realizar:  
  
- una única operación de copia masiva  
  
- varias operaciones de copia masiva  
  
- una operación de copia masiva en una transacción  
  
> [!NOTE]
> Cuando se usa .NET Framework versión 1,1 o anterior (que no admite la <xref:System.Data.SqlClient.SqlBulkCopy> clase), se puede ejecutar la instrucción SQL Server **Bulk Insert** de Transact-SQL mediante <xref:System.Data.SqlClient.SqlCommand> el objeto.  
  
## <a name="in-this-section"></a>En esta sección  
 [Configuración de ejemplos de copia masiva](../../../../../docs/framework/data/adonet/sql/bulk-copy-example-setup.md)  
 Describe las tablas usadas en los ejemplos de copia masiva y proporciona scripts SQL para crear las tablas de la base de datos AdventureWorks.  
  
 [Operaciones de copia masiva únicas](../../../../../docs/framework/data/adonet/sql/single-bulk-copy-operations.md)  
 Describe cómo realizar una sola copia masiva de datos en una instancia de SQL Server mediante la clase <xref:System.Data.SqlClient.SqlBulkCopy>, y cómo realizar la operación de copia masiva con las instrucciones Transact-SQL y la clase <xref:System.Data.SqlClient.SqlCommand>.  
  
 [Varias operaciones de copia masiva](../../../../../docs/framework/data/adonet/sql/multiple-bulk-copy-operations.md)  
 Describe cómo realizar varias operaciones de copia masiva de datos en una instancia de SQL Server mediante la clase <xref:System.Data.SqlClient.SqlBulkCopy>.  
  
 [Transacción y operaciones de copia masiva](../../../../../docs/framework/data/adonet/sql/transaction-and-bulk-copy-operations.md)  
 Describe cómo realizar una operación de copia masiva en una transacción, lo que incluye cómo confirmar o revertir la transacción.  
  
## <a name="see-also"></a>Vea también

- [SQL Server y ADO.NET](../../../../../docs/framework/data/adonet/sql/index.md)
- [Proveedores administrados de ADO.NET y Centro para desarrolladores de DataSet](https://go.microsoft.com/fwlink/?LinkId=217917)
