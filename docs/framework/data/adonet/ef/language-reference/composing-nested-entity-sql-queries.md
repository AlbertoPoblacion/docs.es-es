---
title: Crear consultas anidadas de Entity SQL
ms.date: 03/30/2017
ms.assetid: 685d4cd3-2c1f-419f-bb46-c9d97a351eeb
ms.openlocfilehash: cd41c36853f50597a32d511d455148d649d9eb64
ms.sourcegitcommit: 2e95559d957a1a942e490c5fd916df04b39d73a9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/16/2019
ms.locfileid: "72395559"
---
# <a name="composing-nested-entity-sql-queries"></a>Crear consultas anidadas de Entity SQL
[!INCLUDE[esql](../../../../../../includes/esql-md.md)] es un lenguaje funcional enriquecido. El bloque de creación de [!INCLUDE[esql](../../../../../../includes/esql-md.md)] es una expresión. A diferencia de SQL convencional, [!INCLUDE[esql](../../../../../../includes/esql-md.md)] no se limita a un conjunto de resultados tabulares: [!INCLUDE[esql](../../../../../../includes/esql-md.md)] admite la creación de expresiones complejas que pueden tener literales, parámetros o expresiones anidadas. Un valor de la expresión se puede parametrizar o se compone de otra expresión.  
  
## <a name="nested-expressions"></a>Expresiones anidadas  
 Una expresión anidada se puede colocar en cualquier parte donde se acepte un valor del tipo que devuelve. Por ejemplo:  
  
```sql  
-- Returns a hierarchical collection of three elements at top-level.   
-- x must be passed in the parameter collection.  
ROW(@x, {@x}, {@x, 4, 5}, {@x, 7, 8, 9})  
  
-- Returns a hierarchical collection of one element at top-level.  
-- x must be passed in the parameter collection.  
{{{@x}}};  
```  
  
 Una consulta anidada se puede colocar en una cláusula de proyección. Por ejemplo:  
  
```sql  
-- Returns a collection of rows where each row contains an Address entity.  
-- and a collection of references to its corresponding SalesOrderHeader entities.  
SELECT address, (SELECT DEREF(soh)   
                    FROM NAVIGATE(address, AdventureWorksModel.FK_SalesOrderHeader_Address_BillToAddressID) AS soh)   
                    AS salesOrderHeader FROM AdventureWorksEntities.Address AS address  
```  
  
 En [!INCLUDE[esql](../../../../../../includes/esql-md.md)], las consultas anidadas siempre deben ir entre paréntesis:  
  
```sql  
-- Pseudo-Entity SQL  
( SELECT …  
FROM … )  
UNION ALL  
( SELECT …  
FROM … );  
```  
  
 En el ejemplo siguiente se muestra cómo anidar correctamente las expresiones en [!INCLUDE[esql](../../../../../../includes/esql-md.md)]: [Cómo: ordenar la Unión de dos consultas](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb896299(v=vs.100)).  
  
## <a name="nested-queries-in-projection"></a>Consultas anidadas en proyección  
 Las consultas anidadas en la cláusula del proyecto se podrían traducir en consultas de producto cartesiano en el servidor. En algunos servidores back-end, incluido SQL Server, esto puede hacer que la tabla TempDB sea muy grande, lo que puede afectar negativamente al rendimiento del servidor.  
  
 A continuación se muestra un ejemplo de dicha consulta:  
  
```sql  
SELECT c, (SELECT c, (SELECT c FROM AdventureWorksModel.Vendor AS c  ) As Inner2 FROM AdventureWorksModel.JobCandidate AS c  ) As Inner1 FROM AdventureWorksModel.EmployeeDepartmentHistory AS c  
```  
  
## <a name="ordering-nested-queries"></a>Ordenar las consultas anidadas  
 En el Entity Framework, una expresión anidada se puede colocar en cualquier parte de la consulta. Dado que Entity SQL permite gran flexibilidad al escribir las consultas, es posible escribir una consulta que contenga una ordenación de las consultas anidadas. Sin embargo, el orden de una consulta anidada no se conserva.  
  
```sql  
-- The following query will order the results by last name.  
SELECT C1.FirstName, C1.LastName  
        FROM AdventureWorksModel.Contact as C1  
        ORDER BY C1.LastName  
```  
  
```sql  
-- In the following query, ordering of the nested query is ignored.  
SELECT C2.FirstName, C2.LastName  
    FROM (SELECT C1.FirstName, C1.LastName  
        FROM AdventureWorksModel.Contact as C1  
        ORDER BY C1.LastName) as C2  
```  
  
## <a name="see-also"></a>Vea también

- [Información general sobre Entity SQL](entity-sql-overview.md)
