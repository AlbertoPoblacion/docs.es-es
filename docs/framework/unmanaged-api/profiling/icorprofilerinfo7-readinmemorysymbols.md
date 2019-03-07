---
title: ICorProfilerInfo7::ReadInMemorySymbols
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo7.ReadInMemorySymbols
api_location:
- CorProf.idl
- CorProf.h
- CorGuids.lib
api_type:
- COM
ms.assetid: 1745a0b9-8332-4777-a670-b549bff3b901
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 4f42345977f69dd27294a44b4c007ab08d2ec6f6
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/06/2019
ms.locfileid: "57468356"
---
# <a name="icorprofilerinfo7readinmemorysymbols"></a>ICorProfilerInfo7::ReadInMemorySymbols
[compatible con la versión [!INCLUDE[net_v461](../../../../includes/net-v461-md.md)] y posteriores]  
  
 Lee los bytes de una secuencia de símbolos en memoria.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
HRESULT ReadInMemorySymbols(  
        [in] ModuleID moduleId,  
        [in] DWORD symbolsReadOffset,  
        [out] BYTE* pSymbolBytes,  
        [in] DWORD countSymbolBytes,  
        [out] DWORD* pCountSymbolBytesRead  
);  
```  
  
## <a name="parameters"></a>Parámetros  
 `moduleId`  
 [in] El identificador del módulo que contiene la secuencia en memoria.  
  
 `symbolsReadOffset`  
 [in] El desplazamiento dentro de la secuencia en memoria en el que se va a empezar a leer los bytes.  
  
 `pSymbolBytes`  
 [out] Un puntero al búfer al que se copiarán los datos. Debe tener el búfer `countSymbolBytes` de espacio disponible.  
  
 `countSymbolBytes`  
 [in] El número de bytes para copiar.  
  
 `pCountSymbolBytesRead`  
 [out] Cuando el método vuelve, contiene el número real de bytes leídos.  
  
## <a name="return-value"></a>Valor devuelto  
 `S_OK`, si un número distinto de cero de bytes leído.  
  
 `CORPROF_E_MODULE_IS_DYNAMIC`, si se creó el módulo mediante <xref:System.Reflection.Emit>.  
  
## <a name="remarks"></a>Comentarios  
 El `ReadInMemorySymbols` método intenta leer `countSymbolBytes` de datos empezando en el desplazamiento `symbolsReadOffset` dentro de la secuencia en memoria. Los datos se copian a `pSymbolBytes`, que se espera que tenga `countSymbolBytes` de espacio disponible.     `pCountSymbolsBytesRead` contiene el número real de bytes leídos, que puede ser menor que `countSymbolBytes` si se alcanza el final de la secuencia.  
  
> [!NOTE]
>  La implementación actual no admite Reflection.Emit. Si se creó el módulo mediante Reflection.Emit, el método devuelve `CORPROF_E_MODULE_IS_DYNAMIC`.  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Consulte [Requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado**: CorProf.idl, CorProf.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **Versiones de .NET Framework:** [!INCLUDE[net_current_v461plus](../../../../includes/net-current-v461plus-md.md)]  
  
## <a name="see-also"></a>Vea también
- [ICorProfilerInfo7 (interfaz)](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo7-interface.md)
