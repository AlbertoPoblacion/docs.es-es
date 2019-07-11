---
title: ICorDebugNativeFrame::GetIP (Método)
ms.date: 03/30/2017
api_name:
- ICorDebugNativeFrame.GetIP
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugNativeFrame::GetIP
helpviewer_keywords:
- GetIP method, ICorDebugNativeFrame interface [.NET Framework debugging]
- ICorDebugNativeFrame::GetIP method [.NET Framework debugging]
ms.assetid: 99f693f3-d3b9-4fd8-9d09-b8efd03f7b67
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 71e9149bafc866f89253c4318ac69f2705431e48
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/10/2019
ms.locfileid: "67765306"
---
# <a name="icordebugnativeframegetip-method"></a>ICorDebugNativeFrame::GetIP (Método)
Obtiene el código nativo desplazar ubicación a la que está establecido actualmente el puntero de instrucción.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
HRESULT GetIP (  
    [out] ULONG32           *pnOffset  
);  
```  
  
## <a name="parameters"></a>Parámetros  
 `pnOffset`  
 [out] Un puntero a la ubicación de desplazamiento en el código nativo.  
  
## <a name="remarks"></a>Comentarios  
 Si el marco de pila es representado por esta instancia de "ICorDebugNativeFrame" está activo, el desplazamiento es la dirección de la siguiente instrucción que se ejecutará. Si este marco de pila no está activo, el desplazamiento es la dirección de la siguiente instrucción que se ejecutará cuando se reactiva el marco de pila.  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Consulte [Requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado**: CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **Versiones de .NET Framework:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Vea también
