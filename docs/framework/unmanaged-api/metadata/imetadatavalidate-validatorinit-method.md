---
title: IMetaDataValidate::ValidatorInit (Método)
ms.date: 03/30/2017
api_name:
- IMetaDataValidate.ValidatorInit
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataValidate::ValidatorInit
helpviewer_keywords:
- IMetaDataValidate::ValidatorInit method [.NET Framework metadata]
- ValidatorInit method [.NET Framework metadata]
ms.assetid: 6bafd75a-e2d0-4aea-aed1-074374d5dff6
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: d2018be28cbfe72bb7c989634374b8ab43693e6f
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/06/2019
ms.locfileid: "57491963"
---
# <a name="imetadatavalidatevalidatorinit-method"></a>IMetaDataValidate::ValidatorInit (Método)
Establece una marca que especifica el tipo del módulo en el ámbito de metadatos actual y registra el método de devolución de llamada especificado para los errores de validación.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
HRESULT ValidatorInit (  
   [in] DWORD       dwModuleType,  
   [in] IUnknown    *pUnk  
);  
```  
  
## <a name="parameters"></a>Parámetros  
 `dwModule`  
 [in] Un valor de la [CorValidatorModuleType](../../../../docs/framework/unmanaged-api/metadata/corvalidatormoduletype-enumeration.md) enumeración que especifica el tipo del módulo en el ámbito de metadatos actual.  
  
 `pUnk`  
 [in] Un puntero a un [IUnknown](/cpp/atl/iunknown) instancia que actúa como una devolución de llamada de función para errores de validación.  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Consulte [Requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado**: Cor.h  
  
 **Biblioteca:** Usar como un recurso en MsCorEE.dll  
  
 **Versiones de .NET Framework:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Vea también
- [IMetaDataValidate (interfaz)](../../../../docs/framework/unmanaged-api/metadata/imetadatavalidate-interface.md)
