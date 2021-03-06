---
title: Contadores de rendimiento de los servicios
ms.date: 03/30/2017
ms.assetid: 4210f549-31f2-4ea7-99bd-69eaffb98ddf
ms.openlocfilehash: bf0b12e6d4954c0a1392554d7269a7d539a77dc1
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/23/2019
ms.locfileid: "54545600"
---
# <a name="service-performance-counters"></a>Contadores de rendimiento de los servicios
Los contadores de rendimiento del servicio miden el conjunto del comportamiento del servicio y se utilizan para diagnosticar el rendimiento de todo el servicio. Se pueden encontrar bajo el objeto de rendimiento `ServiceModelService 4.0.0.0` al visualizarlo mediante el monitor de rendimiento (Perfmon.exe). Los nombres de las instancias se establecen utilizando el siguiente patrón:  
  
```  
ServiceName@ServiceBaseAddress  
```  
  
> [!CAUTION]
>  Hay un límite en la longitud del nombre de una instancia del contador de rendimiento. Cuando un nombre de instancia del contador de Windows Communication Foundation (WCF) supera la longitud máxima, WCF reemplaza una parte del nombre de instancia con un valor hash.  
  
## <a name="see-also"></a>Vea también
- [Contadores de rendimiento](../../../../../docs/framework/wcf/diagnostics/performance-counters/index.md)
