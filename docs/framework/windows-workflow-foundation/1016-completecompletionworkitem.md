---
title: 1016 - CompleteCompletionWorkItem
ms.date: 03/30/2017
ms.assetid: 246929fb-6f14-440a-814b-cd8349350644
ms.openlocfilehash: 3f0904a561a242cd3be528c9707a409b6f98e0fe
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61925091"
---
# <a name="1016---completecompletionworkitem"></a>1016 - CompleteCompletionWorkItem
## <a name="properties"></a>Propiedades  
  
|||  
|-|-|  
|ID|1016|  
|Palabras clave|WFRuntime|  
|Nivel|Detallado|  
|Canal|Microsoft-Windows-Application Server-Applications/Debug|  
  
## <a name="description"></a>Descripción  
 Indica que se ha completado un CompletionWorkItem.  
  
## <a name="message"></a>Mensaje  
 Un CompletionWorkItem se ha completado para la actividad primaria '%1', DisplayName: '%2', InstanceId: '%3'. Actividad completada '%4', DisplayName: '%5', InstanceId: '%6'.  
  
## <a name="details"></a>Detalles  
  
|Nombre del elemento de datos|Tipo del elemento de datos|Descripción|  
|--------------------|--------------------|-----------------|  
|ParentActivity|xs:string|Nombre del tipo de la actividad principal.|  
|ParentDisplayName|xs:string|Identificación y nombre para mostrar de la actividad principal.|  
|ParentInstanceId|xs:string|Identificador de instancia de la actividad principal.|  
|CompletedActivity|xs:string|El nombre del tipo de la actividad que se completó.|  
|CompletedActivityDisplayName|xs:string|Nombre para mostrar de la actividad que se ha completado.|  
|CompletedActivityInstanceId|xs:string|Identificador de instancia de la actividad que se ha completado.|  
|AppDomain|xs:string|La cadena devuelta por AppDomain.CurrentDomain.FriendlyName.|
