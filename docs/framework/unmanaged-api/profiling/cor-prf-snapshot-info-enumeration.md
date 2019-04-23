---
title: COR_PRF_SNAPSHOT_INFO (Enumeración)
ms.date: 03/30/2017
api_name:
- COR_PRF_SNAPSHOT_INFO
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- COR_PRF_SNAPSHOT_INFO
helpviewer_keywords:
- COR_PRF_SNAPSHOT_INFO enumeration [.NET Framework profiling]
ms.assetid: a5906b2a-ad4a-4cc6-a421-2d7d8adf7468
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: fa85fb2cebb47ecbd7b0f091cb79f6ea0936b1cb
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59177845"
---
# <a name="corprfsnapshotinfo-enumeration"></a>COR_PRF_SNAPSHOT_INFO (Enumeración)
Especifica cuánto hacer una copia de datos para pasar con una instantánea de pila en cada llamada al generador de perfiles [StackSnapshotCallback](../../../../docs/framework/unmanaged-api/profiling/stacksnapshotcallback-function.md) función.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
typedef enum _COR_PRF_SNAPSHOT_INFO {  
    COR_PRF_SNAPSHOT_DEFAULT = 0x0,  
    COR_PRF_SNAPSHOT_REGISTER_CONTEXT = 0x1,  
    COR_PRF_SNAPSHOT_X86_OPTIMIZED = 0X2  
} COR_PRF_SNAPSHOT_INFO;  
```  
  
## <a name="members"></a>Miembros  
  
|Miembros|Descripción|  
|-------------|-----------------|  
|`COR_PRF_SNAPSHOT_DEFAULT`|Indica que se deben pasar valores para todos los `StackSnapshotCallback` parámetros, excepto el `context` parámetro.|  
|`COR_PRF_SNAPSHOT_REGISTER_CONTEXT`|Indica que se deben pasar valores para todos los `StackSnapshotCallback` parámetros, incluido el `context` parámetro.|  
|`COR_PRF_SNAPSHOT_X86_OPTIMIZED`|Indica que se usará un algoritmo de recorrido de pila más sencillo y alternativo.|  
  
## <a name="remarks"></a>Comentarios  
 Los valores proporcionados por el `COR_PRF_SNAPSHOT_INFO` enumeración se pasan como parámetros a la [DoStackSnapshot](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-dostacksnapshot-method.md) método.  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Consulte [Requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado**: CorProf.idl, CorProf.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **Versiones de .NET Framework:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Vea también

- [DoStackSnapshot (método)](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-dostacksnapshot-method.md)
- [Enumeraciones para generación de perfiles](../../../../docs/framework/unmanaged-api/profiling/profiling-enumerations.md)
