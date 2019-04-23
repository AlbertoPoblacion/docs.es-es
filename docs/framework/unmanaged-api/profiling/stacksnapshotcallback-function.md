---
title: StackSnapshotCallback (Función)
ms.date: 03/30/2017
api_name:
- StackSnapshotCallback
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- StackSnapshotCallback
helpviewer_keywords:
- StackSnapshotCallback function [.NET Framework profiling]
ms.assetid: d0f235b2-91fe-4f82-b7d5-e5c64186eea8
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 891423661f45a1167d53385e6e0306fb09487278
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59198327"
---
# <a name="stacksnapshotcallback-function"></a>StackSnapshotCallback (Función)
Proporciona el generador de perfiles con información sobre cada marco administrado y cada ejecución de los marcos no administrados en la pila durante un recorrido de pila, que se inicia mediante la [ICorProfilerInfo2:: DoStackSnapshot](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-dostacksnapshot-method.md) método.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
HRESULT __stdcall StackSnapshotCallback (  
    [in] FunctionID funcId,  
    [in] UINT_PTR ip,  
    [in] COR_PRF_FRAME_INFO frameInfo,  
    [in] ULONG32 contextSize,  
    [in] BYTE context[],  
    [in] void *clientData  
);  
```  
  
## <a name="parameters"></a>Parámetros  
 `funcId`  
 [in] Si este valor es cero, esta devolución de llamada es para una ejecución de marcos no administrados; en caso contrario, es el identificador de una función administrada y esta devolución de llamada es para un marco administrado.  
  
 `ip`  
 [in] El valor de puntero de instrucción de código nativo en el marco.  
  
 `frameInfo`  
 [in] Un `COR_PRF_FRAME_INFO` valor al que hace referencia a información sobre el marco de pila. Este valor es válido para su uso solo durante esta devolución de llamada.  
  
 `contextSize`  
 [in] El tamaño de la `CONTEXT` estructura, que hace referencia el `context` parámetro.  
  
 `context`  
 [in] Un puntero a Win32 `CONTEXT` estructura que representa el estado de la CPU para este marco.  
  
 El `context` parámetro sólo es válido si se pasó el marcador COR_PRF_SNAPSHOT_CONTEXT `ICorProfilerInfo2::DoStackSnapshot`.  
  
 `clientData`  
 [in] Un puntero a los datos de cliente, que se pasan directamente a través de `ICorProfilerInfo2::DoStackSnapshot`.  
  
## <a name="remarks"></a>Comentarios  
 El `StackSnapshotCallback` función se implementa el sistema de escritura del generador de perfiles. Debe limitar la complejidad del trabajo realizado `StackSnapshotCallback`. Por ejemplo, al usar `ICorProfilerInfo2::DoStackSnapshot` de forma asincrónica, el subproceso de destino puede mantener bloqueos. Si el código dentro de `StackSnapshotCallback` requiere los mismos bloqueos, puede producirse un interbloqueo.  
  
 El `ICorProfilerInfo2::DoStackSnapshot` llamadas al método el `StackSnapshotCallback` función una vez por cada marco administrado o una vez por cada ejecución de marcos no administrados. Si `StackSnapshotCallback` se llama para una ejecución de marcos no administrados, el generador de perfiles puede utilizar el contexto del registro (que se hace referencia mediante el `context` parámetro) para realizar su propio recorrido de pila no administrado. En este caso, Win32 `CONTEXT` estructura representa el estado de la CPU para el marco insertado más recientemente en la ejecución de los marcos no administrados. Aunque Win32 `CONTEXT` estructura incluye valores para todos los registros, debe confiar sólo en los valores de registro de puntero de marco, el registro de puntero de pila, registro de puntero de instrucción y la no volátil (es decir, conservada) registros de enteros.  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Consulte [Requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado**: CorProf.idl  
  
 **Biblioteca:** CorGuids.lib  
  
 **Versiones de .NET Framework:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Vea también

- [DoStackSnapshot (método)](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-dostacksnapshot-method.md)
- [Funciones estáticas globales para generación de perfiles](../../../../docs/framework/unmanaged-api/profiling/profiling-global-static-functions.md)
