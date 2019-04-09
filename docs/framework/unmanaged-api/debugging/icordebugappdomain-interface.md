---
title: Interfaz ICorDebugAppDomain
ms.date: 03/30/2017
api_name:
- ICorDebugAppDomain
api_location:
- corguids.lib
api_type:
- COM
f1_keywords:
- ICorDebugAppDomain
helpviewer_keywords:
- ICorDebugAppDomain interface [.NET Framework debugging]
ms.assetid: be7ae711-1217-4a44-be40-166e29641b77
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 40619aa40f9924d94c82541eb8d30790e774a675
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2019
ms.locfileid: "59141510"
---
# <a name="icordebugappdomain-interface"></a>Interfaz ICorDebugAppDomain

Proporciona métodos para depurar dominios de aplicación. Esta interfaz es una subclase de ICorDebugController.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descripción|  
|------------|-----------------|  
|[Método Attach](../../../../docs/framework/unmanaged-api/debugging/icordebugappdomain-attach-method.md)|Asocia al depurador al dominio de aplicación.|  
|[Método EnumerateAssemblies](../../../../docs/framework/unmanaged-api/debugging/icordebugappdomain-enumerateassemblies-method.md)|Obtiene un enumerador para los ensamblados en el dominio de aplicación.|  
|[Método EnumerateBreakpoints](../../../../docs/framework/unmanaged-api/debugging/icordebugappdomain-enumeratebreakpoints-method.md)|Obtiene un enumerador para todos los puntos de interrupción activos en el dominio de aplicación.|  
|[Método EnumerateSteppers](../../../../docs/framework/unmanaged-api/debugging/icordebugappdomain-enumeratesteppers-method.md)|Obtiene un enumerador para todos los steppers activos en el dominio de aplicación.|  
|[Método GetId](../../../../docs/framework/unmanaged-api/debugging/icordebugappdomain-getid-method.md)|Obtiene el identificador único del dominio de aplicación.|  
|[Método GetModuleFromMetaDataInterface](../../../../docs/framework/unmanaged-api/debugging/icordebugappdomain-getmodulefrommetadatainterface-method.md)|Obtiene el objeto ICorDebugModule con la interfaz de metadatos especificado.|  
|[Método GetName](../../../../docs/framework/unmanaged-api/debugging/icordebugappdomain-getname-method.md)|Obtiene el nombre del dominio de aplicación.|  
|[GetObject (Método)](../../../../docs/framework/unmanaged-api/debugging/icordebugappdomain-getobject-method.md)|Obtiene un puntero de interfaz para el dominio de aplicación de common language runtime (CLR).|  
|[Método GetProcess](../../../../docs/framework/unmanaged-api/debugging/icordebugappdomain-getprocess-method.md)|Obtiene el proceso que contiene el dominio de aplicación.|  
|[Método IsAttached](../../../../docs/framework/unmanaged-api/debugging/icordebugappdomain-isattached-method.md)|Determina si el depurador está asociado al dominio de aplicación.|  
  
## <a name="remarks"></a>Comentarios  
  
> [!NOTE]
>  Esta interfaz no admite que se la llame de forma remota, ya sea entre procesos o entre equipos.  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Consulte [Requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado**: CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **Versiones de .NET Framework:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Vea también

- [Interfaces para depuración](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
