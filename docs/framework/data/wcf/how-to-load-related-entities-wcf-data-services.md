---
title: Procedimiento Cargar entidades relacionadas (WCF Data Services)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF Data Services, deferred content
- WCF Data Services, loading data
ms.assetid: 6f143d30-d997-4e6b-bcf0-d5c394ecb108
ms.openlocfilehash: 14b0ba988c96c270610208a4f944083bb333eac5
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/07/2019
ms.locfileid: "70780026"
---
# <a name="how-to-load-related-entities-wcf-data-services"></a>Procedimiento Cargar entidades relacionadas (WCF Data Services)
Cuando necesite cargar entidades asociadas en [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)], puede usar el método <xref:System.Data.Services.Client.DataServiceContext.LoadProperty%2A> de la clase <xref:System.Data.Services.Client.DataServiceContext>. También puede utilizar el <xref:System.Data.Services.Client.DataServiceQuery%601.Expand%2A> método <xref:System.Data.Services.Client.DataServiceQuery%601> en para requerir que las entidades relacionadas se carguen diligentemente en la misma respuesta de la consulta.  
  
 En el ejemplo de este tema se usa el servicio de datos de ejemplo Northwind y las clases del servicio de datos de cliente generadas automáticamente. Este servicio y las clases de datos de cliente se crean al completar la guía de [Inicio rápido de WCF Data Services](quickstart-wcf-data-services.md).  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se muestra cómo cargar explícitamente la entidad `Customer` relacionada con cada instancia de `Orders` devuelta.  
  
 [!code-csharp[Astoria Northwind Client#LoadRelatedOrderCustomer](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#loadrelatedordercustomer)]
 [!code-vb[Astoria Northwind Client#LoadRelatedOrderCustomer](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#loadrelatedordercustomer)]  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se muestra cómo usar el método <xref:System.Data.Services.Client.DataServiceQuery%601.Expand%2A> para devolver las entidades `Order Details` pertenecientes a las entidades `Orders` devueltas por la consulta.  
  
 [!code-csharp[Astoria Northwind Client#ExpandOrderDetails](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#expandorderdetails)]
 [!code-vb[Astoria Northwind Client#ExpandOrderDetails](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#expandorderdetails)]  
  
## <a name="see-also"></a>Vea también

- [Consultar el servicio de datos](querying-the-data-service-wcf-data-services.md)
