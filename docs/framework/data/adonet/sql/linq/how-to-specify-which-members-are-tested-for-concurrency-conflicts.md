---
title: Filtrar para especificar en qué miembros se comprueban los conflictos de simultaneidad
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: d2cda293-1e2f-4878-af0e-5aaf0d092120
ms.openlocfilehash: 9a1b4ab2dc28c569473eddbf50b96d10298d8d3c
ms.sourcegitcommit: 558d78d2a68acd4c95ef23231c8b4e4c7bac3902
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/09/2019
ms.locfileid: "59310439"
---
# <a name="how-to-specify-which-members-are-tested-for-concurrency-conflicts"></a>Filtrar para especificar en qué miembros se comprueban los conflictos de simultaneidad
Aplicar una de las tres enumeraciones a la [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] <xref:System.Data.Linq.Mapping.ColumnAttribute.UpdateCheck%2A> propiedad en un <xref:System.Data.Linq.Mapping.ColumnAttribute> comprueba el atributo para especificar qué miembros estarán incluidos en la actualización para la detección de conflictos de simultaneidad optimista.  
  
 La propiedad <xref:System.Data.Linq.Mapping.ColumnAttribute.UpdateCheck%2A> (asignada en tiempo de diseño) se utiliza junto con las características de simultaneidad en tiempo de ejecución de [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]. Para obtener más información, consulte [simultaneidad optimista: Información general sobre](../../../../../../docs/framework/data/adonet/sql/linq/optimistic-concurrency-overview.md).  
  
> [!NOTE]
>  Los valores de miembro originales se comparan con el estado de la base de datos actual siempre y cuando ningún miembro se designe como `IsVersion=true`. Para obtener más información, consulta <xref:System.Data.Linq.Mapping.ColumnAttribute.IsVersion%2A>.  
  
 Para obtener ejemplos de código, vea <xref:System.Data.Linq.Mapping.ColumnAttribute.UpdateCheck%2A>.  
  
### <a name="to-always-use-this-member-for-detecting-conflicts"></a>Para usar siempre este miembro para detectar los conflictos  
  
1. Agregue la propiedad <xref:System.Data.Linq.Mapping.ColumnAttribute.UpdateCheck%2A> al atributo <xref:System.Data.Linq.Mapping.ColumnAttribute>.  
  
2. Establezca el valor de propiedad <xref:System.Data.Linq.Mapping.ColumnAttribute.UpdateCheck%2A> en `Always`.  
  
### <a name="to-never-use-this-member-for-detecting-conflicts"></a>Para no usar nunca este miembro para detectar los conflictos  
  
1. Agregue la propiedad <xref:System.Data.Linq.Mapping.ColumnAttribute.UpdateCheck%2A> al atributo <xref:System.Data.Linq.Mapping.ColumnAttribute>.  
  
2. Establezca el valor de propiedad <xref:System.Data.Linq.Mapping.ColumnAttribute.UpdateCheck%2A> en `Never`.  
  
### <a name="to-use-this-member-for-detecting-conflicts-only-when-the-application-has-changed-the-value-of-the-member"></a>Para utilizar este miembro para detectar conflictos sólo cuando la aplicación cambia el valor del miembro  
  
1. Agregue la propiedad <xref:System.Data.Linq.Mapping.ColumnAttribute.UpdateCheck%2A> al atributo <xref:System.Data.Linq.Mapping.ColumnAttribute>.  
  
2. Establezca el valor de propiedad <xref:System.Data.Linq.Mapping.ColumnAttribute.UpdateCheck%2A> en `WhenChanged`.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se especifica que nunca deberían probarse los objetos `HomePage` durante las comprobaciones de actualización. Para obtener más información, consulta <xref:System.Data.Linq.Mapping.ColumnAttribute.UpdateCheck%2A>.  
  
 [!code-csharp[System.Data.Linq.Mapping.UpdateCheck#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/system.data.linq.mapping.updatecheck/cs/northwind.cs#1)]
 [!code-vb[System.Data.Linq.Mapping.UpdateCheck#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/system.data.linq.mapping.updatecheck/vb/northwind.vb#1)]  
  
## <a name="see-also"></a>Vea también

- [Filtrar para administrar conflictos de cambios](../../../../../../docs/framework/data/adonet/sql/linq/how-to-manage-change-conflicts.md)
- [Realizar y enviar cambios de datos](../../../../../../docs/framework/data/adonet/sql/linq/making-and-submitting-data-changes.md)
