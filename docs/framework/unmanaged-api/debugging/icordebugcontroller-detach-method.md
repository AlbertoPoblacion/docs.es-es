---
title: ICorDebugController::Detach (Método)
ms.date: 03/30/2017
api_name:
- ICorDebugController.Detach
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugController::Detach
helpviewer_keywords:
- Detach method, ICorDebugController interface [.NET Framework debugging]
- ICorDebugController::Detach method [.NET Framework debugging]
ms.assetid: 06fae364-f2c6-4a50-aa7e-3da9f2684dc3
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: f687e48413cb227ad715720e24bd645065309553
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/10/2019
ms.locfileid: "67748845"
---
# <a name="icordebugcontrollerdetach-method"></a>ICorDebugController::Detach (Método)
Desasocia al depurador desde el dominio de aplicación o proceso.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
HRESULT Detach ();  
```  
  
## <a name="remarks"></a>Comentarios  
 El proceso o dominio de aplicación continúa la ejecución con normalidad, pero el objeto "ICorDebugProcess" o "ICorDebugAppDomain" ya no es válido y no se producirá ninguna devolución de llamada adicional.  
  
 En la versión 2.0 de .NET Framework, si está habilitada la depuración no administrada, este método se producirá un error debido a limitaciones del sistema operativo.  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Consulte [Requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado**: CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **Versiones de .NET Framework:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Vea también
