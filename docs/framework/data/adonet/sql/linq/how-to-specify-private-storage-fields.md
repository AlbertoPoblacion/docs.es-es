---
title: Procedimiento para especificar campos de almacenamiento privado
ms.date: 03/30/2017
ms.assetid: 5a40e816-cc6e-43a0-b32a-9caaa0ab6912
ms.openlocfilehash: 843b7ae8dbddb76e0e5fa33d3594a5655dbf1a37
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59302457"
---
# <a name="how-to-specify-private-storage-fields"></a>Procedimiento para especificar campos de almacenamiento privado
Use la [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] <xref:System.Data.Linq.Mapping.DataAttribute.Storage%2A> propiedad en el <xref:System.Data.Linq.Mapping.DataAttribute> atributo para designar el nombre de un campo de almacenamiento subyacente.  
  
 Para obtener ejemplos de código, vea <xref:System.Data.Linq.Mapping.DataAttribute.Storage%2A>.  
  
### <a name="to-specify-the-name-of-an-underlying-storage-field"></a>Para especificar el nombre de un campo de almacenamiento subyacente  
  
1. Agregue la propiedad <xref:System.Data.Linq.Mapping.DataAttribute.Storage%2A> al atributo <xref:System.Data.Linq.Mapping.ColumnAttribute>.  
  
2. Asigne el nombre del campo como valor de la propiedad <xref:System.Data.Linq.Mapping.DataAttribute.Storage%2A>.  
  
## <a name="see-also"></a>Vea también

- [Modelo de objetos de LINQ to SQL](../../../../../../docs/framework/data/adonet/sql/linq/the-linq-to-sql-object-model.md)
- [Cómo: Personalizar las clases de entidad mediante el Editor de código](../../../../../../docs/framework/data/adonet/sql/linq/how-to-customize-entity-classes-by-using-the-code-editor.md)
