---
title: CertTimestampAuthenticodeLicense (Función)
ms.date: 03/30/2017
api_name:
- CertTimestampAuthenticodeLicense
api_location:
- clr.dll
api_type:
- DLLExport
ms.assetid: d468325a-21c5-43ce-8567-84e342b22308
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: c7b336d1372bdbe0d6dbdcf79d94e14c30ad2ebe
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/06/2019
ms.locfileid: "57497345"
---
# <a name="certtimestampauthenticodelicense-function"></a>CertTimestampAuthenticodeLicense (Función)
Aplica marcas de hora a una licencia Authenticode XrML.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
HRESULT CertTimestampAuthenticodeLicense (  
    [in]  PCRYPT_DATA_BLOB   pSignedLicenseBlob,  
    [in]  LPCWSTR            pwszTimestampURI,  
    [out] PCRYPT_DATA_BLOB   pTimestampSignatureBlob  
);  
```  
  
## <a name="parameters"></a>Parámetros  
 `pSignedLicenseBlob`  
 [in] Licencia Authenticode XrML firmada a la que se va a aplicar la marca de hora. Consulte la [CRYPTOAPI_BLOB](/windows/desktop/api/dpapi/ns-dpapi-_cryptoapi_blob) estructura.  
  
 `pwszTimestampURI`  
 [in] URI del servidor de marca de hora.  
  
 `pTimestampSignatureBlob`  
 [out] Puntero a CRYPT_DATA_BLOB para recibir la firma de marca de hora con codificación base64. Es responsabilidad del llamante liberar `pTimestampSignatureBlob` -> `pbData` con `HepFree()` tras su uso. Consulte la [CRYPTOAPI_BLOB](/windows/desktop/api/dpapi/ns-dpapi-_cryptoapi_blob) estructura.  
  
## <a name="remarks"></a>Comentarios  
 La firma de marca de hora es en realidad un mensaje PKCS #7 SignedData cuyo contenido es el formato binario del SignatureValue de la firma de la licencia. Básicamente, actúa como contrafirma de la licencia.  
  
## <a name="return-value"></a>Valor devuelto  
 `S_OK` si la función se realiza correctamente. De lo contrario, devuelve un código de error.  
  
## <a name="see-also"></a>Vea también
- [Authenticode](../../../../docs/framework/unmanaged-api/authenticode/index.md)
