---
title: LoggingLevelEnum (Enumeración)
ms.date: 03/30/2017
api_name:
- LoggingLevelEnum
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- LoggingLevelEnum
helpviewer_keywords:
- LoggingLevelEnum enumeration [.NET Framework debugging]
ms.assetid: 09daac08-005a-46b2-beab-408d0820c5e5
topic_type:
- apiref
ms.openlocfilehash: 01e1eafd9955a0876f77e34eb73c2a3fc6d815c2
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/30/2019
ms.locfileid: "73139204"
---
# <a name="logginglevelenum-enumeration"></a>LoggingLevelEnum (Enumeración)
Indica el nivel de gravedad de un mensaje descriptivo que se escribe en el registro de eventos cuando un subproceso administrado registra un evento.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
typedef enum LoggingLevelEnum {  
    LTraceLevel0 = 0,  
    LTraceLevel1,  
    LTraceLevel2,  
    LTraceLevel3,  
    LTraceLevel4,  
    LStatusLevel0 = 20,  
    LStatusLevel1,  
    LStatusLevel2,  
    LStatusLevel3,  
    LStatusLevel4,  
    LWarningLevel = 40,  
    LErrorLevel = 50,  
    LPanicLevel = 100  
} LoggingLevelEnum;  
```  
  
## <a name="members"></a>Miembros  
  
|Miembro|Descripción|  
|------------|-----------------|  
|`LTraceLevel0`|El mensaje es un nivel de seguimiento 0.|  
|`LTraceLevel1`|El mensaje es un nivel de seguimiento 1.|  
|`LTraceLevel2`|El mensaje es un nivel de seguimiento 2.|  
|`LTraceLevel3`|El mensaje es un nivel de seguimiento 3.|  
|`LTraceLevel4`|El mensaje es un nivel de seguimiento 4.|  
|`LStatusLevel0`|El mensaje es un nivel de estado 0.|  
|`LStatusLevel1`|El mensaje es un nivel de estado 1.|  
|`LStatusLevel2`|El mensaje es un nivel de estado 2.|  
|`LStatusLevel3`|El mensaje es un nivel de estado 3.|  
|`LStatusLevel4`|El mensaje es un nivel de estado 4.|  
|`LWarningLevel`|El mensaje es un nivel de advertencia.|  
|`LErrorLevel`|El mensaje es un nivel de error.|  
|`LPanicLevel`|El mensaje es un nivel de pánico.|  
  
## <a name="remarks"></a>Comentarios  
 El Common Language Runtime (CLR) llama al método [ICorDebugManagedCallback:: LogMessage](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback-logmessage-method.md) para notificar al depurador que un subproceso administrado ha registrado un evento. El CLR pasa un valor de la enumeración `LoggingLevelEnum` para indicar el nivel de gravedad del mensaje que el subproceso administrado escribió en el registro de eventos.  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Vea [Requisitos de sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **Versiones de .NET Framework:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Vea también

- <xref:System.Diagnostics.EventLog>
- [Enumeraciones de depuración](../../../../docs/framework/unmanaged-api/debugging/debugging-enumerations.md)
