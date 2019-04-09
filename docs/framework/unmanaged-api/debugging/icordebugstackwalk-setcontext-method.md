---
title: ICorDebugStackWalk::SetContext (Método)
ms.date: 03/30/2017
api_name:
- ICorDebugStackWalk.SetContext Method
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugStackWalk::SetContext
helpviewer_keywords:
- SetContext method [.NET Framework debugging]
- ICorDebugStackWalk::SetContext method [.NET Framework debugging]
ms.assetid: bac0b156-31a3-4e7f-be4d-ab21789c81f1
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 7306ee61d750ae256c93c049819a23d3d61f7297
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2019
ms.locfileid: "59116472"
---
# <a name="icordebugstackwalksetcontext-method"></a>ICorDebugStackWalk::SetContext (Método)
Establece el [ICorDebugStackWalk](../../../../docs/framework/unmanaged-api/debugging/icordebugstackwalk-interface.md) contexto actual del objeto en un contexto válido para el subproceso.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
HRESULT SetContext([in] CorDebugSetContextFlag flag,  
                   [in] ULONG32 contextSize,  
                   [in, size_is(contextSize)] BYTE context[]);  
```  
  
## <a name="parameters"></a>Parámetros  
 `flag`  
 [in] Un [CorDebugSetContextFlag](../../../../docs/framework/unmanaged-api/debugging/cordebugsetcontextflag-enumeration.md) marca que indica si el contexto procede del marco activo de la pila o un contexto obtenido desenredando la pila.  
  
 `contextSize`  
 [in] El tamaño asignado de la `CONTEXT` búfer.  
  
 `context`  
 [in] El `CONTEXT` búfer.  
  
## <a name="return-value"></a>Valor devuelto  
 Este método devuelve los siguientes HRESULT específicos y los errores HRESULT que indican un error del método.  
  
|HRESULT|Descripción|  
|-------------|-----------------|  
|S_OK|El `ICorDebugStackWalk` contexto del objeto se ha establecido correctamente.|  
|E_FAIL|El `ICorDebugStackWalk` no se ha establecido el contexto del objeto.|  
|E_INVALIDARG|El contexto es null.|  
|HRESULT_FROM_WIN32(ERROR_INSUFFICIENT_BUFFER)|El búfer de contexto es demasiado pequeño.|  
  
## <a name="exceptions"></a>Excepciones  
  
## <a name="remarks"></a>Comentarios  
 Este método no modifica el contexto del subproceso actual.  
  
 Establecer el contexto actual en un contexto no válido, puede producir resultados imprevisibles desde el Rastreador de pila.  
  
 Puede recuperar una copia bit a bit exacta de este contexto llamando inmediatamente el [ICorDebugStackWalk:: GetContext](../../../../docs/framework/unmanaged-api/debugging/icordebugstackwalk-getcontext-method.md) método.  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Consulte [Requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado**: CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **Versiones de .NET Framework:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Vea también

- [Interfaces para depuración](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
- [Depuración](../../../../docs/framework/unmanaged-api/debugging/index.md)
