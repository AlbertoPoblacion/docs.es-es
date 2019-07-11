---
title: GetMethodOrigin (función) (referencia de API no administrada)
description: GetMethodOrigin (función) determina la clase en el que se declara un método.
ms.date: 11/06/2017
api_name:
- GetMethodOrigin
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- GetMethodOrigin
helpviewer_keywords:
- GetMethodOrigin function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 6b21e08d3bf6845b9fc44d5a5edef0ea39b91da5
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/10/2019
ms.locfileid: "67746527"
---
# <a name="getmethodorigin-function"></a>Función GetMethodOrigin
Determina la clase en la que se declara un método.

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
    
## <a name="syntax"></a>Sintaxis  
  
```cpp  
HRESULT GetMethodOrigin (
   [in] int                 vFunc, 
   [in] IWbemClassObject*   ptr, 
   [in] LPCWSTR             wszMethodName,
   [out] BSTR*              pstrClassName
); 
```  

## <a name="parameters"></a>Parámetros

`vFunc`  
[in] Este parámetro se usa.

`ptr`  
[in] Un puntero a un [IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) instancia.

`wszMethodName`  
[in] El nombre del método para el objeto cuya clase propietaria se solicita. 

`pstrClassName`  
[out] Recibe el nombre de la clase que posee el método.

## <a name="return-value"></a>Valor devuelto

Los siguientes valores devueltos por esta función se definen en el *WbemCli.h* archivo de encabezado, también puede definir como constantes en el código:

|Constante  |Value  |DESCRIPCIÓN  |
|---------|---------|---------|
|`WBEM_E_NOT_FOUND` | 0x80041002 | No se encontró el método especificado. |
|`WBEM_E_INVALID_PARAMETER` | 0x80041008 | Uno o más parámetros no son válidos. |
|`WBEM_S_NO_ERROR` | 0 | La llamada de función fue correcta.  |
  
## <a name="remarks"></a>Comentarios

Esta función contiene una llamada a la [IWbemClassObject::GetMethodOrigin](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-getmethod) método.

Porque una clase puede heredar los métodos de una o más clases bases, los desarrolladores a menudo desean determinar la clase en el que se define un método determinado.

El `pstrClassName` parámetro no debe apuntar a una `BSTR` antes de llama a la función porque se trata de un `out` parámetro; este puntero no se desasigna cuando la función vuelve.

## <a name="requirements"></a>Requisitos  
**Plataformas:** Consulte [Requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado**: WMINet_Utils.idl  
  
 **Versiones de .NET Framework:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>Vea también

- [WMI y contadores de rendimiento (referencia de API no administrada)](index.md)
