---
title: ICLRStrongName::StrongNameGetBlob (Método)
ms.date: 03/30/2017
api_name:
- ICLRStrongName.StrongNameGetBlob
- ICLRStrongName.StrongNameGetBlob
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRStrongName::StrongNameGetBlob
helpviewer_keywords:
- ICLRStrongName::StrongNameGetBlob method [.NET Framework hosting]
- StrongNameGetBlob method, ICLRStrongName interface [.NET Framework hosting]
ms.assetid: a24218f8-7196-44be-b7a2-ee9cdd7a85c4
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 38b6785afae75888398f1c0d3d69be2ce21d67bd
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59160789"
---
# <a name="iclrstrongnamestrongnamegetblob-method"></a>ICLRStrongName::StrongNameGetBlob (Método)
Llena el búfer especificado con la representación binaria del archivo ejecutable en la dirección especificada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
HRESULT StrongNameGetBlob (  
    [in]  LPCWSTR    wszFilePath,  
    [in]  BYTE       *pbBlob,  
    [in, out] DWORD  *pcbBlob  
);  
```  
  
## <a name="parameters"></a>Parámetros  
 `wszFilePath`  
 [in] Una ruta de acceso válida para el archivo ejecutable que se va a cargar.  
  
 `pbBlob`  
 [in] Búfer en el que se va a cargar el archivo ejecutable.  
  
 `pcbBlob`  
 [in, out] El solicita el tamaño máximo, en bytes, de `pbBlob`. Cuando se devuelve, el tamaño real, en bytes, de `pbBlob`.  
  
## <a name="return-value"></a>Valor devuelto  
 `S_OK` Si el método se completó correctamente; en caso contrario, un valor HRESULT que indica un error (consulte [valores HRESULT comunes](https://go.microsoft.com/fwlink/?LinkId=213878) para obtener una lista).  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Consulte [Requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado**: MetaHost.h  
  
 **Biblioteca:** Incluye como recurso en MSCorEE.dll  
  
 **Versiones de .NET Framework:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Vea también

- [StrongNameGetBlobFromImage (método)](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-strongnamegetblobfromimage-method.md)
- [ICLRStrongName (interfaz)](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-interface.md)
