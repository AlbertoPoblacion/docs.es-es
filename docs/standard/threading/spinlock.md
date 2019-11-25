---
title: SpinLock
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- synchronization primitives, SpinLock
ms.assetid: f9af93bb-7a0d-4ba5-afe8-74f48b6b6958
ms.openlocfilehash: eac9a1be38ea81e8ccee1d05d9061ceeb597627f
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/30/2019
ms.locfileid: "73106164"
---
# <a name="spinlock"></a>SpinLock
La estructura <xref:System.Threading.SpinLock> es un primitivo de sincronización de exclusión mutua y de bajo nivel que itera mientras espera a que se adquiera un bloqueo. En los equipos con varios núcleos, cuando se prevea que los tiempos de espera van ser breves y si la contención es mínima, <xref:System.Threading.SpinLock> puede funcionar mejor que otros tipos de bloqueos. Sin embargo, se recomienda usar <xref:System.Threading.SpinLock> solo cuando determine mediante la generación de perfiles que el método <xref:System.Threading.Monitor?displayProperty=nameWithType> o los métodos <xref:System.Threading.Interlocked> reducen significativamente el rendimiento del programa.  
  
 <xref:System.Threading.SpinLock> puede generar el intervalo de tiempo del subproceso incluso si aún no ha adquirido el bloqueo. Esto se hace para evitar la inversión de prioridades del subproceso y para permitir que el recolector de elementos no utilizados progrese. Cuando se usa <xref:System.Threading.SpinLock>, asegúrese de que ningún subproceso mantenga el bloqueo durante más de un intervalo de tiempo muy breve y que ningún subproceso puede bloquearse mientras mantiene el bloqueo.  
  
 Como SpinLock es un tipo de valor, explícitamente debe pasarlo por referencia si pretende que las dos copias hagan referencia al mismo bloqueo.  
  
 Para obtener más información acerca de cómo utilizar este tipo, vea <xref:System.Threading.SpinLock?displayProperty=nameWithType>. Como ejemplo, vea [Cómo: para usar SpinLock para la sincronización de bajo nivel](../../../docs/standard/threading/how-to-use-spinlock-for-low-level-synchronization.md).  
  
 <xref:System.Threading.SpinLock> admite un modo *thread*-*tracking* que puede usar durante la fase de desarrollo para ayudar a realizar un seguimiento del subproceso que está reteniendo el bloqueo en un momento determinado. El modo de seguimiento de subprocesos es muy útil para la depuración, pero se recomienda apagarlo en la versión de lanzamiento del programa porque puede ralentizar el rendimiento. Para obtener más información, vea [Cómo: para habilitar el modo de seguimiento de subprocesos en el bloqueo SpinLock](../../../docs/standard/threading/how-to-enable-thread-tracking-mode-in-spinlock.md).  
  
## <a name="see-also"></a>Vea también

- [Objetos y características de subprocesos](../../../docs/standard/threading/threading-objects-and-features.md)
