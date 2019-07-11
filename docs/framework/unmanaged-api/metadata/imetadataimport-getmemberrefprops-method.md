---
title: IMetaDataImport::GetMemberRefProps (Método)
ms.date: 03/30/2017
api_name:
- IMetaDataImport.GetMemberRefProps
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::GetMemberRefProps
helpviewer_keywords:
- GetMemberRefProps method [.NET Framework metadata]
- IMetaDataImport::GetMemberRefProps method [.NET Framework metadata]
ms.assetid: 0ea73055-ece0-4151-a094-414c88ef8941
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: fadc54d74ce6027bd021e148a14cb0c432eb41fe
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/10/2019
ms.locfileid: "67782344"
---
# <a name="imetadataimportgetmemberrefprops-method"></a>IMetaDataImport::GetMemberRefProps (Método)
Obtiene los metadatos asociados al miembro al que hace referencia el token especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
HRESULT GetMemberRefProps (  
   [in]  mdMemberRef       mr,   
   [out] mdToken           *ptk,   
   [out] LPWSTR            szMember,   
   [in]  ULONG             cchMember,   
   [out] ULONG             *pchMember,   
   [out] PCCOR_SIGNATURE   *ppvSigBlob,   
   [out] ULONG             *pbSig   
);  
```  
  
## <a name="parameters"></a>Parámetros  
 `mr`  
 [in] El token MemberRef para devolver los metadatos asociados.  
  
 `ptk`  
 [out] Un token de TypeDef o TypeRef o TypeSpec que representa la clase que declara el miembro o un token ModuleRef que representa la clase de módulo que declara el miembro o MethodDef que representa al miembro.  
  
 `szMember`  
 [out] Un búfer de cadena para el nombre del miembro.  
  
 `cchMember`  
 [in] El tamaño solicitado en caracteres anchos de `szMember`.  
  
 `pchMember`  
 [out] El tamaño devuelto en caracteres anchos de `szMember`.  
  
 `ppvSibBlob`  
 [out] Un puntero a la firma de metadatos binaria para el miembro.  
  
 `pbSig`  
 [out] El tamaño en bytes de `ppvSigBlob`.  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Consulte [Requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado**: Cor.h  
  
 **Biblioteca:** Incluye como recurso en MsCorEE.dll  
  
 **Versiones de .NET Framework:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Vea también

- [IMetaDataImport (interfaz)](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-interface.md)
- [IMetaDataImport2 (interfaz)](../../../../docs/framework/unmanaged-api/metadata/imetadataimport2-interface.md)
