---
title: ISymUnmanagedENCUpdate::UpdateSymbolStore2 (Método)
ms.date: 03/30/2017
api_name:
- ISymUnmanagedENCUpdate.UpdateSymbolStore2
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedENCUpdate::UpdateSymbolStore2
helpviewer_keywords:
- ISymUnmanagedENCUpdate::UpdateSymbolStore2 method [.NET Framework debugging]
- UpdateSymbolStore2 method [.NET Framework debugging]
ms.assetid: 35588317-6184-485c-ab41-4b15fc1765d9
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 5a4bcc4e6994f06fabf69e5548ad6922343b7dd5
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/06/2019
ms.locfileid: "57479797"
---
# <a name="isymunmanagedencupdateupdatesymbolstore2-method"></a>ISymUnmanagedENCUpdate::UpdateSymbolStore2 (Método)
Permite que un compilador que omita las funciones que no se han modificado desde el flujo de programa (PDB) de la base de datos, siempre que la información de línea cumpla los requisitos. Con la antigua información de línea PDB y un carácter delta para todas las líneas en la función se puede determinar la información de línea correctos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
HRESULT UpdateSymbolStore2(  
    [in]  IStream      *pIStream,  
    [in]  SYMLINEDELTA* pDeltaLines,  
    [in]  ULONG         cDeltaLines);  
```  
  
## <a name="parameters"></a>Parámetros  
 `pIStream`  
 [in] Un puntero a un [IStream](/windows/desktop/api/objidl/nn-objidl-istream) que contiene la información de línea.  
  
 `pDeltaLines`  
 [in] Un puntero a un [SYMLINEDELTA](../../../../docs/framework/unmanaged-api/diagnostics/symlinedelta-structure.md) estructura que contiene las líneas que han cambiado.  
  
 `cDeltaLines`  
 [in] Un `ULONG` que representa el número de líneas que han cambiado.  
  
## <a name="return-value"></a>Valor devuelto  
 S_OK si el método se realiza correctamente; en caso contrario, E_FAIL u otro código de error.  
  
## <a name="requirements"></a>Requisitos  
 **Encabezado**: CorSym.idl, CorSym.h  
  
## <a name="see-also"></a>Vea también
- [ISymUnmanagedENCUpdate (interfaz)](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedencupdate-interface.md)
