---
title: ICeeGen::GetIlSection (Método)
ms.date: 03/30/2017
api_name:
- ICeeGen.GetIlSection
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICeeGen::GetIlSection
helpviewer_keywords:
- GetIlSection method [.NET Framework metadata]
- ICeeGen::GetIlSection method [.NET Framework metadata]
ms.assetid: 6f2db2ca-203f-4ac3-9530-208642ca385e
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 0e9d71edc580591b698ad039f8ee73e49c4e1d6a
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/06/2019
ms.locfileid: "57489051"
---
# <a name="iceegengetilsection-method"></a>ICeeGen::GetIlSection (Método)
Obtiene la sección de la base de código de lenguaje intermedio al que hace referencia el identificador especificado.  
  
 Este método está obsoleto y no debe usarse.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
HRESULT GetIlSection (  
    [in] HCEESECTION  *section  
);  
```  
  
## <a name="parameters"></a>Parámetros  
 `section`  
 [in] El identificador de la sección para obtener.  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Consulte [Requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado**: Cor.h  
  
 **Biblioteca:** Usar como un recurso en MsCorEE.dll  
  
 **Versiones de .NET Framework:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Vea también
- [ICeeGen (interfaz)](../../../../docs/framework/unmanaged-api/metadata/iceegen-interface.md)
