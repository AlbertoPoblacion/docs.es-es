---
title: ICLRStrongName::StrongNameGetPublicKey (Método)
ms.date: 03/30/2017
api_name:
- ICLRStrongName.StrongNameGetPublicKey
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRStrongName::StrongNameGetPublicKey
helpviewer_keywords:
- StrongNameGetPublicKey method, ICLRStrongName interface [.NET Framework hosting]
- ICLRStrongName::StrongNameGetPublicKey method [.NET Framework hosting]
ms.assetid: a31dcaa9-a404-4c1d-8cc7-081827c52935
topic_type:
- apiref
ms.openlocfilehash: 943251357a91ea9ae3d492fa7bf20eebf948b8b2
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/30/2019
ms.locfileid: "73135076"
---
# <a name="iclrstrongnamestrongnamegetpublickey-method"></a>ICLRStrongName::StrongNameGetPublicKey (Método)
Obtiene la clave pública de un par de claves pública y privada. El par de claves se puede proporcionar como un nombre de contenedor de claves dentro de un proveedor de servicios criptográficos (CSP) o como una colección de bytes sin procesar.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
HRESULT StrongNameGetPublicKey (   
    [in]  LPCWSTR   szKeyContainer,  
    [in]  BYTE      *pbKeyBlob,  
    [in]  ULONG     cbKeyBlob,  
    [out] BYTE      **ppbPublicKeyBlob,  
    [out] ULONG     *pcbPublicKeyBlob  
);  
```  
  
## <a name="parameters"></a>Parámetros  
 `szKeyContainer`  
 de Nombre del contenedor de claves que contiene el par de claves pública y privada. Si `pbKeyBlob` es null, `szKeyContainer` debe especificar un contenedor válido en el CSP. En este caso, el método [ICLRStrongName:: StrongNameGetPublicKey (](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-strongnamegetpublickey-method.md) extrae la clave pública del par de claves almacenado en el contenedor.  
  
 Si `pbKeyBlob` no es null, se supone que el par de claves está incluido en el objeto binario grande (BLOB) de clave.  
  
 Las claves deben ser claves de firma de Rivest-Shamir-Adleman (RSA) de 1024 bits. En este momento no se admite ningún otro tipo de clave.  
  
 `pbKeyBlob`  
 de Puntero al par de claves pública y privada. Este par está en el formato creado por la función `CryptExportKey` de Win32. Si `pbKeyBlob` es null, se supone que el contenedor de claves especificado por `szKeyContainer` contiene el par de claves.  
  
 `cbKeyBlob`  
 de Tamaño, en bytes, de `pbKeyBlob`.  
  
 `ppbPublicKeyBlob`  
 enuncia El BLOB de clave pública devuelto. El Common Language Runtime asigna el parámetro `ppbPublicKeyBlob` y se devuelve al autor de la llamada. El llamador debe liberar memoria mediante el método [ICLRStrongName:: StrongNameFreeBuffer](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-strongnamefreebuffer-method.md) .  
  
 `pcbPublicKeyBlob`  
 enuncia Tamaño del BLOB de clave pública devuelto.  
  
## <a name="return-value"></a>Valor devuelto  
 `S_OK` si el método se completó correctamente; de lo contrario, un valor HRESULT que indica un error (vea [Valores HRESULT comunes](https://go.microsoft.com/fwlink/?LinkId=213878) para una lista).  
  
## <a name="remarks"></a>Comentarios  
 La clave pública está contenida en una estructura [PublicKeyBlob](../../../../docs/framework/unmanaged-api/strong-naming/publickeyblob-structure.md) .  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Vea [Requisitos de sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado:** Metahost. h  
  
 **Biblioteca:** Se incluye como recurso en MSCorEE. dll  
  
 **Versiones de .NET Framework:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Vea también

- [StrongNameTokenFromPublicKey (método)](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-strongnametokenfrompublickey-method.md)
- [PublicKeyBlob (estructura)](../../../../docs/framework/unmanaged-api/strong-naming/publickeyblob-structure.md)
- [ICLRStrongName (interfaz)](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-interface.md)
