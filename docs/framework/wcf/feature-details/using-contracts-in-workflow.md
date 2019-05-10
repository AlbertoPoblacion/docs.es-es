---
title: Utilizar contratos en flujo de trabajo
ms.date: 03/30/2017
ms.assetid: 939c64e9-e7cc-4abc-b41e-27cfce1d7e50
ms.openlocfilehash: dc2d631d8a9e588645dd60495c54799b2a2dd8a0
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2019
ms.locfileid: "64637760"
---
# <a name="using-contracts-in-workflow"></a>Utilizar contratos en flujo de trabajo
Al implementar un servicio, defina varios contratos que describan el servicio y los datos que envía y recibe. Los datos se representan como contratos de datos y los contratos de mensaje; servicios WCF y flujo de trabajo utilizan definiciones de contrato de mensaje y de contrato de datos como parte de las descripciones del servicio. El servicio expone metadatos (en el formulario de WSDL) para describir las operaciones del servicio. En WCF, los contratos de servicios y los contratos de operaciones definen el servicio y las operaciones admitidos. Sin embargo, en un servicio de flujo de trabajo, estos contratos forman parte del propio proceso de negocio; se exponen en metadatos mediante un proceso llamado inferencia del contrato.  
  
## <a name="contract-inference"></a>Inferencia del contrato  
 Cuando un servicio de flujo de trabajo se hospeda mediante <xref:System.ServiceModel.Activities.WorkflowServiceHost>, se examina la definición de flujo de trabajo y se genera un contrato en función del conjunto de actividades de mensajería presentes en el flujo de trabajo. En especial, se emplean las siguientes actividades y propiedades para generar el contrato:  
  
 Actividad <xref:System.ServiceModel.Activities.Receive>  
  
- <xref:System.ServiceModel.Activities.Receive.ServiceContractName%2A>  
  
- <xref:System.ServiceModel.Activities.Receive.OperationName%2A>
  
- <xref:System.ServiceModel.Activities.Receive.Action%2A>   
 
 Actividad <xref:System.ServiceModel.Activities.SendReply>  
  
- <xref:System.ServiceModel.Activities.SendReply.Action%2A>  
  
 Actividad <xref:System.ServiceModel.Activities.TransactedReceiveScope>  
  
 El resultado final de inferencia del contrato es una descripción del servicio mediante las mismas estructuras de datos que el servicio de WCF y los contratos de operación. A continuación, esta información se utiliza para exponer WSDL para el servicio de flujo de trabajo.  
  
## <a name="see-also"></a>Vea también

- [Servicios de flujo de trabajo](../../../../docs/framework/wcf/feature-details/workflow-services.md)
- [Actividades de mensajería](../../../../docs/framework/wcf/feature-details/messaging-activities.md)
- [Cómo: Crear un servicio de flujo de trabajo con actividades de mensajería](../../../../docs/framework/wcf/feature-details/how-to-create-a-workflow-service-with-messaging-activities.md)
- [Cómo: Crear un servicio de flujo de trabajo que consuma un contrato de servicio existente](../../../../docs/framework/windows-workflow-foundation/how-to-create-a-workflow-service-that-consumes-an-existing-service-contract.md)
