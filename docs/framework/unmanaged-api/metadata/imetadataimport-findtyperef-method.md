---
title: IMetaDataImport::FindTypeRef (Método)
ms.date: 03/30/2017
api_name:
- IMetaDataImport.FindTypeRef
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::FindTypeRef
helpviewer_keywords:
- IMetaDataImport::FindTypeRef method [.NET Framework metadata]
- FindTypeRef method [.NET Framework metadata]
ms.assetid: 1b2bbf3f-943e-412e-b66c-e802431b055c
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: acc006894f05536ed76bac60b0fde9277a460813
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2019
ms.locfileid: "59199029"
---
# <a name="imetadataimportfindtyperef-method"></a>IMetaDataImport::FindTypeRef (Método)
Obtiene un puntero al TypeRef token para el <xref:System.Type> referencia que se encuentra en el ámbito especificado y que tiene el nombre especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
HRESULT FindTypeRef (  
   [in] mdToken        tkResolutionScope,  
   [in]  LPCWSTR       szName,  
   [out] mdTypeRef     *ptr  
);  
```  
  
## <a name="parameters"></a>Parámetros  
 `tkResolutionScope`  
 [in] Un token ModuleRef, AssemblyRef o TypeRef que especifica el módulo, ensamblado o tipo, respectivamente, en que el tipo de referencia se define.  
  
 `szName`  
 [in] El nombre de la referencia de tipo que se buscará.  
  
 `ptr`  
 [out] Un puntero al token TypeRef coincidente.  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Consulte [Requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado**: Cor.h  
  
 **Biblioteca:** Incluye como recurso en MsCorEE.dll  
  
 **Versiones de .NET Framework:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Vea también

- [IMetaDataImport (Interfaz)](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-interface.md)
- [IMetaDataImport2 (Interfaz)](../../../../docs/framework/unmanaged-api/metadata/imetadataimport2-interface.md)
