---
title: IMetaDataTables::GetNextGuid (Método)
ms.date: 03/30/2017
api_name:
- IMetaDataTables.GetNextGuid
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataTables::GetNextGuid
helpviewer_keywords:
- GetNextGuid method [.NET Framework metadata]
- IMetaDataTables::GetNextGuid method [.NET Framework metadata]
ms.assetid: 68f6ea4d-9112-4d6b-93d9-e34f1e2f2496
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 345c43b5a6e3c185b5e8070e9d6e1c1443673149
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/10/2019
ms.locfileid: "67781468"
---
# <a name="imetadatatablesgetnextguid-method"></a>IMetaDataTables::GetNextGuid (Método)
Obtiene el índice del siguiente valor de GUID de la columna de tabla actual.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
HRESULT GetNextGuid (  
    [in]  ULONG   ixGuid,  
    [out] ULONG   *pNext  
);  
```  
  
## <a name="parameters"></a>Parámetros  
 `ixGuid`  
 [in] El valor de índice de una columna de tabla GUID.  
  
 `pNext`  
 [out] Un puntero al índice del siguiente valor de GUID.  
  
## <a name="remarks"></a>Comentarios  
 No se recomienda el uso de este método, porque no devuelve resultados coherentes. Para obtener información acerca de la tabla GUID, consulte la documentación de Common Language Infrastructure (CLI), especialmente "Partition II: Definición de metadatos y la semántica". La documentación está disponible en línea; vea [ECMA C# and Common Language Infrastructure Standards](https://go.microsoft.com/fwlink/?LinkID=99212) (Estándares de ECMA C# y Common Language Infrastructure) en MSDN y [Standard ECMA-335 - Common Language Infrastructure (CLI)](https://go.microsoft.com/fwlink/?LinkID=65552) (Estándar ECMA-335: Common Language Infrastructure [CLI]) en el sitio web de Ecma International.  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Consulte [Requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado**: Cor.h  
  
 **Biblioteca:** Usar como un recurso en MsCorEE.dll  
  
 **Versiones de .NET Framework:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Vea también

- [IMetaDataTables (interfaz)](../../../../docs/framework/unmanaged-api/metadata/imetadatatables-interface.md)
- [IMetaDataTables2 (interfaz)](../../../../docs/framework/unmanaged-api/metadata/imetadatatables2-interface.md)
