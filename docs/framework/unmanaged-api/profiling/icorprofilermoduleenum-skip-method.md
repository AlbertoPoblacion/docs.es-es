---
title: ICorProfilerModuleEnum::Skip (Método)
ms.date: 03/30/2017
api_name:
- ICorProfilerModuleEnum.Skip Method
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerModuleEnum::Skip
helpviewer_keywords:
- Skip method, ICorProfilerModuleEnum interface [.NET Framework profiling]
- ICorProfilerModuleEnum::Skip method [.NET Framework profiling]
ms.assetid: 8dc29c6a-e2ba-41d8-a1e0-0fdd21421e0b
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: eecb2a5da9dddaccbab7fcc6d74af6e4c6bfb72c
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/10/2019
ms.locfileid: "67775128"
---
# <a name="icorprofilermoduleenumskip-method"></a>ICorProfilerModuleEnum::Skip (Método)
Desplaza el cursor del enumerador desde su posición actual de manera que se omita el número especificado de elementos.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
HRESULT Skip([in] ULONG celt);  
```  
  
## <a name="parameters"></a>Parámetros  
 `celt`  
 [in] El número de elementos que se van a omitir.  
  
## <a name="return-value"></a>Valor devuelto  
 Este método devuelve los siguientes HRESULT específicos y los errores HRESULT que indican un error del método.  
  
|HRESULT|DESCRIPCIÓN|  
|-------------|-----------------|  
|S_OK|`celt` se omitieron los elementos.|  
|S_FALSE|Menos de `celt` se omitieron los elementos, lo que indica que no hay ningún elemento más.|  
  
## <a name="remarks"></a>Comentarios  
 La nueva posición del cursor de este enumerador es (posición actual) + `celt`.  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Consulte [Requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado**: CorProf.idl, CorProf.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **Versiones de .NET Framework:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Vea también

- [ICorProfilerModuleEnum (interfaz)](../../../../docs/framework/unmanaged-api/profiling/icorprofilermoduleenum-interface.md)
- [Interfaces para generación de perfiles](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)
