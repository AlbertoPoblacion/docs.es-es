---
title: ECustomDumpFlavor (Enumeración)
ms.date: 03/30/2017
api_name:
- ECustomDumpFlavor
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ECustomDumpFlavor
helpviewer_keywords:
- ECustomDumpFlavor enumeration [.NET Framework hosting]
ms.assetid: b39b3320-fac7-41f1-9a03-ab6fb0cd89c7
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: d1e69d9cbf39049e82803d2f7bc795cc9fd0b368
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61796011"
---
# <a name="ecustomdumpflavor-enumeration"></a>ECustomDumpFlavor (Enumeración)
Contiene valores que indican qué elementos desea incluir en un subconjunto de un montón personalizado de volcado de memoria al informar de errores.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
typedef enum {  
    DUMP_FLAVOR_Mini            = 1,  
    DUMP_FLAVOR_NonHeapCLRState = 2  
} ECustomDumpFlavor;  
```  
  
## <a name="members"></a>Miembros  
  
|Miembro|Descripción|  
|------------|-----------------|  
|`DUMP_FLAVOR_Mini`|Especifica que el volcado del montón personalizado debe iniciarse como minivolcado e incluir datos adicionales que se especificó ninguno [CustomDumpItem](../../../../docs/framework/unmanaged-api/hosting/customdumpitem-structure.md) las instancias que se pasan al mismo método.|  
|`DUMP_FLAVOR_NonHeapCLRState`|Especifica que el volcado del montón personalizado debe recopilar todos los datos de estado de tiempo de ejecución que no se ha asignado dinámicamente.|  
  
## <a name="remarks"></a>Comentarios  
 Un parámetro de tipo `ECustomDumpFlavor` se pasa a la [ICLRErrorReportingManager:: BeginCustomDump](../../../../docs/framework/unmanaged-api/hosting/iclrerrorreportingmanager-begincustomdump-method.md) método.  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Consulte [Requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado**: MSCorEE.h  
  
 **Biblioteca:** MSCorEE.dll  
  
 **Versiones de .NET Framework:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Vea también

- [ECustomDumpItemKind (enumeración)](../../../../docs/framework/unmanaged-api/hosting/ecustomdumpitemkind-enumeration.md)
- [ICLRErrorReportingManager (interfaz)](../../../../docs/framework/unmanaged-api/hosting/iclrerrorreportingmanager-interface.md)
- [Enumeraciones para hosts](../../../../docs/framework/unmanaged-api/hosting/hosting-enumerations.md)
