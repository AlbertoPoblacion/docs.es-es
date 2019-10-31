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
ms.openlocfilehash: 1759ee2ecf08322b745a4f80a62b24596c4504cb
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/30/2019
ms.locfileid: "73123248"
---
# <a name="loadlibraryshim-function"></a>LoadLibraryShim (Función)
Carga una versión especificada de una DLL incluida en el paquete redistribuible de .NET Framework.  
  
 Esta función está en desuso en el .NET Framework 4. Use en su lugar el método [ICLRRuntimeInfo:: LoadLibrary](../../../../docs/framework/unmanaged-api/hosting/iclrruntimeinfo-loadlibrary-method.md) .  
  
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
 de Cadena terminada en cero que representa el nombre del archivo DLL que se va a cargar desde la biblioteca de .NET Framework.  
  
 `szVersion`  
 de Cadena terminada en cero que representa la versión de la DLL que se va a cargar. Si `szVersion` es null, la versión seleccionada para cargar es la versión más reciente del archivo DLL especificado que es anterior a la versión 4. Es decir, todas las versiones iguales o posteriores a la versión 4 se omiten si `szVersion` es null, y si no se instala ninguna versión anterior a la versión 4, la DLL no se carga. Esto se hace para asegurarse de que la instalación de .NET Framework 4 no afecte a las aplicaciones o componentes preexistentes. Vea la entrada [en proceso SxS y inicio rápido de migración](https://go.microsoft.com/fwlink/?LinkId=200329) en el blog del equipo de CLR.  
  
 `pvReserved`  
 Reservado para un uso futuro.  
  
 `phModDll`  
 enuncia Puntero al identificador del módulo.  
  
## <a name="return-value"></a>Valor devuelto  
 Este método devuelve los códigos de error del modelo de objetos componentes (COM) estándar, tal y como se define en WinError. h, además de los valores siguientes.  
  
|Código devuelto|Descripción|  
|-----------------|-----------------|  
|S_OK|El método se completó correctamente.|  
|CLR_E_SHIM_RUNTIMELOAD|La carga de `szDllName` requiere cargar el Common Language Runtime (CLR) y no se puede cargar la versión necesaria de CLR.|  
  
## <a name="remarks"></a>Comentarios  
 Esta función se usa para cargar los archivos DLL que se incluyen en el paquete redistribuible de .NET Framework. No carga los archivos dll generados por el usuario.  
  
> [!NOTE]
> A partir de la versión .NET Framework 2,0, la carga de Fusion. dll hace que se cargue el CLR. Esto se debe a que las funciones de Fusion. dll son ahora contenedores cuyas implementaciones son proporcionadas por el tiempo de ejecución.  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Vea [Requisitos de sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado:** MSCorEE. h  
  
 **Versiones de .NET Framework:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Vea también

- [Funciones de hospedaje de CLR en desuso](../../../../docs/framework/unmanaged-api/hosting/deprecated-clr-hosting-functions.md)
