---
title: ETaskType (Enumeración)
ms.date: 03/30/2017
api_name:
- ETaskType
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ETaskType
helpviewer_keywords:
- ETaskType enumeration [.NET Framework hosting]
ms.assetid: aa527b31-89d4-41f2-ad6f-63b76950b7df
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: f256195a4cd5b18f568e05156db867aa5dba9161
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61627968"
---
# <a name="etasktype-enumeration"></a>ETaskType (Enumeración)
Contiene valores que indican el tipo de tarea que se representa mediante un [ICLRTask](../../../../docs/framework/unmanaged-api/hosting/iclrtask-interface.md) o un [IHostTask](../../../../docs/framework/unmanaged-api/hosting/ihosttask-interface.md) interfaz.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
typedef enum ETaskType {  
    TT_DEBUGGERHELPER           = 0x1,  
    TT_GC                       = 0x2,  
    TT_FINALIZER                = 0x4,  
    TT_THREADPOOL_TIMER         = 0x8,  
    TT_THREADPOOL_GATE          = 0x10,  
    TT_THREADPOOL_WORKER        = 0x20,  
    TT_THREADPOOL_IOCOMPLETION  = 0x40,  
    TT_ADUNLOAD                 = 0x80,  
    TT_USER                     = 0x100,  
    TT_THREADPOOL_WAIT          = 0x200,  
    TT_UNKNOWN                  = 0x80000000  
} ETaskType;  
```  
  
## <a name="members"></a>Miembros  
  
|Miembro|Descripción|  
|------------|-----------------|  
|`TT_ADUNLOAD`|La interfaz representa una tarea de descarga del dominio de aplicación.|  
|`TT_DEBUGGERHELPER`|La interfaz representa una tarea de la aplicación auxiliar de depurador.|  
|`TT_FINALIZER`|La interfaz representa una tarea de finalizador.|  
|`TT_GC`|La interfaz representa una tarea de recopilación de elementos no utilizados.|  
|`TT_THREADPOOL_GATE`|La interfaz representa una tarea de subproceso de la puerta.|  
|`TT_THREADPOOL_IOCOMPLETION`|La interfaz representa una tarea de subproceso de E/S o una tarea de subproceso de puerto de finalización.|  
|`TT_THREADPOOL_TIMER`|La interfaz representa una tarea de subproceso de temporizador.|  
|`TT_THREADPOOL_WAIT`|La interfaz representa una tarea de espera de subproceso.|  
|`TT_THREADPOOL_WORKER`|La interfaz representa una tarea de subproceso de trabajo.|  
|`TT_UNKNOWN`|La tarea es desconocida.|  
|`TT_USER`|La interfaz representa una tarea de usuario.|  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Consulte [Requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado**: MSCorEE.h  
  
 **Biblioteca:** MSCorEE.dll  
  
 **Versiones de .NET Framework:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Vea también

- [Enumeraciones para hosts](../../../../docs/framework/unmanaged-api/hosting/hosting-enumerations.md)
