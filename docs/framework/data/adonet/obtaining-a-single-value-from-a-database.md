---
title: Obtener un valor único de una base de datos
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: b38526cd-a62a-48cb-822a-e91dfa68e02d
ms.openlocfilehash: 5eb81fd2a64f06f1252f71e251e58df568e7407c
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59120684"
---
# <a name="obtaining-a-single-value-from-a-database"></a>Obtener un valor único de una base de datos
En ocasiones se debe devolver información de bases de datos consistente en un único valor, en lugar de una tabla o un flujo de datos. Por ejemplo, es posible que desea devolver el resultado de una función de agregado como COUNT (\*), SUM o AVG (Quantity). El **comando** objeto proporciona la capacidad de devolver valores únicos mediante el **ExecuteScalar** método. El **ExecuteScalar** método devuelve, como un valor escalar, el valor de la primera columna de la primera fila del conjunto de resultados.  
  
 El ejemplo de código siguiente inserta un valor nuevo en la base de datos utilizando <xref:System.Data.SqlClient.SqlCommand>. El método <xref:System.Data.SqlClient.SqlCommand.ExecuteScalar%2A> se utiliza para devolver el valor de columna de identidad para el registro insertado.  
  
 [!code-csharp[DataWorks SqlCommand.ExecuteScalar#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlCommand.ExecuteScalar/CS/source.cs#1)]
 [!code-vb[DataWorks SqlCommand.ExecuteScalar#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlCommand.ExecuteScalar/VB/source.vb#1)]  
  
## <a name="see-also"></a>Vea también

- [Comandos y parámetros](../../../../docs/framework/data/adonet/commands-and-parameters.md)
- [Ejecución de un comando](../../../../docs/framework/data/adonet/executing-a-command.md)
- [DbConnection, DbCommand y DbException](../../../../docs/framework/data/adonet/dbconnection-dbcommand-and-dbexception.md)
- [Proveedores administrados de ADO.NET y Centro para desarrolladores de DataSet](https://go.microsoft.com/fwlink/?LinkId=217917)
