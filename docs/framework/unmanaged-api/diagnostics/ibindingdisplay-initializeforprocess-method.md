---
title: IBindingDisplay::InitializeForProcess (Método)
ms.date: 03/30/2017
api_name:
- IBindingDisplay.InitializeForProcess
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- IBindingDisplay::InitializeForProcess
helpviewer_keywords:
- IBindingDisplay::InitializeForProcess method [.NET Framework debugging]
- InitializeForProcess method [.NET Framework debugging]
ms.assetid: 59417acb-4e59-46ad-acfe-d827e6ab6078
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: aa1e85751f90c34d40e88207af5c7eed2dd1bb82
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59197885"
---
# <a name="ibindingdisplayinitializeforprocess-method"></a>IBindingDisplay::InitializeForProcess (Método)
Inicializa el [IBindingDisplay](../../../../docs/framework/unmanaged-api/diagnostics/ibindingdisplay-interface.md) objeto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
HRESULT InitializeForProcess (  
    [in] ULONG32   pid  
);  
```  
  
## <a name="parameters"></a>Parámetros  
 `pid`  
 [in] El identificador de proceso.  
  
## <a name="remarks"></a>Comentarios  
 El depurador llama el `InitializeForProcess` método en tiempo de creación para inicializar la presentación de enlace. `InitializeForProcess` se debe llamar en tiempo de creación antes de cualquier otro método en `IBindingDisplay` se llama.  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Consulte [Requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado**: BindingDisplay.h  
  
 **Biblioteca:** BindingDisplay.idl  
  
 **Versiones de .NET Framework:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Vea también

- [IBindingDisplay (interfaz)](../../../../docs/framework/unmanaged-api/diagnostics/ibindingdisplay-interface.md)
