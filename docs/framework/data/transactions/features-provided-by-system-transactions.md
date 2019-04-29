---
title: Características proporcionadas por System.Transactions
ms.date: 03/30/2017
ms.assetid: e458cef9-63b5-4401-b448-1536dcd9d9e5
ms.openlocfilehash: 6fc20f8249f37f69689fb3fc6b3144792badad3c
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61793697"
---
# <a name="features-provided-by-systemtransactions"></a>Características proporcionadas por System.Transactions
En esta sección se describe cómo se pueden utilizar las características proporcionadas por el espacio de nombres <xref:System.Transactions> para escribir su propia aplicación transaccional y administrador de recursos. Específicamente, esta sección trata de cómo crear y participar en una transacción (local o distribuida) con uno o varios participantes.  
  
## <a name="overview-of-systemtransactions"></a>Información general sobre System.Transactions  
 La infraestructura proporcionada por las clases en el espacio de nombres <xref:System.Transactions> hace que la programación transaccional sea sencilla y eficaz en toda la plataforma al admitir las transacciones iniciadas en SQL Server, ADO.NET, Message Queuing (MSMQ) y MSDTC (Coordinador de transacciones distribuidas de Microsoft). El espacio de nombres <xref:System.Transactions> proporciona un modelo de programación explícito según la clase <xref:System.Transactions.Transaction>, así como un modelo de programación implícito utilizando la clase <xref:System.Transactions.TransactionScope>, en la que la infraestructura administra automáticamente las transacciones. Para obtener más información sobre cómo crear una aplicación transaccional utilizando estos dos modelos, vea [crear una aplicación transaccional](../../../../docs/framework/data/transactions/writing-a-transactional-application.md).  
  
 El espacio de nombres <xref:System.Transactions> también proporciona tipos para implementar un administrador de recursos. Un administrador de recursos administra los datos duraderos o volátiles que se utilizan en una transacción, y trabaja en cooperación con el administrador de transacciones para dotar a la aplicación de una garantía de atomicidad y aislamiento. El administrador de transacciones que proporciona la infraestructura <xref:System.Transactions> admite transacciones que implican varios recursos volátiles o un recurso duradero único. Para obtener más información sobre la implementación de un administrador de recursos, consulte [implementar un administrador de recursos](../../../../docs/framework/data/transactions/implementing-a-resource-manager.md).  
  
 Cuando un administrador de recursos duraderos adicional se da de alta a sí mismo en una transacción, el administrador de transacciones también dirige de forma transparente las transacciones locales a transacciones distribuidas, coordinando con un administrador de transacciones basado en disco como DTC. La infraestructura <xref:System.Transactions> proporciona un rendimiento mejorado principalmente de dos formas:  
  
- Subida dinámica, que asegura que la infraestructura <xref:System.Transactions> solo activa el MSDTC cuando una transacción abarca varios recursos distribuidos. Para obtener más información sobre la elevación dinámica. consulte [subida de administración de la transacción](../../../../docs/framework/data/transactions/transaction-management-escalation.md) tema.  
  
- Inscripciones de ascenso, que permiten que un recurso, como una base de datos, asuma la propiedad de la transacción si es la única entidad que participa en la transacción. Posteriormente, si resulta necesario, la infraestructura <xref:System.Transactions> aún puede dirigir la administración de la transacción a la MSDTC. Esto reduce aún más la oportunidad de utilizar MSDTC. Las inscripciones promocionales se tratan en profundidad en el tema[optimización con la confirmación de fase única y fase única Promovible](../../../../docs/framework/data/transactions/optimization-spc-and-promotable-spn.md).  
  
 El espacio de nombres <xref:System.Transactions> define tres niveles de confianza - AllowPartiallyTrustedCallers (APTCA), DistributedTransactionPermission (DTP) y plena confianza - que restringe el acceso a los tipos de recursos que expone. Para obtener más información acerca de los diversos niveles de confianza, vea [niveles de confianza de seguridad de acceso a recursos](../../../../docs/framework/data/transactions/security-trust-levels-in-accessing-resources.md).  
  
## <a name="in-this-section"></a>En esta sección  
  
### <a name="writing-a-transactional-application"></a>Crear una aplicación transaccional  
 El espacio de nombres <xref:System.Transactions> proporciona dos modelos para crear aplicaciones transaccionales. [Implementar una transacción implícita mediante el ámbito de transacción](../../../../docs/framework/data/transactions/implementing-an-implicit-transaction-using-transaction-scope.md) describe cómo el <xref:System.Transactions> espacio de nombres admite crear transacciones implícitas mediante la <xref:System.Transactions.TransactionScope> clase.  
  
 [Implementación de una transacción explícita utilizando CommittableTransaction](../../../../docs/framework/data/transactions/implementing-an-explicit-transaction-using-committabletransaction.md) describe cómo el <xref:System.Transactions> espacio de nombres admite crear transacciones implícitas mediante la <xref:System.Transactions.CommittableTransaction> clase.  
  
 Para consultar otros temas que abarcan escribir una aplicación transaccional, vea [crear una aplicación transaccional](../../../../docs/framework/data/transactions/writing-a-transactional-application.md).  
  
### <a name="implementing-a-resource-manager"></a>Implementar un administrador de recursos  
 Para implementar un administrador de recursos que puede participar en una transacción, vea [implementar un administrador de recursos](../../../../docs/framework/data/transactions/implementing-a-resource-manager.md). En esta sección trata la inscripción de un recurso, la confirmación de transacciones, la recuperación después del error, y los procedimientos recomendados de la optimización.
