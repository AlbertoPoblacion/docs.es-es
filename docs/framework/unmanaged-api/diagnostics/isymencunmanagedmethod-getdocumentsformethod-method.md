---
title: ISymENCUnmanagedMethod::GetDocumentsForMethod (Método)
ms.date: 03/30/2017
api_name:
- ISymENCUnmanagedMethod.GetDocumentsForMethod
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymENCUnmanagedMethod::GetDocumentsForMethod
helpviewer_keywords:
- GetDocumentsForMethod method [.NET Framework debugging]
- ISymENCUnmanagedMethod::GetDocumentsForMethod method [.NET Framework debugging]
ms.assetid: bd6ccde5-d578-48d8-abed-b474fbd48d13
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 42c677ae5aeb1e1b70ab68be8920fc71215cfe63
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/06/2019
ms.locfileid: "57472006"
---
# <a name="isymencunmanagedmethodgetdocumentsformethod-method"></a>ISymENCUnmanagedMethod::GetDocumentsForMethod (Método)
Obtiene los documentos que este método tiene líneas.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
HRESULT GetDocumentsForMethod(  
    [in]  ULONG32  cDocs,  
    [out] ULONG32  *pcDocs,   
    [in, size_is(cDocs)] ISymUnmanagedDocument* documents[]);  
```  
  
## <a name="parameters"></a>Parámetros  
 `cDocs`  
 [in] La longitud del búfer que apunta `pcDocs`.  
  
 `pcDocs`  
 [out] Un puntero a un `ULONG32` que recibe el tamaño, en caracteres, del búfer necesario para contener los documentos.  
  
 `documents`  
 [in] Búfer que contiene los documentos.  
  
## <a name="return-value"></a>Valor devuelto  
 S_OK si el método se realiza correctamente; en caso contrario, un código de error.  
  
## <a name="requirements"></a>Requisitos  
 **Encabezado**: CorSym.idl, CorSym.h  
  
## <a name="see-also"></a>Vea también
- [ISymENCUnmanagedMethod (interfaz)](../../../../docs/framework/unmanaged-api/diagnostics/isymencunmanagedmethod-interface.md)
