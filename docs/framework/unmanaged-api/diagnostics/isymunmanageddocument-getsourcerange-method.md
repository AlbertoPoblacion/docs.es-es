---
title: ISymUnmanagedDocument::GetSourceRange (Método)
ms.date: 03/30/2017
api_name:
- ISymUnmanagedDocument.GetSourceRange
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedDocument::GetSourceRange
helpviewer_keywords:
- ISymUnmanagedDocument::GetSourceRange method [.NET Framework debugging]
- GetSourceRange method [.NET Framework debugging]
ms.assetid: 20fefee7-1040-41ba-93dc-bd42f68b90c2
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 59420cfd29c3228aece9fc5ae02b950db6099ea0
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2019
ms.locfileid: "59218477"
---
# <a name="isymunmanageddocumentgetsourcerange-method"></a>ISymUnmanagedDocument::GetSourceRange (Método)
Devuelve el intervalo especificado de código fuente incrustado en el búfer especificado. El búfer debe ser suficientemente grande como para contener el código fuente.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
HRESULT GetSourceRange(  
    [in]  ULONG32  startLine,  
    [in]  ULONG32  startColumn,  
    [in]  ULONG32  endLine,  
    [in]  ULONG32  endColumn,  
    [in]  ULONG32  cSourceBytes,  
    [out] ULONG32  *pcSourceBytes,  
    [out, size_is(cSourceBytes),  
        length_is(*pcSourceBytes)] BYTE source[]);  
```  
  
## <a name="parameters"></a>Parámetros  
 `startLine`  
 [in] La línea inicial del documento actual.  
  
 `startColumn`  
 [in] La columna inicial del documento actual.  
  
 `endLine`  
 [in] La última línea del documento actual.  
  
 `endColumn`  
 [in] La columna final del documento actual.  
  
 `cSourceBytes`  
 [in] El tamaño de la fuente, en bytes.  
  
 `pcSourceBytes`  
 [out] Un puntero a una variable que recibe el tamaño del origen.  
  
 `source`  
 [out] El tamaño y la longitud del intervalo especificado del documento de origen, en bytes.  
  
## <a name="return-value"></a>Valor devuelto  
 S_OK si el método tiene éxito.  
  
## <a name="see-also"></a>Vea también

- [ISymUnmanagedDocument (Interfaz)](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanageddocument-interface.md)
