---
title: ISymENCUnmanagedMethod (Interfaz)
ms.date: 03/30/2017
api_name:
- ISymENCUnmanagedMethod
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymENCUnmanagedMethod
helpviewer_keywords:
- ISymENCUnmanagedMethod interface [.NET Framework debugging]
ms.assetid: faebf594-67d5-4abf-b9c1-547fd3a1ff87
topic_type:
- apiref
ms.openlocfilehash: 47477bb473df8b568844d07bea704df681c9b95d
ms.sourcegitcommit: 9a39f2a06f110c9c7ca54ba216900d038aa14ef3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/23/2019
ms.locfileid: "74448611"
---
# <a name="isymencunmanagedmethod-interface"></a>ISymENCUnmanagedMethod (Interfaz)
Proporciona información para la característica editar y continuar.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descripción|  
|------------|-----------------|  
|[GetDocumentsForMethod (método)](../../../../docs/framework/unmanaged-api/diagnostics/isymencunmanagedmethod-getdocumentsformethod-method.md)|Obtiene los documentos en los que este método tiene líneas.|  
|[GetDocumentsForMethodCount (método)](../../../../docs/framework/unmanaged-api/diagnostics/isymencunmanagedmethod-getdocumentsformethodcount-method.md)|Obtiene el número de documentos en los que este método tiene líneas.|  
|[GetFileNameFromOffset (método)](../../../../docs/framework/unmanaged-api/diagnostics/isymencunmanagedmethod-getfilenamefromoffset-method.md)|Obtiene el nombre de archivo de la línea asociada a un desplazamiento.|  
|[GetLineFromOffset (método)](../../../../docs/framework/unmanaged-api/diagnostics/isymencunmanagedmethod-getlinefromoffset-method.md)|Obtiene la información de línea asociada a un desplazamiento.|  
|[GetSourceExtentInDocument (método)](../../../../docs/framework/unmanaged-api/diagnostics/isymencunmanagedmethod-getsourceextentindocument-method.md)|Obtiene la línea de inicio más pequeña y la línea de finalización más grande para el método en un documento específico.|  
  
## <a name="requirements"></a>Requisitos  
 **Encabezado:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Vea también

- [Interfaces de almacén de símbolos de diagnósticos](../../../../docs/framework/unmanaged-api/diagnostics/diagnostics-symbol-store-interfaces.md)
