---
title: Excepciones en las transacciones
ms.date: 03/30/2017
ms.assetid: 1d27ed51-7eda-477f-9eca-94fa129f3e07
ms.openlocfilehash: 85d8d043a5610743d6cbad4d950330ed4bedb502
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61936986"
---
# <a name="transaction-exceptions"></a>Excepciones en las transacciones
En este tema se enumera todas las excepciones generadas por transacciones de Windows Communication Foundation (WCF).  
  
## <a name="exception-list"></a>Lista de excepciones  
  
|Código de recurso|Cadena de recurso|  
|-------------------|---------------------|  
|SFxCannotHaveDifferentTransactionProtocolsInOneBinding|La información de la directiva que se importa a partir de los metadatos especifica valores diferentes para TransactionProtocol entre las operaciones. Se admite solo un TransactionProtocol para cada punto de conexión.|  
|SFxTransactionAutoCompleteFalseAndInstanceContextMode|TransactionAutoComplete no puede ser falso a menos que el InstanceContextMode del servicio sea PerSession. Se encontró un error en la implementación del contrato y operación especificados.|  
|SFxTransactionInvalidSetTransactionComplete|Se puede llamar a OperationContext.SetTransactionComplete en una operación solo cuando TransactionAutoComplete está establecido como falso y TransactionScopeRequired está establecido como verdadero. Éste es un escenario no válido y se finalizó la transacción actual.|  
|TransactionFlowRequiredIssuedTokens|Para el flujo de una transacción, también deben admitirse los tokens emitidos del flujo.|  
|TrustDriverVersionDoesNotSupportIssuedTokens|La versión configurada de Trust no admite tokens emitidos. Utilice WSTrustFeb2005 o posterior.|
