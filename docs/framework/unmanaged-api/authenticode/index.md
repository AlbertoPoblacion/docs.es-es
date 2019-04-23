---
title: Authenticode (Referencia de la API no administrada)
ms.date: 03/30/2017
ms.assetid: 7e8cc303-6e77-4116-aa8b-7ea297a3a467
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 408219307015d5c39cb581b3884ed9810f4c0566
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59216358"
---
# <a name="authenticode-unmanaged-api-reference"></a>Authenticode (Referencia de la API no administrada)
Admite el módulo de creación y verificación de licencias Authenticode XrML.  
  
## <a name="in-this-section"></a>En esta sección  
 [_AxlGetIssuerPublicKeyHash (Función)](../../../../docs/framework/unmanaged-api/authenticode/axlgetissuerpublickeyhash-function.md)  
 Recupera el hash SHA-1 de la clave pública asociada con la clave privada que se usa para firmar el certificado especificado.  
  
 [_AxlPublicKeyBlobToPublicKeyToken (Función)](../../../../docs/framework/unmanaged-api/authenticode/axlpublickeyblobtopublickeytoken-function.md)  
 Calcula el token de clave pública del nombre seguro a partir de un formato CSP PUBLICKEYBLOB.  
  
 [_AxlRSAKeyValueToPublicKeyToken (Función)](../../../../docs/framework/unmanaged-api/authenticode/axlrsakeyvaluetopublickeytoken-function.md)  
 Convierte un blob Modulus y Exponent en un token de clave pública de nombre seguro.  
  
 [CertFreeAuthenticodeSignerInfo (Función)](../../../../docs/framework/unmanaged-api/authenticode/certfreeauthenticodesignerinfo-function.md)  
 Libera recursos asignados para la estructura AXL_AUTHENTICODE_SIGNER_INFO.  
  
 [CertFreeAuthenticodeTimestamperInfo (Función)](../../../../docs/framework/unmanaged-api/authenticode/certfreeauthenticodetimestamperinfo-function.md)  
 Libera recursos asignados para la estructura AXL_AUTHENTICODE_TIMESTAMPER_INFO.  
  
 [CertTimestampAuthenticodeLicense (Función)](../../../../docs/framework/unmanaged-api/authenticode/certtimestampauthenticodelicense-function.md)  
 Aplica marcas de hora a una licencia Authenticode XrML creada por CertCreateAuthenticodeLicense.  
  
 [CertVerifyAuthenticodeLicense (Función)](../../../../docs/framework/unmanaged-api/authenticode/certverifyauthenticodelicense-function.md)  
 Comprueba la validez de una licencia Authenticode XrML.  
  
 [AXL_AUTHENTICODE_SIGNER_INFO (estructura)](../../../../docs/framework/unmanaged-api/authenticode/axl-authenticode-signer-info-structure.md)  
 Define la información del firmante de Authenticode.  
  
 [AXL_AUTHENTICODE_TIMESTAMPER_INFO (estructura)](../../../../docs/framework/unmanaged-api/authenticode/axl-authenticode-timestamper-info-structure.md)  
 Define la información del autor de la marca de hora de Authenticode.  
  
## <a name="see-also"></a>Vea también

- [Referencia de API no administrada](../../../../docs/framework/unmanaged-api/index.md)
