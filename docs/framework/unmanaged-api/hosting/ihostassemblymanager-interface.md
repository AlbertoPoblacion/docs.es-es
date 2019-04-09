---
title: IHostAssemblyManager (Interfaz)
ms.date: 03/30/2017
api_name:
- IHostAssemblyManager
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostAssemblyManager
helpviewer_keywords:
- IHostAssemblyManager interface [.NET Framework hosting]
ms.assetid: dfec05bb-3cd7-4bd5-b396-a4f097c3a636
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 2e300d4645939a131ceb8206999d95056b96a678
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2019
ms.locfileid: "59118955"
---
# <a name="ihostassemblymanager-interface"></a>IHostAssemblyManager (Interfaz)
Proporciona métodos que permiten a un host especificar conjuntos de ensamblados que se deben cargar common language runtime (CLR) o el host.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descripción|  
|------------|-----------------|  
|[Método GetAssemblyStore](../../../../docs/framework/unmanaged-api/hosting/ihostassemblymanager-getassemblystore-method.md)|Obtiene un puntero de interfaz a un [IHostAssemblyStore](../../../../docs/framework/unmanaged-api/hosting/ihostassemblystore-interface.md) que representa la lista de ensamblados cargados por el host.|  
|[Método GetNonHostStoreAssemblies](../../../../docs/framework/unmanaged-api/hosting/ihostassemblymanager-getnonhoststoreassemblies-method.md)|Obtiene un puntero de interfaz a un [ICLRAssemblyReferenceList](../../../../docs/framework/unmanaged-api/hosting/iclrassemblyreferencelist-interface.md) que representa la lista de ensamblados que el host espera que CLR cargue.|  
  
## <a name="remarks"></a>Comentarios  
 El host no es necesario implementar `IHostAssemblyManager` o `IHostAssemblyStore`. Si el host implementa `IHostAssemblyManager`, también debe implementar `IHostAssemblyStore`.  
  
 El tiempo de ejecución de consultas para un `IHostAssemblyManager` mediante una llamada a [IHostControl](../../../../docs/framework/unmanaged-api/hosting/ihostcontrol-gethostmanager-method.md) tras la inicialización con una `IID` de IID_IHostAssemblyManager.  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Consulte [Requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado**: MSCorEE.h  
  
 **Biblioteca:** Incluye como recurso en MSCorEE.dll  
  
 **Versiones de .NET Framework:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Vea también

- [ICLRAssemblyReferenceList (Interfaz)](../../../../docs/framework/unmanaged-api/hosting/iclrassemblyreferencelist-interface.md)
- [IHostAssemblyStore (Interfaz)](../../../../docs/framework/unmanaged-api/hosting/ihostassemblystore-interface.md)
- [IHostControl (Interfaz)](../../../../docs/framework/unmanaged-api/hosting/ihostcontrol-interface.md)
- [Interfaces de hospedaje](../../../../docs/framework/unmanaged-api/hosting/hosting-interfaces.md)
