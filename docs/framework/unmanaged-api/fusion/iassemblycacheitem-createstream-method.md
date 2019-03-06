---
title: IAssemblyCacheItem::CreateStream (Método)
ms.date: 03/30/2017
api_name:
- IAssemblyCacheItem.CreateStream
api_location:
- fusion.dll
api_type:
- COM
f1_keywords:
- IAssemblyCacheItem::CreateStream
helpviewer_keywords:
- CreateStream method [.NET Framework fusion]
- IAssemblyCacheItem::CreateStream method [.NET Framework fusion]
ms.assetid: 697ab0f4-470c-4baa-a415-4a975c42d0d5
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 380e248c8c4e3407fff868cdd9a5c63b63e50c69
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/05/2019
ms.locfileid: "57353912"
---
# <a name="iassemblycacheitemcreatestream-method"></a>IAssemblyCacheItem::CreateStream (Método)

Crea una secuencia con el nombre especificado y el formato.

## <a name="syntax"></a>Sintaxis

```cpp
HRESULT CreateStream (
    [in]  DWORD dwFlags,
    [in]  LPCWSTR pszStreamName,
    [in]  DWORD dwFormat,
    [in]  DWORD dwFormatFlags,
    [out] IStream **ppIStream,
    [in, optional] ULARGE_INTEGER *puliMaxSize
);
```

## <a name="parameters"></a>Parámetros

`dwFlags`\
[in] Marcadores definidos en Fusion.idl.

`pszStreamName`\
[in] El nombre de la secuencia que se va a crear.

`dwFormat`\
[in] El formato del archivo que se transmite por secuencias.

`dwFormatFlags`\
[in] Marcas de formato específicos definidas en Fusion.idl.

`ppIStream`\
[out] Un puntero a la dirección de devuelto [IStream](/windows/desktop/api/objidl/nn-objidl-istream) instancia.

`puliMaxSize`\
[in, optional] El tamaño máximo de la secuencia al que hace referencia `ppIStream`.

## <a name="requirements"></a>Requisitos

**Plataformas:** Consulte [Requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).

**Encabezado**: Fusion.h

**Versiones de .NET Framework:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]

## <a name="see-also"></a>Vea también

- [IAssemblyCacheItem (interfaz)](iassemblycacheitem-interface.md)