---
title: ISymUnmanagedConstant::GetValue (Método)
ms.date: 03/30/2017
api_name:
- ISymUnmanagedConstant.GetValue
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedConstant::GetValue
helpviewer_keywords:
- GetValue method, ISymUnmanagedConstant interface [.NET Framework debugging]
- ISymUnmanagedConstant::GetValue method [.NET Framework debugging]
ms.assetid: 0036fc10-e768-47a8-b9cf-bf47faf8d194
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 75cc16f44ddf29b161c758718b697cc2aaba8e08
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2019
ms.locfileid: "59204671"
---
# <a name="isymunmanagedconstantgetvalue-method"></a>ISymUnmanagedConstant::GetValue (Método)
Obtiene el valor de la constante.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
HRESULT GetValue(  
    [out]  VARIANT* pValue  
);  
```  
  
## <a name="parameters"></a>Parámetros  
 `pValue`  
 [out] Un puntero a una variable que recibe el valor.  
  
## <a name="return-value"></a>Valor devuelto  
 S_OK si el método se realiza correctamente; en caso contrario, E_FAIL u otro código de error.  
  
## <a name="requirements"></a>Requisitos  
 **Encabezado**: CorSym.idl, CorSym.h  
  
## <a name="see-also"></a>Vea también

- [ISymUnmanagedConstant (Interfaz)](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedconstant-interface.md)
- [Método GetName](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedconstant-getname-method.md)
- [Método GetSignature](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedconstant-getsignature-method.md)
