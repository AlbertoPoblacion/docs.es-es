---
title: Resolución de marcadores para WorkflowHostingEndpoint
ms.date: 03/30/2017
ms.assetid: 97fd5816-935e-4625-ad04-e6f6befa07de
ms.openlocfilehash: 4676b3c624a7ba1539a7a12ed38c286f688dcf9f
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62005581"
---
# <a name="bookmark-resolver-for-workflowhostingendpoint"></a>Resolución de marcadores para WorkflowHostingEndpoint
En este ejemplo se muestra cómo se puede utilizar <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint> con <xref:System.ServiceModel.Activities.WorkflowServiceHost> para crear instancias de flujo de trabajo.  
  
## <a name="demonstrates"></a>Demostraciones  
 <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint>, <xref:System.ServiceModel.Activities.WorkflowServiceHost>  
  
## <a name="discussion"></a>Discusión  
 Este ejemplo usa <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint> para crear instancias de flujo de trabajo hospedadas mediante <xref:System.ServiceModel.Activities.WorkflowServiceHost>. <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint> es un punto de extensibilidad para <xref:System.ServiceModel.Activities.WorkflowServiceHost> que se puede usar en los escenarios siguientes:  
  
-   Crear instancias de flujo de trabajo.  
  
-   Reanudar marcadores en una instancia de flujo de trabajo hospedada en un <xref:System.ServiceModel.Activities.WorkflowServiceHost>.  
  
 El extremo de ejemplo que se incluye expone un contrato que proporciona operaciones para crear un flujo de trabajo y devuelve el Id. de instancia o crea una instancia con un identificador concreto. La aplicación de consola de ejemplo crea una instancia de <xref:System.ServiceModel.Activities.WorkflowServiceHost> con una definición de flujo de trabajo y agrega un `CreationEndpoint` al host. A continuación, llama a la operación `Create` en el punto de conexión para crear una instancia de flujo de trabajo.  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>Configurar, compilar y ejecutar el ejemplo  
  
1. Compile la solución.  
  
2. Ejecute la aplicación. La consola `CreationEndpoint` muestra un mensaje que incluye el Id. de instancia cuando se crea la instancia de flujo de trabajo. El mensaje "Hello World!" Imprime la instancia de flujo de trabajo.  
  
> [!IMPORTANT]
>  Puede que los ejemplos ya estén instalados en su equipo. Compruebe el siguiente directorio (predeterminado) antes de continuar.  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  Si no existe este directorio, vaya a [Windows Communication Foundation (WCF) y Windows Workflow Foundation (WF) Samples para .NET Framework 4](https://go.microsoft.com/fwlink/?LinkId=150780) para descargar todos los Windows Communication Foundation (WCF) y [!INCLUDE[wf1](../../../../includes/wf1-md.md)] ejemplos. Este ejemplo se encuentra en el siguiente directorio.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WF\Basic\Execution\CreationEndpoint`
