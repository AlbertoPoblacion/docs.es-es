---
title: ICorConfiguration::SetDebuggerThreadControl (Método)
ms.date: 03/30/2017
api_name:
- ICorConfiguration.SetDebuggerThreadControl
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- SetDebuggerThreadControl
helpviewer_keywords:
- SetDebuggerThreadControl method [.NET Framework hosting]
- ICorConfiguration::SetDebuggerThreadControl method [.NET Framework hosting]
ms.assetid: 1ded7639-dacb-4db1-961c-d1ceaec01959
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: ebbc076f52c661a394eff51954fceefe8e439ded
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/10/2019
ms.locfileid: "67779889"
---
# <a name="icorconfigurationsetdebuggerthreadcontrol-method"></a>ICorConfiguration::SetDebuggerThreadControl (Método)
Establece la interfaz de devolución de llamada que se llamará los servicios de depuración como subprocesos de common language runtime (CLR) se bloquea y desbloquea para la depuración.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
HRESULT SetDebuggerThreadControl (  
    [in] IDebuggerThreadControl* pDebuggerThreadControl  
);  
```  
  
## <a name="parameters"></a>Parámetros  
 `pDebuggerThreadControl`  
 [in] Un puntero a un [IDebuggerThreadControl](../../../../docs/framework/unmanaged-api/hosting/idebuggerthreadcontrol-interface.md) objeto que notifica al host el bloqueo y desbloqueo de subprocesos por los servicios de depuración.  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Consulte [Requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado**: MSCorEE.h  
  
 **Biblioteca:** Incluye como recurso en MSCorEE.dll  
  
 **Versiones de .NET Framework:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Vea también

- [ICorConfiguration (interfaz)](../../../../docs/framework/unmanaged-api/hosting/icorconfiguration-interface.md)
