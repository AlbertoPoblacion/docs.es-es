---
title: ExecNotificationQueryWmi (función) (referencia de API no administrada)
description: ExecNotificationQueryWmi (función) ejecuta una consulta para recibir eventos.
ms.date: 11/06/2017
api_name:
- ExecNotificationQueryWmi
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- ExecNotificationQueryWmi
helpviewer_keywords:
- ExecNotificationQueryWmi function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: aa2233bab82f3cd4d1bbcb59f5714c6e4dc91aa5
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/15/2019
ms.locfileid: "65636556"
---
# <a name="execnotificationquerywmi-function"></a>Función ExecNotificationQueryWmi

Ejecuta una consulta para recibir eventos. La llamada devuelve inmediatamente, y el llamador puede sondear el enumerador devuelto para los eventos cuando llegan. Liberar el enumerador devuelto, cancela la consulta.

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a>Sintaxis

```cpp
HRESULT ExecNotificationQueryWmi (
   [in] BSTR                    strQueryLanguage,
   [in] BSTR                    strQuery,
   [in] long                    lFlags,
   [in] IWbemContext*           pCtx,
   [out] IEnumWbemClassObject** ppEnum,
   [in] DWORD                   authLevel,
   [in] DWORD                   impLevel,
   [in] IWbemServices*          pCurrentNamespace,
   [in] BSTR                    strUser,
   [in] BSTR                    strPassword,
   [in] BSTR                    strAuthority
);
```

## <a name="parameters"></a>Parámetros

`strQueryLanguage`\
[in] Una cadena con el lenguaje de consulta válido compatible con la administración de Windows. Debe ser "WQL", que es el acrónimo de lenguaje de consulta de WMI.

`strQuery`\
[in] El texto de la consulta. Este parámetro no puede ser `null`.

`lFlags`\
[in] Una combinación de los dos indicadores siguientes que afectan al comportamiento de esta función. Estos valores se definen en el *WbemCli.h* archivo de encabezado, también puede definir como constantes en el código.

| Constante | Valor  | Descripción  |
|---------|---------|---------|
| `WBEM_FLAG_RETURN_IMMEDIATELY` | 0x10 | La marca provoca una llamada semisincrónica. Si no se establece esta marca, se produce un error en la llamada. Esto es porque se reciben eventos de forma continua, lo que significa que el usuario debe sondear el enumerador devuelto. Esta llamada de bloqueo indefinidamente hace sea imposible. |
| `WBEM_FLAG_FORWARD_ONLY` | 0x20 | La función devuelve un enumerador de solo avance. Normalmente, los enumeradores de sólo avance son más rápidos y usan menos memoria que los enumeradores convencionales, pero no permiten las llamadas a [clon](clone.md). |

`pCtx`\
[in] Normalmente, este valor es `null`. En caso contrario, es un puntero a un [IWbemContext](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemcontext) instancia que se puede usar el proveedor que está proporcionando los eventos solicitados.

`ppEnum`\
[out] Si se produce ningún error, recibe el puntero en el enumerador que permite al llamador recuperar las instancias en el conjunto de resultados de la consulta. Consulte la [comentarios](#remarks) sección para obtener más información.

`authLevel`\
[in] El nivel de autorización.

`impLevel`\
[in] El nivel de suplantación.

`pCurrentNamespace`\
[in] Un puntero a un [IWbemServices](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemservices) objeto que representa el espacio de nombres actual.

`strUser`\
[in] El nombre de usuario. Consulte la [ConnectServerWmi](connectserverwmi.md) función para obtener más información.

`strPassword`\
[in] La contraseña. Consulte la [ConnectServerWmi](connectserverwmi.md) función para obtener más información.

`strAuthority`\
[in] El nombre de dominio del usuario. Consulte la [ConnectServerWmi](connectserverwmi.md) función para obtener más información.

## <a name="return-value"></a>Valor devuelto

Los siguientes valores devueltos por esta función se definen en el *WbemCli.h* archivo de encabezado, también puede definir como constantes en el código:

|Constante  |Valor  |Descripción  |
|---------|---------|---------|
| `WBEM_E_ACCESS_DENIED` | 0x80041003 | El usuario no tiene permiso para ver una o varias de las clases que puede devolver la función. |
| `WBEM_E_FAILED` | 0x80041001 | Se ha producido un error no especificado. |
| `WBEM_E_INVALID_PARAMETER` | 0x80041008 | Un parámetro no es válido. |
| `WBEM_E_INVALID_CLASS` | 0x80041010 | La consulta especifica una clase que no existe. |
| `WBEMESS_E_REGISTRATION_TOO_PRECISE` | 0x80042002 | Se ha solicitado demasiada precisión en la entrega de eventos. Debe especificarse una mayor tolerancia de sondeo. |
| `WBEMESS_E_REGISTRATION_TOO_BROAD` | 0x80042001 | La consulta solicita más información que puede proporcionar la administración de Windows. Esto `HRESULT` se devuelve cuando una consulta de evento da como resultado una solicitud para sondear todos los objetos en un espacio de nombres. |
| `WBEM_E_INVALID_QUERY` | 0x80041017 | La consulta tuvo un error de sintaxis. |
| `WBEM_E_INVALID_QUERY_TYPE` | 0x80041018 | No se admite el lenguaje de consulta solicitado. |
| `WBEM_E_QUOTA_VIOLATION` | 0x8004106c | La consulta es demasiado compleja. |
| `WBEM_E_OUT_OF_MEMORY` | 0x80041006 | No hay suficiente memoria disponible para completar la operación. |
| `WBEM_E_SHUTTING_DOWN` | 0x80041033 | WMI era probablemente detenido y volver a iniciar. Llame a [ConnectServerWmi](connectserverwmi.md) nuevo. |
| `WBEM_E_TRANSPORT_FAILURE` | 0x80041015 | Error en el vínculo de procedimiento remoto (RPC) de la llamada entre el proceso actual y WMI. |
| `WBEM_E_UNPARSABLE_QUERY` | 0x80041058 | No se puede analizar la consulta. |
| `WBEM_S_NO_ERROR` | 0 | La llamada de función fue correcta.  |

## <a name="remarks"></a>Comentarios

Esta función contiene una llamada a la [IWbemServices::ExecNotificationQuery](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemservices-execnotificationquery) método.

Después de que se devuelva la función, el llamador pasa periódicamente el valor devuelto `ppEnum` de objeto para el [siguiente](next.md) función para ver si los eventos están disponibles.

No hay límite al número de `AND` y `OR` palabras clave que se pueden usar en las consultas WQL. Gran número de palabras clave WQL que se usa en una consulta compleja puede hacer que WMI devolver el `WBEM_E_QUOTA_VIOLATION` (o 0x8004106c) código de error como un `HRESULT` valor. El límite de palabras clave WQL depende de la complejidad de la consulta es.

Si se produce un error en la llamada de función, puede obtener información de error adicional mediante una llamada a la [GetErrorInfo](geterrorinfo.md) función.

## <a name="requirements"></a>Requisitos

**Plataformas:** Consulte [Requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).

**Encabezado**: WMINet_Utils.idl

**Versiones de .NET Framework:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]

## <a name="see-also"></a>Vea también

- [WMI y contadores de rendimiento (referencia de API no administrada)](index.md)
