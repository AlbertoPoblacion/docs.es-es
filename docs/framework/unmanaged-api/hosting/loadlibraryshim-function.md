---
title: LoadLibraryShim (Función)
ms.date: 03/30/2017
api_name:
- LoadLibraryShim
api_location:
- mscoree.dll
- mscoreei.dll
api_type:
- DLLExport
f1_keywords:
- LoadLibraryShim
helpviewer_keywords:
- LoadLibraryShim function [.NET Framework hosting]
ms.assetid: 30931874-4d0e-4df1-b3d1-e425b50655d1
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 03bc5584d24efa790989f93426251f9f38e65904
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/10/2019
ms.locfileid: "67768523"
---
# <a name="loadlibraryshim-function"></a>LoadLibraryShim (Función)
Carga la versión especificada de un archivo DLL que se incluye en el paquete redistribuible de .NET Framework.  
  
 Esta función está desusada en .NET Framework 4. Use la [ICLRRuntimeInfo](../../../../docs/framework/unmanaged-api/hosting/iclrruntimeinfo-loadlibrary-method.md) método en su lugar.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
HRESULT LoadLibraryShim (  
    [in]  LPCWSTR  szDllName,  
    [in]  LPCWSTR  szVersion,  
          LPVOID   pvReserved,  
    [out] HMODULE *phModDll  
);  
```  
  
## <a name="parameters"></a>Parámetros  
 `szDllName`  
 [in] Una cadena terminada en cero que representa el nombre del archivo DLL que se cargue desde la biblioteca de .NET Framework.  
  
 `szVersion`  
 [in] Una cadena terminada en cero que representa la versión de la DLL que se va a cargar. Si `szVersion` es null, la versión seleccionada para la carga es la versión más reciente del archivo DLL especificada que es menor que la versión 4. Es decir, todas las versiones iguales o mayores que la versión 4 se omiten si `szVersion` es null, y si no está instalada ninguna versión inferior a la versión 4, no puede cargar el archivo DLL. Esto es para asegurarse de que la instalación de .NET Framework 4 no afecta a las aplicaciones ya existentes o componentes. Vea la entrada [In-Proc SxS y migración de inicio rápido](https://go.microsoft.com/fwlink/?LinkId=200329) en el blog del equipo CLR.  
  
 `pvReserved`  
 Reservado para un uso futuro.  
  
 `phModDll`  
 [out] Un puntero al identificador del módulo.  
  
## <a name="return-value"></a>Valor devuelto  
 Este método devuelve códigos de error de modelo de objetos componentes (COM) estándar, tal como se define en WinError.h, además de los valores siguientes.  
  
|Código devuelto|DESCRIPCIÓN|  
|-----------------|-----------------|  
|S_OK|El método se completó correctamente.|  
|CLR_E_SHIM_RUNTIMELOAD|Cargando `szDllName` requiere la carga no se puede cargar common language runtime (CLR) y la versión necesaria de CLR.|  
  
## <a name="remarks"></a>Comentarios  
 Esta función se usa para cargar los archivos DLL que se incluyen en el paquete redistribuible de .NET Framework. No carga las DLL generadas por el usuario.  
  
> [!NOTE]
>  A partir de la versión 2.0 de .NET Framework, carga el archivo Fusion.dll hace que el CLR que se va a cargar. Esto es porque las funciones en el archivo Fusion.dll ahora son contenedores cuyas implementaciones son proporcionados por el tiempo de ejecución.  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Consulte [Requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado**: MSCorEE.h  
  
 **Versiones de .NET Framework:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Vea también

- [Funciones de hospedaje de CLR en desuso](../../../../docs/framework/unmanaged-api/hosting/deprecated-clr-hosting-functions.md)
