---
title: ClrCreateManagedInstance (Función)
ms.date: 03/30/2017
api_name:
- ClrCreateManagedInstance
api_location:
- mscoree.dll
- clr.dll
- mscorwks.dll
- mscoreei.dll
- mscorsvr.dll
api_type:
- DLLExport
f1_keywords:
- ClrCreateManagedInstance
helpviewer_keywords:
- ClrCreateManagedInstance function [.NET Framework hosting]
ms.assetid: 58ba42c0-4857-43bf-a039-73a4dc6544c2
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: e1ae530b8488dcd375e91058a227316dd38cf4ab
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/10/2019
ms.locfileid: "67779157"
---
# <a name="clrcreatemanagedinstance-function"></a>ClrCreateManagedInstance (Función)
Crea una instancia del tipo administrado especificado.  
  
 Esta función está desusada en .NET Framework 4. Utilizar la activación de COM para crear una instancia del tipo administrado o utilizar el host (consulte [CLR hospedaje Interfaces agregadas en .NET Framework 4 y 4.5](../../../../docs/framework/unmanaged-api/hosting/clr-hosting-interfaces-added-in-the-net-framework-4-and-4-5.md)).  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
STDAPI ClrCreateManagedInstance (  
    [in]  LPCWSTR  pTypeName,   
    [in]  REFIID   riid,   
    [out] void     **ppObject  
);  
```  
  
## <a name="parameters"></a>Parámetros  
 `pTypeName`  
 [in] Un puntero al nombre del tipo de instancia que se solicita.  
  
 `riid`  
 [in] El `IID` del tipo de instancia que se solicita.  
  
 `ppObject`  
 [out] Un puntero a un puntero a una instancia del tipo administrado que se solicitó el llamador.  
  
## <a name="remarks"></a>Comentarios  
 Ya se debe cargar common language runtime en un proceso. Por ejemplo, se puede cargar mediante el uso de una llamada a la [CorBindToRuntimeEx](../../../../docs/framework/unmanaged-api/hosting/corbindtoruntimeex-function.md) funcionen antes de la `ClrCreateManagedInstance` se llama a la función. Si no se carga el tiempo de ejecución, `ClrCreateManagedInstance` en primer lugar intenta cargar v1.0.3705 del tiempo de ejecución. Si se produce un error, intenta cargar la versión más reciente del tiempo de ejecución.  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Consulte [Requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado**: MSCorEE.h  
  
 **Biblioteca:** MSCorEE.dll  
  
 **Versiones de .NET Framework:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Vea también

- [Funciones de hospedaje de CLR en desuso](../../../../docs/framework/unmanaged-api/hosting/deprecated-clr-hosting-functions.md)
- [Hospedar aplicaciones de WPF](../../../../docs/framework/unmanaged-api/hosting/index.md)
