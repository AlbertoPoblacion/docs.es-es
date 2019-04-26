---
title: Seguimiento de actividades en la seguridad de mensajes
ms.date: 03/30/2017
ms.assetid: 68862534-3b2e-4270-b097-8121b12a2c97
ms.openlocfilehash: c3bd36598fd903dc016959149e563174624d084b
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61912657"
---
# <a name="activity-tracing-in-message-security"></a>Seguimiento de actividades en la seguridad de mensajes
En este tema se describe el seguimiento de actividades para el procesamiento de seguridad, que pasa en las tres fases siguientes.  
  
-   Intercambio de SCT/negociación. Esto puede pasar en la capa de transporte (a través del intercambio de datos binarios) o en la capa de mensaje (a través de intercambios de mensajes SOAP).  
  
-   Cifrado/descifrado del mensaje, con comprobación y autenticación de firma. Los seguimientos aparecen en la actividad ambiente, normalmente la “Acción de proceso"."  
  
-   Autorización y comprobación. Esto puede pasar localmente o en la comunicación entre extremos.  
  
## <a name="negotiationsct-exchange"></a>Intercambio de SCT/negociación.  
 En la fase de intercambio de SCT/negociación, se crean dos tipos de actividad en el cliente: "Configurar sesión segura" y "Cerrar sesión segura". “Configurar sesión segura” abarca los seguimientos de los intercambios de mensajes RST/RSTR/SCT, mientras que “Cerrar sesión segura” incluye los seguimientos para el mensaje de cancelación.  
  
 En el servidor, cada solicitud/responda para RST/RSTR/SCT aparece en su propia actividad. Si `propagateActivity` = `true` en el servidor y cliente, las actividades del servidor tienen el mismo identificador y aparecen juntas en el "Configurar sesión segura" cuando se ven a través de Service Trace Viewer.  
  
 Esta modelo de seguimiento de actividades es válido para la autenticación de nombre de usuario/contraseña, autenticación de certificado y autenticación NTLM.  
  
 La tabla siguiente hace una lista de las actividades y seguimientos para el intercambio de SCT y negociación.  
  
||Hora en la que sucede el intercambio SCT/negociación|Actividades|Seguimientos|  
|-|-------------------------------------------------|----------------|------------|  
|Transporte Seguro<br /><br /> (HTTPS, SSL)|En primer mensaje recibido.|Los seguimientos se emiten en la actividad ambiente.|: Realiza un seguimiento de Exchange<br />-Canal seguro establecido<br />-Secretos obtenidos del recurso compartido.|  
|Capa de mensajes segura<br /><br /> (WSHTTP)|En primer mensaje recibido.|En el cliente:<br /><br /> -"Configurar sesión segura" de "Acción de proceso" de ese primer mensaje, para cada solicitud/respuesta para RST/RSTR/SCT.<br />-"Cerrar sesión segura" para el intercambio Cancelar, fuera de la "actividad cerrar Proxy". Esta actividad puede pasar debido a alguna otra actividad ambiente, dependiendo de cuándo se cierre la sesión segura.<br /><br /> En el servidor:<br /><br /> : Actividad "Procesar acción" una para cada solicitud/respuesta para RST/SCT/Cancelar en el servidor. Si `propagateActivity` = `true`, las actividades RST/RSTR/SCT se combinan con "Configurar sesión de seguridad" y Cancelar se combina con la actividad "Cerrar" desde el cliente.<br /><br /> Hay dos fases para “Configurar sesión segura”:<br /><br /> 1.  Negociación de autenticación. Esto es opcional si el cliente ya tiene las credenciales apropiadas. Esta fase se puede hacer a través de transporte seguro o a través de intercambios de mensajes. En el caso último, pueden tener lugar 1 ó 2 intercambios RST/RSTR. Para estos intercambios, los seguimientos se emiten en nuevas actividades de solicitud/respuesta como se diseñó previamente.<br />2.  Establecimiento de sesión segura (SCT), en la que tiene lugar un intercambio RST/RSTR. Esto tiene las mismas actividades de ambiente, tal y como se describió previamente.|: Realiza un seguimiento de Exchange<br />-Canal seguro establecido<br />-Secretos obtenidos del recurso compartido.|  
  
> [!NOTE]
>  En modo de seguridad mixta, la autenticación de la negociación tiene lugar en intercambios binarios, pero SCT sucede en intercambio de mensajes. En modo de transporte puro, la negociación solo sucede en transporte sin actividades adicionales.  
  
## <a name="message-encryption-and-decryption"></a>Cifrado y descifrado de mensajes  
 La tabla siguiente hace una lista de las actividades y seguimientos para el cifrado/descifrado de mensajes, así como la autenticación de la firma.  
  
||Transporte Seguro<br /><br /> (HTTPS, SSL) y capa de mensajes segura<br /><br /> (WSHTTP)|  
|-|---------------------------------------------------------------------------------|  
|Hora en la que tiene lugar el cifrado/descifrado y la autenticación de la firma|En mensaje recibido|  
|Actividades|Los seguimientos se emiten en la actividad ProcessAction en el cliente y servidor.|  
|Seguimientos|-   sendSecurityHeader (sender):<br />: Mensaje de inicio de sesión<br />-Cifrar los datos de solicitud<br />-   receiveSecurityHeader (receiver):<br />-Comprobar firma<br />-Descifrar los datos de respuesta<br />-Autenticación|  
  
> [!NOTE]
>  En modo de transporte puro, el cifrado/descifrado del mensaje solo sucede en transporte sin actividades adicionales.  
  
## <a name="authorization-and-verification"></a>Autorización y comprobación  
 La tabla siguiente hace una lista de las actividades y seguimiento para la autorización.  
  
||Hora en la que tiene lugar la autorización|Actividades|Seguimientos|  
|-|-------------------------------------|----------------|------------|  
|Local (valor predeterminado)|Después de que se haya descifrado el mensaje en el servidor|Los seguimientos se emiten en la actividad ProcessAction en el servidor.|Usuario autorizado.|  
|Remoto|Después de que se haya descifrado el mensaje en el servidor|Los seguimientos se emiten en una nueva actividad invocada por la actividad ProcessAction.|Usuario autorizado.|
