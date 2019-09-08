---
title: Procedimiento Crear un servicio de datos mediante el proveedor de reflexión (WCF Data Services)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF Data Services, providers
ms.assetid: 7315c6d8-f452-4fb2-a0c1-76ab0593c146
ms.openlocfilehash: feee679c37cd3dafb80021752ee25444c54f0809
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/07/2019
ms.locfileid: "70790999"
---
# <a name="how-to-create-a-data-service-using-the-reflection-provider-wcf-data-services"></a>Procedimiento Crear un servicio de datos mediante el proveedor de reflexión (WCF Data Services)
[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] le permite definir un modelo de datos que está basado en clases arbitrarias siempre que dichas clases se expongan como objetos que implementan la interfaz <xref:System.Linq.IQueryable%601>. Para obtener más información, vea [proveedores de Data Services](data-services-providers-wcf-data-services.md).  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se define un modelo de datos que incluye `Orders` y `Items`. La clase del contenedor de entidades `OrderItemData` tiene dos métodos públicos que devuelven interfaces <xref:System.Linq.IQueryable%601>. Estas interfaces son los conjuntos de entidades de los tipos de entidad `Orders` y `Items`. Cada `Order` puede incluir varios `Items`, por lo que el tipo de entidad `Orders` tiene una propiedad de navegación `Items` que devuelve una colección de objetos `Items`. La clase del contenedor de entidades `OrderItemData` es el tipo genérico de la clase <xref:System.Data.Services.DataService%601> de la que se deriva el servicio de datos `OrderItems`.  
  
> [!NOTE]
> Dado que este ejemplo muestra un proveedor de datos en memoria y los cambios no se conservan fuera de las instancias de objeto actuales, no hay ninguna ventaja derivada de implementar la interfaz <xref:System.Data.Services.IUpdatable>. Para obtener un ejemplo que implementa la <xref:System.Data.Services.IUpdatable> interfaz, consulte [cómo: Cree un servicio de datos mediante un origen](create-a-data-service-using-linq-to-sql-wcf.md)de datos de LINQ to SQL.  
  
 [!code-csharp[Astoria Reflection Provider#CustomIQueryable](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_reflection_provider/cs/orderitems.svc.cs#customiqueryable)]
 [!code-vb[Astoria Reflection Provider#CustomIQueryable](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_reflection_provider/vb/orderitems.svc.vb#customiqueryable)]  
  
## <a name="see-also"></a>Vea también

- [Cómo: Crear un servicio de datos mediante un origen de datos de LINQ to SQL](create-a-data-service-using-linq-to-sql-wcf.md)
- [Proveedores de Data Services](data-services-providers-wcf-data-services.md)
- [Cómo: Creación de un servicio de datos mediante un origen de datos de ADO.NET Entity Framework](create-a-data-service-using-an-adonet-ef-data-wcf.md)
