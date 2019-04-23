---
title: ICorProfilerCallback4::MovedReferences2 (Método)
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback4.MovedReferences2
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback4::MovedReferences2
helpviewer_keywords:
- MovedReferences2 method, ICorProfilerCallback4 interface [.NET Framework profiling]
- ICorProfilerCallback4::MovedReferences2 method [.NET Framework profiling]
ms.assetid: d17a065b-5bc6-4817-b3e1-1e413fcb33a8
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: d368c88503853d0620f28f02f88a6d887c1aa681
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59156408"
---
# <a name="icorprofilercallback4movedreferences2-method"></a>ICorProfilerCallback4::MovedReferences2 (Método)
Se le llama para informar de la nueva distribución de los objetos del montón como resultado de una recolección de elementos no utilizados con compactación. Este método se llama si el generador de perfiles ha implementado la [ICorProfilerCallback4](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback4-interface.md) interfaz. Esta devolución de llamada reemplaza el [MovedReferences](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-movedreferences-method.md) método, porque puede informar sobre intervalos más grandes de objetos cuyas longitudes superen lo que se puede expresar en ULONG.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
HRESULT MovedReferences2(  
    [in]  ULONG  cMovedObjectIDRanges,  
    [in, size_is(cMovedObjectIDRanges)] ObjectID oldObjectIDRangeStart[] ,  
    [in, size_is(cMovedObjectIDRanges)] ObjectID newObjectIDRangeStart[] ,  
    [in, size_is(cMovedObjectIDRanges)] SIZE_T    cObjectIDRangeLength[] );  
```  
  
## <a name="parameters"></a>Parámetros  
 `cMovedObjectIDRanges`  
 [in] Número de bloques de objetos contiguos que se movieron como resultado de la recolección de elementos no utilizados con compactación. Es decir, el valor de `cMovedObjectIDRanges` es el tamaño total de las matrices `oldObjectIDRangeStart`, `newObjectIDRangeStart` y `cObjectIDRangeLength`.  
  
 Los tres argumentos siguientes de `MovedReferences2` son matrices paralelas. En otras palabras, `oldObjectIDRangeStart[i]`, `newObjectIDRangeStart[i]` y `cObjectIDRangeLength[i]` hacen referencia a un único bloque de objetos contiguos.  
  
 `oldObjectIDRangeStart`  
 [in] Matriz de valores `ObjectID`, cada uno de los cuales es la dirección inicial antigua (antes de la recolección de elementos no utilizados) de un bloque de objetos contiguos activos en la memoria.  
  
 `newObjectIDRangeStart`  
 [in] Matriz de valores `ObjectID`, cada uno de los cuales es la dirección inicial nueva (después de la recolección de elementos no utilizados) de un bloque de objetos contiguos activos en la memoria.  
  
 `cObjectIDRangeLength`  
 [in] Matriz de enteros, cada uno de los cuales es el tamaño de un bloque de objetos contiguos en la memoria.  
  
 Se especifica un tamaño para cada bloque al que se hace referencia en las matrices `oldObjectIDRangeStart` y `newObjectIDRangeStart`.  
  
## <a name="remarks"></a>Comentarios  
 Un recolector de elementos no utilizados con compactación recupera la memoria ocupada por los objetos inactivos y compacta ese espacio liberado. Como resultado, los objetos activos podrían moverse dentro del montón y los valores de `ObjectID` distribuidos por notificaciones anteriores podrían cambiar.  
  
 Supongamos que un valor `ObjectID` existente (`oldObjectID`) se encuentra dentro del intervalo siguiente:  
  
 `oldObjectIDRangeStart[i]` <= `oldObjectID` < `oldObjectIDRangeStart[i]` + `cObjectIDRangeLength[i]`  
  
 En este caso, el desplazamiento desde el inicio del intervalo al inicio del objeto es el siguiente:  
  
 `oldObjectID` - `oldObjectRangeStart[i]`  
  
 Para cualquier valor de `i` que esté en el intervalo siguiente:  
  
 0 <= `i` < `cMovedObjectIDRanges`  
  
 puede calcular el nuevo `ObjectID` de la siguiente manera:  
  
 `newObjectID` = `newObjectIDRangeStart[i]` + (`oldObjectID` – `oldObjectIDRangeStart[i]`)  
  
 Ninguno de los valores `ObjectID` pasados por `MovedReferences2` son válidos durante la devolución de llamada en sí porque el recolector de elementos no utilizados puede estar en pleno proceso de mover objetos desde ubicaciones anteriores a ubicaciones nuevas. Por lo tanto, los generadores de perfiles no deben intentar inspeccionar objetos durante una llamada a `MovedReferences2`. Un [ICorProfilerCallback2:: GarbageCollectionFinished](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-garbagecollectionfinished-method.md) devolución de llamada indica que todos los objetos se han movido a sus nuevas ubicaciones y se puede realizar la inspección.  
  
 Si el generador de perfiles implementa tanto la [ICorProfilerCallback](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md) y [ICorProfilerCallback4](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback4-interface.md) interfaces, la `MovedReferences2` se llama al método antes de la [ICorProfilerCallback:: MovedReferences](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-movedreferences-method.md) método, pero solo si el `MovedReferences2` método devuelve correctamente. Los generadores de perfiles pueden devolver un HRESULT que indica un error del método `MovedReferences2` para evitar llamar al segundo método.  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Consulte [Requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado**: CorProf.idl, CorProf.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **Versiones de .NET Framework:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>Vea también

- [ICorProfilerCallback (interfaz)](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md)
- [MovedReferences (método)](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-movedreferences-method.md)
- [ICorProfilerCallback4 (interfaz)](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback4-interface.md)
- [Interfaces para generación de perfiles](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)
- [Generación de perfiles](../../../../docs/framework/unmanaged-api/profiling/index.md)
