---
title: FunctionLeave3WithInfo (Función)
ms.date: 03/30/2017
api_name:
- FunctionLeave3WithInfo
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- FunctionLeave3WithInfo
helpviewer_keywords:
- FunctionLeave3WithInfo function [.NET Framework profiling]
ms.assetid: 5fa68a67-ced6-41c6-a2c0-467060fd0692
topic_type:
- apiref
ms.openlocfilehash: a62f402fbfae6188ab0423ea7a55a4dfc6cb4112
ms.sourcegitcommit: 9a39f2a06f110c9c7ca54ba216900d038aa14ef3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/23/2019
ms.locfileid: "74427402"
---
# <a name="functionleave3withinfo-function"></a>FunctionLeave3WithInfo (Función)
Notifica al generador de perfiles que el control se devuelve desde una función y proporciona un identificador que se puede pasar al [método ICorProfilerInfo3:: GetFunctionLeave3Info (](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-getfunctionleave3info-method.md) para recuperar el marco de pila y el valor devuelto.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
void __stdcall FunctionLeave3WithInfo(  
               [in] FunctionIDOrClientID functionIDOrClientID,  
               [in] COR_PRF_ELT_INFO eltInfo);  
```  
  
## <a name="parameters"></a>Parámetros  
 `functionIDOrClientID`  
 de Identificador de la función de la que se devuelve el control.  
  
 `eltInfo`  
 [in] Controlador opaco que representa información sobre un marco de pila determinado. Este identificador es válido solo durante la devolución de llamada a la que se pasa.  
  
## <a name="remarks"></a>Comentarios  
 El método de devolución de llamada `FunctionLeave3WithInfo` notifica al generador de perfiles cuando se llama a las funciones y permite al generador de perfiles usar el [método ICorProfilerInfo3:: GetFunctionLeave3Info (](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-getfunctionleave3info-method.md) para inspeccionar el valor devuelto. Para tener acceso a la información del valor devuelto, se debe establecer la marca `COR_PRF_ENABLE_FUNCTION_RETVAL`. El generador de perfiles puede utilizar el [método ICorProfilerInfo:: SetEventMask](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-seteventmask-method.md) para establecer las marcas de evento y, a continuación, usar el [método ICorProfilerInfo3:: SetEnterLeaveFunctionHooks3WithInfo (](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-setenterleavefunctionhooks3withinfo-method.md) para registrar la implementación de esta función.  
  
 La función `FunctionLeave3WithInfo` es una devolución de llamada; debe implementarla. La implementación de debe utilizar el atributo de clase de almacenamiento `__declspec(naked)`.  
  
 El motor de ejecución no guarda ningún registro antes de llamar a esta función.  
  
- En la entrada, debe guardar todos los registros que use, incluidos los de la unidad de punto flotante (FPU).  
  
- Al salir, debe restaurar la pila desactivando todos los parámetros insertados por el autor de la llamada.  
  
 La implementación de `FunctionLeave3WithInfo` no debe bloquearse porque retrasará la recolección de elementos no utilizados. La implementación no debe intentar una recolección de elementos no utilizados, porque es posible que la pila no esté en un estado reconocible para la recolección de elementos no utilizados. Si se intenta realizar una recolección de elementos no utilizados, el tiempo de ejecución se bloqueará hasta que `FunctionLeave3WithInfo` devuelva.  
  
 La función `FunctionLeave3WithInfo` no debe llamar a código administrado ni producir una asignación de memoria administrada de ninguna manera.  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Vea [Requisitos de sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado:** Corprof. idl  
  
 **Biblioteca:** CorGuids.lib  
  
 **Versiones de .NET Framework:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Vea también

- [Getfunctionleave3info (](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-getfunctionleave3info-method.md)
- [FunctionEnter3](../../../../docs/framework/unmanaged-api/profiling/functionenter3-function.md)
- [FunctionLeave3](../../../../docs/framework/unmanaged-api/profiling/functionleave3-function.md)
- [FunctionTailcall3](../../../../docs/framework/unmanaged-api/profiling/functiontailcall3-function.md)
- [FunctionEnter3WithInfo](../../../../docs/framework/unmanaged-api/profiling/functionenter3withinfo-function.md)
- [FunctionTailcall3WithInfo](../../../../docs/framework/unmanaged-api/profiling/functiontailcall3withinfo-function.md)
- [Setenterleavefunctionhooks3 (](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-setenterleavefunctionhooks3-method.md)
- [Setenterleavefunctionhooks3withinfo (](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-setenterleavefunctionhooks3withinfo-method.md)
- [Setfunctionidmapper (](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-setfunctionidmapper-method.md)
- [Setfunctionidmapper2 (](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-setfunctionidmapper2-method.md)
- [Funciones estáticas globales para generación de perfiles](../../../../docs/framework/unmanaged-api/profiling/profiling-global-static-functions.md)
