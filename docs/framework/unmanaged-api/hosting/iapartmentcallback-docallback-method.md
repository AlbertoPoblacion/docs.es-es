---
title: IApartmentCallback::DoCallback (Método)
ms.date: 03/30/2017
api_name:
- IApartmentCallback.DoCallback
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- DoCallback
helpviewer_keywords:
- IApartmentCallback::DoCallback method [.NET Framework hosting]
- DoCallback method [.NET Framework hosting]
ms.assetid: 8edad30c-30ff-4bee-813c-75525a82fc93
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 80aa64a8867a84100996ae88c5e65233d6b15782
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/06/2019
ms.locfileid: "57481075"
---
# <a name="iapartmentcallbackdocallback-method"></a>IApartmentCallback::DoCallback (Método)
Ejecuta la función especificada dentro de un apartamento.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
HRESULT _stdcall DoCallback(  
    [in] SIZE_T pFunc,  
    [in] SIZE_T pData  
);  
```  
  
## <a name="parameters"></a>Parámetros  
 `pFunc`  
 [in] Un puntero a la función que se ejecuta en el apartamento.  
  
 `pData`  
 [in] Un puntero al argumento de la función.  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Consulte [Requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado**: MSCorEE.h  
  
 **Biblioteca:** Incluye como recurso en MSCorEE.dll  
  
 **Versiones de .NET Framework:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Vea también
- [IApartmentCallback (interfaz)](../../../../docs/framework/unmanaged-api/hosting/iapartmentcallback-interface.md)
