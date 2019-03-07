---
title: IMetaDataImport::GetMethodProps (Método)
ms.date: 03/30/2017
api_name:
- IMetaDataImport.GetMethodProps
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::GetMethodProps
helpviewer_keywords:
- GetMethodProps method [.NET Framework metadata]
- IMetaDataImport::GetMethodProps method [.NET Framework metadata]
ms.assetid: e0667ef7-1d31-4c89-a2d3-d426f023f8d2
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 57604d80d40130ca147c026852b7bcd23f8f90bc
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/06/2019
ms.locfileid: "57496461"
---
# <a name="imetadataimportgetmethodprops-method"></a>IMetaDataImport::GetMethodProps (Método)
Obtiene los metadatos asociados al método al que hace referencia el token de MethodDef especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
HRESULT GetMethodProps (  
    [in]  mdMethodDef         mb,  
    [out] mdTypeDef           *pClass,  
    [out] LPWSTR              szMethod,  
    [in]  ULONG               cchMethod,  
    [out] ULONG               *pchMethod,  
    [out] DWORD               *pdwAttr,  
    [out] PCCOR_SIGNATURE     *ppvSigBlob,  
    [out] ULONG               *pcbSigBlob,  
    [out] ULONG               *pulCodeRVA,  
    [out] DWORD               *pdwImplFlags  
);  
```  
  
## <a name="parameters"></a>Parámetros  
 `mb`  
 [in] El token de MethodDef que representa el método para devolver los metadatos.  
  
 `pClass`  
 [out] Un puntero a un token de TypeDef que representa el tipo que implementa el método.  
  
 `szMethod`  
 [out] Un puntero a un búfer que contiene el nombre del método.  
  
 `cchMethod`  
 [in] El tamaño solicitado del `szMethod`.  
  
 `pchMethod`  
 [out] Un puntero al tamaño en caracteres anchos de `szMethod`, o en el caso de truncamiento, el número real de caracteres anchos en el nombre del método.  
  
 `pdwAttr`  
 [out] Un puntero a cualquier indicador asociado al método.  
  
 `ppvSigBlob`  
 [out] Un puntero a la firma de metadatos binaria del método.  
  
 `pcbSigBlob`  
 [out] Un puntero al tamaño en bytes de `ppvSigBlob`.  
  
 `pulCodeRVA`  
 [out] Un puntero a la dirección virtual relativa del método.  
  
 `pdwImplFlags`  
 [out] Un puntero a los marcadores de implementación para el método.  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Consulte [Requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado**: Cor.h  
  
 **Biblioteca:** Incluye como recurso en MsCorEE.dll  
  
 **Versiones de .NET Framework:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Vea también
- [IMetaDataImport (interfaz)](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-interface.md)
- [IMetaDataImport2 (interfaz)](../../../../docs/framework/unmanaged-api/metadata/imetadataimport2-interface.md)
