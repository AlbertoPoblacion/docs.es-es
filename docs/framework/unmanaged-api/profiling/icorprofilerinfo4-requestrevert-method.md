---
title: ICorProfilerInfo4::RequestRevert (Método)
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo4.RequestRevert
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo4::RequestRevert
helpviewer_keywords:
- RequestRevert method, ICorProfilerInfo4 interface [.NET Framework profiling]
- ICorProfilerInfo4::RequestRevert method [.NET Framework profiling]
ms.assetid: 70261da5-5933-4e25-9de0-ddf51cba56cc
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 92137e1a5b0923bc34745513715934c483616700
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62000498"
---
# <a name="icorprofilerinfo4requestrevert-method"></a>ICorProfilerInfo4::RequestRevert (Método)
Revierte todas las instancias de las funciones especificadas a sus versiones originales.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
HRESULT RequestRevert (  
   [in] ULONG    cFunctions,  
   [in, size_is(cFunctions)]  ModuleID    moduleIds[],  
   [in, size_is(cFunctions)]  mdMethodDef methodIds[],  
   [out, size_is(cFunctions)]  HRESULT status[]);  
```  
  
## <a name="parameters"></a>Parámetros  
 `cFunctions`  
 [in] Número de funciones que se va a revertir.  
  
 `moduleIds`  
 [in] Especifica la parte `moduleId` de los pares (`module`, `methodDef`) que identifican las funciones que se van a revertir.  
  
 `methodIds`  
 [in] Especifica la parte `methodId` de los pares (`module`, `methodDef`) que identifican las funciones que se van a revertir.  
  
 `status`  
 [out] Matriz de valores HRESULT enumerados en la sección "HRESULT de estado" más adelante en este tema. Cada HRESULT indica el intento correcto o erróneo de revertir cada función especificada en las matrices paralelas `moduleIds` y `methodIds`.  
  
## <a name="return-value"></a>Valor devuelto  
 Este método devuelve los siguientes HRESULT específicos y los errores HRESULT que indican un error del método.  
  
|HRESULT|Descripción|  
|-------------|-----------------|  
|S_OK|Se intentaron revertir todas las solicitudes; sin embargo, se debe comprobar la matriz de estados devueltos para determinar qué funciones se han revertido correctamente.|  
|CORPROF_E_CALLBACK4_REQUIRED|El generador de perfiles debe implementar la [ICorProfilerCallback4](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback4-interface.md) interfaz para esta llamada que se deben admitir.|  
|CORPROF_E_REJIT_NOT_ENABLED|No se habilitó la recompilación con JIT. Debe habilitar recompilación con JIT durante la inicialización mediante el [ICorProfilerInfo:: SetEventMask](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-seteventmask-method.md) método para establecer el `COR_PRF_ENABLE_REJIT` marca.|  
|E_INVALIDARG|`cFunctions` es 0, o `moduleIds` o `methodIds` es `NULL`.|  
|E_OUTOFMEMORY|El CLR no pudo completar la solicitud porque se quedó sin memoria.|  
  
## <a name="status-hresults"></a>HRESULT de estado  
  
|HRESULT de la matriz de estados|Descripción|  
|--------------------------|-----------------|  
|S_OK|La función correspondiente se revirtió correctamente.|  
|E_INVALIDARG|El parámetro `moduleID` o `methodDef` es `NULL`.|  
|CORPROF_E_DATAINCOMPLETE|El módulo no está totalmente cargado aún o está en proceso de descarga.|  
|CORPROF_E_MODULE_IS_DYNAMIC|El módulo especificado se genera dinámicamente (por ejemplo, mediante `Reflection.Emit`). Por lo tanto, este método no lo admite.|  
|CORPROF_E_ACTIVE_REJIT_REQUEST_NOT_FOUND|El CLR no pudo revertir la función especificada porque no se encontró la solicitud de recompilación activa correspondiente. La recompilación nunca se solicitó o la función ya se había revertido.|  
|Otros|El sistema operativo devolvió un error fuera del control del CLR. Por ejemplo, si se produce un error en una llamada del sistema para cambiar la protección de acceso de una página de memoria, se mostrará el error del sistema operativo.|  
  
## <a name="remarks"></a>Comentarios  
 La próxima vez que se llame a cualquiera de las instancias de la función revertida, se ejecutarán las versiones originales de las funciones. Si ya se está ejecutando una función, finalizará la ejecución de la versión que se está ejecutando.  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Consulte [Requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado**: CorProf.idl, CorProf.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **Versiones de .NET Framework:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>Vea también

- [ICorProfilerInfo4 (interfaz)](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo4-interface.md)
- [Interfaces para generación de perfiles](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)
- [Generación de perfiles](../../../../docs/framework/unmanaged-api/profiling/index.md)
