---
title: CreateApplicationContext (Función)
ms.date: 03/30/2017
api_name:
- CreateApplicationContext
api_location:
- fusion.dll
api_type:
- DLLExport
f1_keywords:
- CreateApplicationContext
helpviewer_keywords:
- CreateApplicationContext function [.NET Framework fusion]
ms.assetid: 7bf8a141-b2c0-4058-9885-1cef7dcaa811
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: d98829b29100824e5d606e23aaf287c9f6e81d69
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2019
ms.locfileid: "59170968"
---
# <a name="createapplicationcontext-function"></a>CreateApplicationContext (Función)
Esta función admite la infraestructura de .NET Framework y no está pensada para utilizarse directamente desde el código.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
HRESULT CreateApplicationContext (  
    [in]  IAssemblyName  *pName,  
    [out] LPPAPPLICATIONCONTEXT  *ppCtx  
 );  
```  
  
## <a name="parameters"></a>Parámetros  
 `pName`  
 [in] Un puntero a un nombre descriptivo.  
  
 `ppCtx`  
 [out] Un puntero a un contexto de la aplicación.  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Consulte [Requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado**: Fusion.h  
  
 **Biblioteca:** Incluye como recurso en el archivo Fusion.dll  
  
 **Versiones de .NET Framework:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Vea también

- [IAssemblyCache (Interfaz)](../../../../docs/framework/unmanaged-api/fusion/iassemblycache-interface.md)
- [Funciones estáticas globales de la fusión](../../../../docs/framework/unmanaged-api/fusion/fusion-global-static-functions.md)
- [Caché global de ensamblados](../../../../docs/framework/app-domains/gac.md)
