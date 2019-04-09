---
title: Generación de SQL
ms.date: 03/30/2017
ms.assetid: 0e16aa02-d458-4418-a765-58b42aad9315
ms.openlocfilehash: 108a68f74849c7fa1418775c2a37db06d9d947ff
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2019
ms.locfileid: "59180585"
---
# <a name="sql-generation"></a>Generación de SQL
Al escribir un proveedor para [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)], debe traducir los árboles de comandos de [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] en SQL que una base de datos concreta puede entender, como Transact-SQL para SQL Server o PL/SQL para Oracle. En esta sección, obtendrá información sobre cómo desarrollar un componente de generación de SQL (para consultas SELECT) para un proveedor de [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)]. Para obtener información acerca de la inserción, actualización y eliminar consultas, consulte [generar SQL de modificación](../../../../../docs/framework/data/adonet/ef/modification-sql-generation.md).  
  
 Para entender esta sección, debe estar familiarizado con [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] y el modelo de proveedor de ADO.NET. También debe comprender los árboles de comandos y <xref:System.Data.Common.CommandTrees.DbExpression>.  
  
## <a name="the-role-of-the-sql-generation-module"></a>El rol del módulo de generación de SQL  
 El módulo de generación de SQL de un proveedor de [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] traduce un árbol de comandos de consulta determinado en una instrucción SELECT de SQL única que tiene como destino una base de datos conforme a SQL:1999. El SQL generado debe tener el menor número posible de consultas anidadas. El módulo de generación de SQL no debe simplificar el árbol de comandos de consulta de salida. [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] se encargará de hacerlo, por ejemplo mediante la eliminación de combinaciones y la contracción de nodos de filtro consecutivos.  
  
 La clase <xref:System.Data.Common.DbProviderServices> es el punto inicial para tener acceso al nivel de generación de SQL para convertir árboles de comandos en <xref:System.Data.Common.DbCommand>.  
  
## <a name="in-this-section"></a>En esta sección  
 [Forma de los árboles de comandos](../../../../../docs/framework/data/adonet/ef/the-shape-of-the-command-trees.md)  
  
 [Generar SQL a partir de árboles de comandos: procedimientos recomendados](../../../../../docs/framework/data/adonet/ef/generating-sql-from-command-trees-best-practices.md)  
  
 [Generación de SQL en el proveedor de ejemplo](../../../../../docs/framework/data/adonet/ef/sql-generation-in-the-sample-provider.md)  
  
## <a name="see-also"></a>Vea también

- [Escribir un proveedor de datos de Entity Framework](../../../../../docs/framework/data/adonet/ef/writing-an-ef-data-provider.md)
