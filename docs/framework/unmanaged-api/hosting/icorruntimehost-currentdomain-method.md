---
title: ICorRuntimeHost::CurrentDomain (Método)
ms.date: 03/30/2017
api_name:
- ICorRuntimeHost.CurrentDomain
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICorRuntimeHost::CurrentDomain
helpviewer_keywords:
- ICorRuntimeHost::CreateDomain method [.NET Framework hosting]
- CurrentDomain method [.NET Framework hosting]
ms.assetid: dd2afb38-675b-4c3c-a9f3-8ab3b133eb02
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: d3aa6bc844d2c6629085b0596127c0b51b99357d
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/10/2019
ms.locfileid: "67766355"
---
# <a name="icorruntimehostcurrentdomain-method"></a>ICorRuntimeHost::CurrentDomain (Método)
Obtiene un puntero de interfaz de tipo <xref:System.AppDomain?displayProperty=nameWithType> que representa el dominio cargado en el subproceso actual.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
HRESULT CurrentDomain (  
    [out] IUnknown** pAppDomain  
);  
```  
  
## <a name="parameters"></a>Parámetros  
 `pAppDomain`  
 [out] Un puntero de tipo <xref:System.AppDomain?displayProperty=nameWithType> que representa el dominio de aplicación actual del subproceso. Este puntero es de tipo `IUnknown`, por lo que generalmente deberían llamar los llamadores `QueryInterface` para obtener un puntero de tipo <xref:System._AppDomain>.  
  
## <a name="return-value"></a>Valor devuelto  
  
|HRESULT|DESCRIPCIÓN|  
|-------------|-----------------|  
|S_OK|La operación fue correcta.|  
|S_FALSE|No se pudo completar la operación.|  
|E_FAIL|Se ha producido un error catastrófico desconocido. Si el método devuelve E_FAIL, common language runtime (CLR) ya no es utilizable en el proceso. Las llamadas subsiguientes a cualquier API de hospedaje devuelven HOST_E_CLRNOTAVAILABLE.|  
|HOST_E_CLRNOTAVAILABLE|El CLR no se ha cargado en un proceso o el CLR se encuentra en un estado en el que no se puede ejecutar código administrado o procesar la llamada correctamente.|  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Consulte [Requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado**: MSCorEE.h  
  
 **Biblioteca:** Incluye como recurso en MSCorEE.dll  
  
 **Versiones de .NET framework:** 1.0, 1.1  
  
## <a name="see-also"></a>Vea también

- <xref:System._AppDomain>
- <xref:System.AppDomain>
- [ICorRuntimeHost (interfaz)](../../../../docs/framework/unmanaged-api/hosting/icorruntimehost-interface.md)
