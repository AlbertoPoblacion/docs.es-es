---
title: CorCheckDuplicatesFor (Enumeración)
ms.date: 03/30/2017
api_name:
- CorCheckDuplicatesFor
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorCheckDuplicatesFor
helpviewer_keywords:
- CorCheckDuplicatesFor enumeration [.NET Framework metadata]
ms.assetid: d8ec8d3c-70f7-4cc6-9957-68068fd8f49c
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: a82ce9709e008e092c5f31372a89bf9a16e1f88b
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/10/2019
ms.locfileid: "67767015"
---
# <a name="corcheckduplicatesfor-enumeration"></a>CorCheckDuplicatesFor (Enumeración)
Especifica los tokens de metadatos que se comprobará si existen duplicados.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
typedef enum CorCheckDuplicatesFor {  
  
    MDDupAll                    = 0xffffffff,  
    MDDupENC                    = MDDupAll,  
    MDNoDupChecks               = 0x00000000,  
    MDDupTypeDef                = 0x00000001,  
    MDDupInterfaceImpl          = 0x00000002,  
    MDDupMethodDef              = 0x00000004,  
    MDDupTypeRef                = 0x00000008,  
    MDDupMemberRef              = 0x00000010,  
    MDDupCustomAttribute        = 0x00000020,  
    MDDupParamDef               = 0x00000040,  
    MDDupPermission             = 0x00000080,  
    MDDupProperty               = 0x00000100,  
    MDDupEvent                  = 0x00000200,  
    MDDupFieldDef               = 0x00000400,  
    MDDupSignature              = 0x00000800,  
    MDDupModuleRef              = 0x00001000,  
    MDDupTypeSpec               = 0x00002000,  
    MDDupImplMap                = 0x00004000,  
    MDDupAssemblyRef            = 0x00008000,  
    MDDupFile                   = 0x00010000,  
    MDDupExportedType           = 0x00020000,  
    MDDupManifestResource       = 0x00040000,  
    MDDupGenericParam           = 0x00080000,  
    MDDupMethodSpec             = 0x00100000,  
    MDDupGenericParamConstraint = 0x00200000,  
  
    MDDupAssembly               = 0x10000000,  
  
    MDDupDefault =   
        MDNoDupChecks | MDDupTypeRef | MDDupMemberRef |   
        MDDupSignature | MDDupTypeSpec | MDDupMethodSpec  
  
} CorCheckDuplicatesFor;  
```  
  
## <a name="members"></a>Miembros  
  
|Member|DESCRIPCIÓN|  
|------------|-----------------|  
|`MDDupAll`|Compruebe todos los tokens de metadatos para los duplicados.|  
|`MDDupENC`|No se utiliza.|  
|`MDNoDupChecks`|No comprobar los tokens de metadatos para los duplicados.|  
|`MDDupTypeDef`|Comprobar duplicados de `mdTypeDef` tokens.|  
|`MDDupInterfaceImpl`|Comprobar duplicados de `mdInterfaceImpl` tokens.|  
|`MDDupMethodDef`|Comprobar duplicados de `mdMethodDef` tokens.|  
|`MDDupTypeRef`|Comprobar duplicados de `mdTypeRef` tokens.|  
|`MDDupMemberRef`|Comprobar duplicados de `mdMemberRef` tokens.|  
|`MDDupCustomAttribute`|Comprobar duplicados de `mdCustomAttribute` tokens.|  
|`MDDupParamDef`|Comprobar duplicados de `mdParamDef` tokens.|  
|`MDDupPermission`|Comprobar duplicados de `mdPermission` tokens.|  
|`MDDupProperty`|Comprobar duplicados de `mdProperty` tokens.|  
|`MDDupEvent`|Comprobar duplicados de `mdEvent` tokens.|  
|`MDDupFieldDef`|Comprobar duplicados de `mdFieldDef` tokens.|  
|`MDDupSignature`|Comprobar duplicados de `mdSignature` tokens.|  
|`MDDupModuleRef`|Comprobar duplicados de `mdModuleRef` tokens.|  
|`MDDupTypeSpec`|Comprobar duplicados de `mdTypeSpec` tokens.|  
|`MDDupImplMap`|Comprobar duplicados de `mdImplMap` tokens.|  
|`MDDupAssemblyRef`|Comprobar duplicados de `mdAssemblyRef` tokens.|  
|`MDDupFile`|Comprobar duplicados de `mdFile` tokens.|  
|`MDDupExportedType`|Comprobar duplicados de `mdExportedType` tokens.|  
|`MDDupManifestResource`|Comprobar duplicados de `mdManifestResource` tokens.|  
|`MDDupGenericParam`|Comprobar duplicados de `mdGenericParam` tokens.|  
|`MDDupMethodSpec`|Comprobar duplicados de `mdMethodSpec` tokens.|  
|`MDDupGenericParamConstraint`|Comprobar duplicados de `mdGenericParamConstraint` tokens.|  
|`MDDupAssembly`|Comprobar duplicados de `mdAssembly` tokens.|  
|`MDDupDefault`|Comprobar duplicados de `mdMemberRef`, `mdTypeRef`, `mdSignature`, `mdTypeSpec`, y `mdMethodSpec` tokens.|  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Consulte [Requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado**: CorHdr.h  
  
 **Versiones de .NET Framework:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Vea también

- [Enumeraciones para metadatos](../../../../docs/framework/unmanaged-api/metadata/metadata-enumerations.md)
