---
title: CertVerifyAuthenticodeLicense (Función)
ms.date: 03/30/2017
api_name:
- CertVerifyAuthenticodeLicense
api_location:
- clr.dll
api_type:
- DLLExport
ms.assetid: 00118de7-33c6-41c4-8e1f-5d5e35e0da83
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: a644e3e2df2544e8164cdaf3bbef3c44d3cd567f
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/06/2019
ms.locfileid: "57502558"
---
# <a name="certverifyauthenticodelicense-function"></a>CertVerifyAuthenticodeLicense (Función)
Comprueba la validez de una licencia Authenticode XrML.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
HRESULT CertVerifyAuthenticodeLicense (  
    [in]   PCRYPT_DATA_BLOB                   pLicenseBlob,  
    [in]   OPTIONAL DWORD                     dwFlags,  
    [out]  PAXL_AUTHENTICODE_SIGNER_INFO      pSignerInfo,  
    [out]  PAXL_AUTHENTICODE_TIMESTAMPER_INFO pTimestamperInfo  
);  
```  
  
## <a name="parameters"></a>Parámetros  
 `pLicenseBlob`  
 [in] Licencia Authenticode XrML que se va a comprobar.  
  
 Consulte la [CRYPTOAPI_BLOB](/windows/desktop/api/dpapi/ns-dpapi-_cryptoapi_blob) estructura.  
  
 `dwFlags`  
 [in] Opcional. Una combinación de los siguientes valores:  
  
-   AXL_REVOCATION_NO_CHECK  
  
-   AXL_REVOCATION_CHECK_END_CERT_ONLY  
  
-   AXL_REVOCATION_CHECK_ENTIRE_CHAIN  
  
-   AXL_URL_CACHE_ONLY_RETRIEVAL  
  
-   AXL_LIFETIME_SIGNING  
  
-   AXL_TRUST_MICROSOFT_ROOT_ONLY  
  
 `pSignerInfo`  
 [out] Para recibir la información del firmante. Si la licencia no estaba firmada, `dwError` se establece en TRUST_E_NOSIGNATURE. Es responsabilidad del llamante liberar recursos usando el [CertFreeAuthenticodeSignerInfo](../../../../docs/framework/unmanaged-api/authenticode/certfreeauthenticodesignerinfo-function.md) función tras su uso.  
  
 Consulte [AXL_AUTHENTICODE_SIGNER_INFO (estructura)](../../../../docs/framework/unmanaged-api/authenticode/axl-authenticode-signer-info-structure.md).  
  
 `pTimestamperInfo`  
 [out] Para recibir la información del autor de la marca de hora, si está disponible. Si la licencia no tenía marca de hora, `dwError` se establece en TRUST_E_NOSIGNATURE. Es responsabilidad del llamante liberar recursos usando el [CertFreeAuthenticodeTimestamperInfo](../../../../docs/framework/unmanaged-api/authenticode/certfreeauthenticodetimestamperinfo-function.md) función tras su uso.  
  
 Consulte [AXL_AUTHENTICODE_TIMESTAMPER_INFO (estructura)](../../../../docs/framework/unmanaged-api/authenticode/axl-authenticode-timestamper-info-structure.md).  
  
## <a name="return-value"></a>Valor devuelto  
 Si la operación se realiza correctamente, devuelve `S_OK`. De lo contrario, devuelve un código de error.  
  
## <a name="see-also"></a>Vea también
- [Authenticode](../../../../docs/framework/unmanaged-api/authenticode/index.md)
- [GetHashFromHandle (método)](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-gethashfromhandle-method.md)
- [ICLRStrongName (interfaz)](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-interface.md)
