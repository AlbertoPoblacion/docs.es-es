---
title: Realizar la recuperación
ms.date: 03/30/2017
ms.assetid: 6dd17bf6-ba42-460a-a44b-8046f52b10d0
ms.openlocfilehash: 149ac6b6162893de830f59b3d18008d8298eab56
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61793619"
---
# <a name="performing-recovery"></a>Realizar la recuperación
El administrador de recursos facilita la resolución de inscripciones duraderas en una transacción volviendo a inscribir al participante de la transacción después de un error de recurso.  
  
## <a name="the-recovery-process"></a>El Proceso de la recuperación  
 Para dar de alta de forma duradera a un recurso (se describe por una implementación de la interfaz <xref:System.Transactions.IEnlistmentNotification>) que puede ser después elegible para la recuperación, debería llamar al método <xref:System.Transactions.Transaction.EnlistDurable%2A>. Además, debe proporcionar un identificador del administrador de recursos (un <xref:System.Transactions.Transaction.EnlistDurable%2A>) que se utiliza para etiquetar de forma consistente al participante de la transacción en caso de un error de recurso al método <xref:System.Guid>. Por este motivo, el <xref:System.Guid> que está siempre a la inscripción inicial debería ser idéntica a llamada la *resourceManagerIdentifier* parámetro en el <xref:System.Transactions.TransactionManager.Reenlist%2A> llamar durante la recuperación. De lo contrario, se produce <xref:System.Transactions.TransactionException>. Para obtener más información sobre las inscripciones duraderas, consulte [dar de alta recursos como participantes en una transacción](../../../../docs/framework/data/transactions/enlisting-resources-as-participants-in-a-transaction.md) .  
  
 En la fase de preparación (fase 1) del  protocolo 2PC, cuando su implementación de un administrador de recursos duradero recibe la notificación <xref:System.Transactions.IEnlistmentNotification.Prepare%2A>, debería registrar su registro de preparación durante esta fase. El registro debería contener toda la información que es necesaria para completar la transacción en confirmación. El registro de preparación puede obtenerse más adelante durante la recuperación mediante la recuperación de la <xref:System.Transactions.PreparingEnlistment.RecoveryInformation%2A> propiedad de la *preparingEnlistment* devolución de llamada. El registro del registro no necesita ser realizado dentro del método <xref:System.Transactions.IEnlistmentNotification.Prepare%2A> cuando RM puede hacer esto en un subproceso de trabajo.  
  
 El proceso de recuperación consiste de los dos siguientes pasos:  
  
### <a name="step-1---reenlist"></a>El paso 1 - ReEnlist  
 El administrador de recursos examina el registro de preparación de la información para cada inscripción que está dudosa. Esto se hace examinando la propiedad <xref:System.Transactions.PreparingEnlistment.RecoveryInformation%2A> de la devolución de llamada <xref:System.Transactions.PreparingEnlistment>, que se pasa al administrador de recursos en la notificación <xref:System.Transactions.IEnlistmentNotification.Prepare%2A> durante fase 1.  
  
 Para cada inscripción que examina, invoca <xref:System.Transactions.TransactionManager.Reenlist%2A> en el administrador de transacciones. Este método pasa en un <xref:System.Guid> único que identifica el administrador de recursos, así como la información de la inscripción en una matriz de bytes. Se devuelve un objeto nuevo <xref:System.Transactions.Enlistment> . En caso de error en el reenganche con una excepción, el administrador de recursos necesitará reintentar en un momento posterior.  
  
 Solo debería llamar al <xref:System.Transactions.TransactionManager.Reenlist%2A> método si un administrador de recursos se reinicia a partir de un error. Además, solo debería volver a inscribir las transacciones sin resolver registradas por un administrador de recursos durante fase de preparación inicial de una confirmación en dos fases. Cualquier intento de llamar a este método en momentos que no corresponda puede generar resultados erróneos.  
  
 Cuando se vuelve a inscribir un participante con este método, se llama a los métodos de la fase 2 de <xref:System.Transactions.IEnlistmentNotification> que corresponden al resultado de la transacción (es decir, <xref:System.Transactions.IEnlistmentNotification.Commit%2A>, <xref:System.Transactions.IEnlistmentNotification.Rollback%2A> o <xref:System.Transactions.IEnlistmentNotification.InDoubt%2A>) según sea adecuado.  
  
### <a name="step-2---completing-the-recovery"></a>El paso 2 - Completando la recuperación  
 Cuando todas las inscripciones hayan finalizado el administrador de recursos llamará al método <xref:System.Transactions.TransactionManager.RecoveryComplete%2A>. Este método completa la recuperación e informa el administrador de transacciones de que el administrador de recursos no tiene ninguna transacción dudosa más. Haciendo esto, el administrador de recursos garantiza que no invocará de nuevo el método <xref:System.Transactions.TransactionManager.Reenlist%2A>.  
  
 No se exige a un administrador de recursos que resuelva todas las transacciones dudosas antes de dar de alta nuevas transacciones. El primer paso puede realizarse en cualquier momento después de que el Administrador de recursos establece una relación con el Administrador de transacciones, pero después <xref:System.Transactions.TransactionManager.RecoveryComplete%2A> ha sido invocar (paso 2); paso 1 no se puede realizar de nuevo. El paso 2 se puede repetir varias veces sin afectar al resultado de transacciones.
