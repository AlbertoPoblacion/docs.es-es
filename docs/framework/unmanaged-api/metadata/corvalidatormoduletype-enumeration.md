---
title: CorValidatorModuleType (Enumeración)
ms.date: 03/30/2017
api_name:
- CorValidatorModuleType
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorValidatorModuleType
helpviewer_keywords:
- CorValidatorModuleType enumeration [.NET Framework metadata]
ms.assetid: 748f1ab2-fbcb-4f55-89ec-8d23d81ebc80
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 04bed418d96658e29328cf2ce6bba445639b437f
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/10/2019
ms.locfileid: "67750762"
---
# <a name="corvalidatormoduletype-enumeration"></a>CorValidatorModuleType (Enumeración)
Especifica el tipo de un módulo.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
typedef enum  
{  
    ValidatorModuleTypeInvalid  = 0x0,  
    ValidatorModuleTypeMin      = 0x00000001,  
    ValidatorModuleTypePE       = 0x00000001,  
    ValidatorModuleTypeObj      = 0x00000002,  
    ValidatorModuleTypeEnc      = 0x00000003,  
    ValidatorModuleTypeIncr     = 0x00000004,  
    ValidatorModuleTypeMax      = 0x00000004  
} CorValidatorModuleType;  
```  
  
## <a name="members"></a>Miembros  
  
|Member|DESCRIPCIÓN|  
|------------|-----------------|  
|`ValidatorModuleTypeInvalid`|El módulo es un tipo no válido.|  
|`ValidatorModuleTypeMin`|El valor mínimo de la `CorValidatorModuleType` enum.|  
|`ValidatorModuleTypePE`|El módulo es un archivo ejecutable portable (PE).|  
|`ValidatorModuleTypeObj`|El módulo es un archivo .obj.|  
|`ValidatorModuleTypeEnc`|El módulo es una sesión del depurador de editar y continuar.|  
|`ValidatorModuleTypeIncr`|El módulo es aquella que se ha compilado de forma incremental.|  
|`ValidatorModuleTypeMax`|El valor máximo de la `CorValidatorModuleType` enum.|  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Consulte [Requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado**: Cor.h  
  
 **Biblioteca:** Incluye como recurso en MsCorEE.dll  
  
 **Versiones de .NET Framework:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Vea también

- [Enumeraciones para metadatos](../../../../docs/framework/unmanaged-api/metadata/metadata-enumerations.md)
