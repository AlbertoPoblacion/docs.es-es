---
title: ICorProfilerCallback::ExceptionThrown (Método)
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.ExceptionThrown
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::ExceptionThrown
helpviewer_keywords:
- ExceptionThrown method [.NET Framework profiling]
- ICorProfilerCallback::ExceptionThrown method [.NET Framework profiling]
ms.assetid: f1a23f3b-ac21-4905-8abf-8ea59f15af53
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: e9cdbc2234519c0dba1a5004246492e7609ea2b3
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2019
ms.locfileid: "59180497"
---
# <a name="icorprofilercallbackexceptionthrown-method"></a>ICorProfilerCallback::ExceptionThrown (Método)
Notifica al generador de perfiles que se ha producido una excepción.  
  
> [!NOTE]
>  Esta función se invoca sólo si la excepción llega a código administrado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
HRESULT ExceptionThrown(  
    [in] ObjectID thrownObjectId);  
```  
  
## <a name="parameters"></a>Parámetros  
 `thrownObjectId`  
 [in] El identificador del objeto que produjo la excepción que se produzca.  
  
## <a name="remarks"></a>Comentarios  
 El generador de perfiles no debe bloquearse en su implementación de este método porque la pila no puede estar en un estado que permita la recolección de elementos y, por lo tanto, no se puede habilitar la recolección preferente. Si el generador de perfiles se bloquea aquí y se intenta realizar la recolección de elementos, el tiempo de ejecución se bloqueará hasta que devuelve esta devolución de llamada.  
  
 Implementación del generador de perfiles de este método no debe llamar a código administrado o en modo alguno provocar una asignación de memoria administrada.  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Consulte [Requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado**: CorProf.idl, CorProf.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **Versiones de .NET Framework:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Vea también

- [ICorProfilerCallback (Interfaz)](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md)
