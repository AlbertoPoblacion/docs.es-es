---
title: ISymUnmanagedBinder::GetReaderForFile (Método)
ms.date: 03/30/2017
api_name:
- ISymUnmanagedBinder.GetReaderForFile
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedBinder::GetReaderForFile
helpviewer_keywords:
- ISymUnmanagedBinder::GetReaderForFile method [.NET Framework debugging]
- GetReaderForFile method [.NET Framework debugging]
ms.assetid: 46c06258-831e-47c8-a50a-8650af6b637e
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 0414cadca910f3290f96a841e3f807f0de469606
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59145969"
---
# <a name="isymunmanagedbindergetreaderforfile-method"></a>ISymUnmanagedBinder::GetReaderForFile (Método)
Dada una interfaz de metadatos y un nombre de archivo, devuelve el valor correcto [ISymUnmanagedReader](isymunmanagedreader-interface.md) interfaz que va a leer los símbolos de depuración asociados al módulo.  
  
 Este método abrirá el archivo de programa (PDB) de la base de datos solo si está junto al archivo ejecutable. Este cambio se realizó por motivos de seguridad. Si necesita una búsqueda más extensa para el archivo PDB, utilice el [ISymUnmanagedBinder2:: Getreaderforfile2](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedbinder2-getreaderforfile2-method.md) método.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
HRESULT GetReaderForFile(  
    [in]  IUnknown     *importer,  
    [in]  const WCHAR  *fileName,  
    [in]  const WCHAR  *searchPath,  
    [out, retval] ISymUnmanagedReader  **pRetVal);  
```  
  
## <a name="parameters"></a>Parámetros  
 `importer`  
 [in] Un puntero a la interfaz de importación de metadatos.  
  
 `fileName`  
 [in] Un puntero al nombre de archivo.  
  
 `searchPath`  
 [in] Un puntero a la ruta de acceso de búsqueda.  
  
 `pRetVal`  
 [out] Un puntero que se establece en el valor devuelto [ISymUnmanagedReader](isymunmanagedreader-interface.md) interfaz.  
  
## <a name="return-value"></a>Valor devuelto  
 S_OK si el método se realiza correctamente; en caso contrario, E_FAIL u otro código de error.  
  
## <a name="requirements"></a>Requisitos  
 **Encabezado**: CorSym.idl, CorSym.h  
  
## <a name="see-also"></a>Vea también

- [ISymUnmanagedBinder (interfaz)](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedbinder-interface.md)
- [GetReaderForFile2 (método)](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedbinder2-getreaderforfile2-method.md)
