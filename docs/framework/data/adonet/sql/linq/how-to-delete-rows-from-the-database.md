---
title: Filtrar para eliminar filas de la base de datos
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 2144c99b-8055-4080-a5c6-1ea14335e2a3
ms.openlocfilehash: 401d445e49e3712b8c59fa9bc9a2e53500a5db16
ms.sourcegitcommit: 558d78d2a68acd4c95ef23231c8b4e4c7bac3902
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/09/2019
ms.locfileid: "59331681"
---
# <a name="how-to-delete-rows-from-the-database"></a>Filtrar para eliminar filas de la base de datos
Puede eliminar filas en una base de datos mediante la eliminación de la correspondiente [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] objetos de su colección relacionada con la tabla. [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] Convierte los cambios en el código SQL apropiado `DELETE` comandos.  
  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] no admite ni reconoce las operaciones de eliminación en cascada. Si desea eliminar una fila de una tabla que tiene restricciones, deberá realizar una de las siguientes tareas:  
  
-   Establezca la regla `ON DELETE CASCADE` en la restricción de clave externa de la base de datos.  
  
-   Utilice su propio código para eliminar primero los objetos secundarios que impiden que se elimine el objeto primario.  
  
 De lo contrario, se inicia una excepción. Vea el segundo ejemplo de código que se muestra más adelante en este tema.  
  
> [!NOTE]
>  Puede invalidar los métodos predeterminados de [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] para las operaciones de base de datos `Insert`, `Update` y `Delete`. Para obtener más información, consulte [personalizar Insert, Update y las operaciones de eliminación](../../../../../../docs/framework/data/adonet/sql/linq/customizing-insert-update-and-delete-operations.md).  
>   
>  Los desarrolladores que usan Visual Studio pueden usar el [!INCLUDE[vs_ordesigner_long](../../../../../../includes/vs-ordesigner-long-md.md)] para desarrollar procedimientos almacenados para el mismo propósito.  
  
 En los pasos siguientes se asume que un objeto <xref:System.Data.Linq.DataContext> válido le conecta a la base de datos Northwind. Para obtener más información, vea [Cómo: Conectarse a una base de datos](../../../../../../docs/framework/data/adonet/sql/linq/how-to-connect-to-a-database.md).  
  
### <a name="to-delete-a-row-in-the-database"></a>Para eliminar una fila en la base de datos  
  
1. Consulte en la base de datos la fila que se va a eliminar.  
  
2. Llame al método <xref:System.Data.Linq.Table%601.DeleteOnSubmit%2A>.  
  
3. Envíe el cambio a la base de datos.  
  
## <a name="example"></a>Ejemplo  
 En este primer ejemplo de código se consultan en la base de datos los detalles del pedido #11000, se marcan dichos detalles para eliminarlos y se envían estos cambios a la base de datos.  
  
 [!code-csharp[System.Data.Linq.Table#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/system.data.linq.table/cs/program.cs#3)]
 [!code-vb[System.Data.Linq.Table#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/system.data.linq.table/vb/module1.vb#3)]  
  
## <a name="example"></a>Ejemplo  
 En este segundo ejemplo, el objetivo es quitar un pedido (#10250). En primer lugar, el código examina la tabla `OrderDetails` para comprobar si el pedido que se va a quitar tiene elementos secundarios en ésta. Si el pedido tiene elementos secundarios, se marcan primero los elementos secundarios y después el pedido para eliminarlos. El objeto <xref:System.Data.Linq.DataContext> coloca las eliminaciones en el orden correcto para que los comandos de eliminación enviados a la base de datos cumplan las restricciones de la misma.  
  
 [!code-csharp[DLinqCascadeWorkaround#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqCascadeWorkaround/cs/Program.cs#1)]
 [!code-vb[DLinqCascadeWorkaround#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqCascadeWorkaround/vb/Module1.vb#1)]  
  
## <a name="see-also"></a>Vea también

- [Filtrar para administrar conflictos de cambios](../../../../../../docs/framework/data/adonet/sql/linq/how-to-manage-change-conflicts.md)
- [Filtrar Asignación de procedimientos almacenados para realizar actualizaciones, inserciones y eliminaciones (Object Relational Designer)](/visualstudio/data-tools/how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-o-r-designer)
- [Realizar y enviar cambios de datos](../../../../../../docs/framework/data/adonet/sql/linq/making-and-submitting-data-changes.md)
