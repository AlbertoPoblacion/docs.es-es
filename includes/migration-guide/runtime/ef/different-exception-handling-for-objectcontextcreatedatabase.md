---
ms.openlocfilehash: 33ad1c044001e0a8d09708cc7a1f06e05cb307de
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2019
ms.locfileid: "59235818"
---
### <a name="different-exception-handling-for-objectcontextcreatedatabase-and-dbproviderservicescreatedatabase-methods"></a>Control de excepciones diferente para los métodos ObjectContext.CreateDatabase y DbProviderServices.CreateDatabase

|   |   |
|---|---|
|Detalles|A partir de .NET Framework 4.5, si se produce un error en la creación de la base de datos, los métodos <code>CreateDatabase</code> intentarán eliminar la base de datos vacía. Si esa operación se realiza correctamente, se propagará la excepción <xref:System.Data.SqlClient.SqlException?displayProperty=name> original (en lugar de la excepción <xref:System.InvalidOperationException?displayProperty=name>, que siempre se iniciaba en .NET Framework 4.0).|
|Sugerencia|Cuando se detecta una excepción <xref:System.InvalidOperationException?displayProperty=name> al ejecutar <xref:System.Data.Objects.ObjectContext.CreateDatabase> o <xref:System.Data.Common.DbProviderServices.CreateDatabase(System.Data.Common.DbConnection,System.Nullable{System.Int32},System.Data.Metadata.Edm.StoreItemCollection)>, ahora también se deben detectar las excepciones SQLExceptions.|
|Ámbito|Secundaria|
|Versión|4.5|
|Tipo|Tiempo de ejecución|
|API afectadas|<ul><li><xref:System.Data.Objects.ObjectContext.CreateDatabase?displayProperty=nameWithType></li><li><xref:System.Data.Common.DbProviderServices.CreateDatabase(System.Data.Common.DbConnection,System.Nullable{System.Int32},System.Data.Metadata.Edm.StoreItemCollection)?displayProperty=nameWithType></li></ul>|
