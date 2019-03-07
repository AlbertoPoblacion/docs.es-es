---
title: FilterInputMessage
ms.date: 03/30/2017
helpviewer_keywords:
- raw input [WPF]
- FilterInputMessage method [WPF]
ms.assetid: 4d74c6cf-7d1d-49ff-96c1-231340ce54f5
ms.openlocfilehash: 65d7795b6c4d8f1386ac9a74772fe8b76bb47622
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/06/2019
ms.locfileid: "57466916"
---
# <a name="filterinputmessage"></a>FilterInputMessage
Lo llama PresentationHost.exe cada vez que se recibe un mensaje a menos que se devuelva E_NOTIMPL.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
HRESULT FilterInputMessage( [in] MSG* pMsg ) ;  
```  
  
## <a name="parameters"></a>Parámetros  
 `pMsg`  
  
 [in] Mensaje WM_INPUT enviado a la ventana que obtiene la entrada sin formato.  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad y valor devuelto  
 HRESULT:  
  
 S_OK: el filtro no procesó el mensaje y se puede producir un procesamiento adicional.  
  
 S_FALSE: el filtro procesó este mensaje y no debe realizarse ningún procesamiento adicional.  
  
 E_NOTIMPL: si se devuelve este valor, [FilterInputMessage](filterinputmessage.md) no se llama de nuevo. Esto se podría devolver desde una aplicación host que solo esté interesada en proporcionar interfaces de usuario personalizadas de progreso y error a PresentationHost.exe y que no esté interesada en que se reenvíen mensajes de entrada sin formato desde PresentationHost.exe.  
  
## <a name="remarks"></a>Comentarios  
 PresentationHost.exe es el destino de varios dispositivos de entrada sin formato, incluidos controles remotos, mouse y teclado. A veces, el comportamiento de la aplicación host depende de entradas que de otra forma serían consumidas por PresentationHost.exe. Por ejemplo, una aplicación host puede depender de recibir ciertos mensajes de entrada para determinar si se debe o no mostrar determinados elementos de la interfaz de usuario.  
  
 Para permitir que la aplicación host recibir los mensajes de entrada necesarios para proporcionar estos comportamientos, PresentationHost.exe reenvía los mensajes de entrada sin formato adecuados para la aplicación hospedada mediante una llamada a [FilterInputMessage](filterinputmessage.md).  
  
 La aplicación hospedada recibe los mensajes de entrada sin formato registrándose con el conjunto de dispositivos de entrada sin formato (dispositivos de interfaz humana) devueltos por [GetRawInputDevices](getrawinputdevices.md).  
  
## <a name="see-also"></a>Vea también
- [WM_INPUT message](/windows/desktop/inputdev/wm-input)
