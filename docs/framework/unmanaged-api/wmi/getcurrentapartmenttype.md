---
title: Función GetCurrentApartmentType (referencia de API no administrada)
description: La función GetCurrentApartmentType recupera el tipo de contenedor en el que se está ejecutando el llamador.
ms.date: 11/06/2017
api_name:
- GetCurrentApartmentType
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- GetCurrentApartmentType
helpviewer_keywords:
- GetCurrentApartmentType function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 76c852ac81126895ea3a2e1b40473722c8445201
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/10/2019
ms.locfileid: "67746560"
---
# <a name="getcurrentapartmenttype-function"></a>Función GetCurrentApartmentType
Recupera el tipo de contenedor en el que se está ejecutando el llamador.   
  
[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
HRESULT GetCurrentApartmentType (
   [in] int                   vFunc, 
   [in] IComThreadingInfo*    ptr, 
   [out] APTTYPE*             aptType
); 
```  

## <a name="parameters"></a>Parámetros

`vFunc`  
[in] Este parámetro se usa.

`ptr`  
[in] Un puntero a un [IComThreadingInfo](/windows/desktop/api/objidlbase/nn-objidlbase-icomthreadinginfo) instancia.

`aptType`  
[out] Un puntero a un [APTTYPE](/windows/desktop/api/objidlbase/ne-objidlbase-_apttype) valor de enumeración que indica el apartamento del llamador.

## <a name="return-value"></a>Valor devuelto

|Constante  |Valor  |DESCRIPCIÓN  |
|---------|---------|---------|
| `S_OK` | 0 | La función que se completó correctamente. |
| `E_FAIL` | 0x80000008 | El llamador no se está ejecutando en un apartamento. |
  
## <a name="remarks"></a>Comentarios

Esta función contiene una llamada a la [IComThreadingInfo::GetCurrentApartmentType](/windows/desktop/api/objidlbase/nf-objidlbase-icomthreadinginfo-getcurrentapartmenttype) método.

## <a name="requirements"></a>Requisitos  
 **Plataformas:** Consulte [Requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado**: WMINet_Utils.idl  
  
 **Versiones de .NET Framework:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>Vea también

- [WMI y contadores de rendimiento (referencia de API no administrada)](index.md)
