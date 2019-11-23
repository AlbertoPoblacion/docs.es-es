---
title: ICeeGen::GetSectionBlock (Método)
ms.date: 03/30/2017
api_name:
- ICeeGen.GetSectionBlock
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICeeGen::GetSectionBlock
helpviewer_keywords:
- GetSectionBlock method [.NET Framework metadata]
- ICeeGen::GetSectionBlock method [.NET Framework metadata]
ms.assetid: 05c78aaf-5bbd-497e-9ae2-55f4fae0c5fb
topic_type:
- apiref
ms.openlocfilehash: 0731053fb37c775d25052a5fd99a479a44ff5862
ms.sourcegitcommit: 9a39f2a06f110c9c7ca54ba216900d038aa14ef3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/23/2019
ms.locfileid: "74434880"
---
# <a name="iceegengetsectionblock-method"></a>ICeeGen::GetSectionBlock (Método)
Gets a section block of the code base.  
  
 This method is obsolete and should not be used.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
HRESULT GetSectionBlock (  
    [in]  HCEESECTION    section,     
    [in]  ULONG          len,  
    [in]  ULONG          align     = 1,  
    [out] void           **ppBytes = 0  
);   
```  
  
## <a name="parameters"></a>Parámetros  
 `section`  
 [in] The section from which to retrieve a block of the code base.  
  
 `len`  
 [in] The length of the block to be retrieved.  
  
 `align`  
 [in] The byte, relative to the beginning of the section, with which to align the first byte of the block. This is the position of the block within the section.  
  
 `ppBytes`  
 [out] A pointer to a location that receives the address of the retrieved block.  
  
## <a name="remarks"></a>Comentarios  
 Call `GetSectionBlock` only if you have special section requirements that are not handled by other methods.  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Vea [Requisitos de sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Header:** Cor.h  
  
 **Library:** Used as a resource in MsCorEE.dll  
  
 **Versiones de .NET Framework:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Vea también

- [ICeeGen (interfaz)](../../../../docs/framework/unmanaged-api/metadata/iceegen-interface.md)
