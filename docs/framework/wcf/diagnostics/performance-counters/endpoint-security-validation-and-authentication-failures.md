---
title: 'Punto de conexión: Errores de autenticación y validación de la seguridad'
ms.date: 03/30/2017
ms.assetid: 5bad60aa-6084-4c7b-aefd-9b581f04382e
ms.openlocfilehash: e69549a276e2f9cece966dd44f6a1b3a3d3cb59f
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61916336"
---
# <a name="endpoint-security-validation-and-authentication-failures"></a>Punto de conexión: Errores de autenticación y validación de la seguridad
Nombre del contador: Errores de autenticación y validación de la seguridad  
  
## <a name="description"></a>Descripción  
 Este contador se incrementa siempre que se rechaza un mensaje debido a un problema de seguridad que no abarca el contador "Llamadas de seguridad no autorizadas". Entre estos problemas se incluyen:  
  
-   No se puede leer el token de cliente en el mensaje.  
  
-   Error al autenticar el token del cliente (contraseña errónea).  
  
-   Error en la comprobación de la firma (mensaje manipulado).  
  
-   El mensaje es un duplicado de uno anterior, que puede producirse durante un ataque de reproducción.  
  
-   Error de descifrado.  
  
-   Faltan algunos elementos necesarios (marca de tiempo o bloque de datos cifrados) en el mensaje.  
  
-   Errores durante el protocolo de enlace TLSNEGO/SPNEGO.
