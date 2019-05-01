---
title: 3552 - MaxPendingMessagesPerChannelExceeded
ms.date: 03/30/2017
ms.assetid: fc8309d9-eb3a-4636-a6f0-dd0018c1361d
ms.openlocfilehash: a163ed216cbdfbf2b9d77d25979733d6bdb121d3
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61945943"
---
# <a name="3552---maxpendingmessagesperchannelexceeded"></a>3552 - MaxPendingMessagesPerChannelExceeded
## <a name="properties"></a>Propiedades  
  
|||  
|-|-|  
|ID|3552|  
|Palabras clave|Cuota, WFServices|  
|Nivel|Advertencia|  
|Canal|Microsoft-Windows-Application Server-Applications/Analytic|  
  
## <a name="description"></a>Descripción  
 Indica que se alcanzó la limitación de 'MaxPendingMessagesPerChannel'.  
  
## <a name="message"></a>Mensaje  
 Se alcanzó el límite de ' maxpendingmessagesperchannel ' de '%1'. Para aumentar este límite, ajuste la propiedad MaxPendingMessagesPerChannel en BufferedReceiveServiceBehavior.  
  
## <a name="details"></a>Detalles  
  
|Nombre del elemento de datos|Tipo del elemento de datos|Descripción|  
|--------------------|--------------------|-----------------|  
|Limit|xs:string|Se alcanzó la limitación de MaxPendingMessagesPerChannel.|  
|AppDomain|xs:string|La cadena devuelta por AppDomain.CurrentDomain.FriendlyName.|
