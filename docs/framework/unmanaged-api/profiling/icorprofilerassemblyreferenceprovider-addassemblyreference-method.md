---
title: ICorProfilerAssemblyReferenceProvider::AddAssemblyReference (Método)
ms.date: 03/30/2017
dev_langs:
- cpp
api_name:
- ICorProfilerAssemblyReferenceProvider.AddAssemblyReference
api_location:
- mscorwks.dll
api_type:
- COM
ms.assetid: 3d5af8e7-c337-48f4-9fa6-97c83878b9b1
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: ae7d896ee8e06921d685fad9ae2fcc0ac215d64a
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/06/2019
ms.locfileid: "57485062"
---
# <a name="icorprofilerassemblyreferenceprovideraddassemblyreference-method"></a>ICorProfilerAssemblyReferenceProvider::AddAssemblyReference (Método)
[Compatible con .NET Framework 4.5.2 y versiones posteriores]  
  
 Informa a common language runtime (CLR) de una referencia de ensamblado que el generador de perfiles planea agregar en el [ICorProfilerCallback:: ModuleLoadFinished](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-moduleloadfinished-method.md) devolución de llamada.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp
HRESULT AddAssemblyReference(  
        const COR_PRF_ASSEMBLY_REFERENCE_INFO* pAssemblyRefInfo  
);  
```  
  
## <a name="parameters"></a>Parámetros  
 pAssemblyRefInfo  
 Un puntero a un [COR_PRF_ASSEMBLY_REFERENCE_INFO](../../../../docs/framework/unmanaged-api/profiling/cor-prf-assembly-reference-info-structure.md) estructura que proporciona información sobre una referencia de ensamblado que debe tener en cuenta al realizar un rastreo de cierre de referencias de ensamblado CLR.  
  
## <a name="remarks"></a>Comentarios  
 El generador de perfiles llama a este método para cada ensamblado de destino tiene previsto hacer referencia desde el ensamblado especificado en el `wszAssemblyPath` argumento de la [icorprofilercallback6:: Getassemblyreferences](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback6-getassemblyreferences-method.md) devolución de llamada. El [ICorProfilerAssemblyReferenceProvider](../../../../docs/framework/unmanaged-api/profiling/icorprofilerassemblyreferenceprovider-interface.md) objeto de interfaz se pasa al generador de perfiles [icorprofilercallback6:: Getassemblyreferences](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback6-getassemblyreferences-method.md) devolución de llamada, junto con la ruta de acceso de ensamblado y el nombre en el `wszAssemblyPath` argumento.  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Consulte [Requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado**: CorProf.idl, CorProf.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **Versiones de .NET Framework:** [!INCLUDE[net_current_v452plus](../../../../includes/net-current-v452plus-md.md)]  
  
## <a name="see-also"></a>Vea también
- [ICorProfilerAssemblyReferenceProvider (interfaz)](../../../../docs/framework/unmanaged-api/profiling/icorprofilerassemblyreferenceprovider-interface.md)
- [GetAssemblyReferences (método)](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback6-getassemblyreferences-method.md)
- [ModuleLoadFinished (método)](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-moduleloadfinished-method.md)
