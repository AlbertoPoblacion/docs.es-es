---
ms.openlocfilehash: db8eb017bdf166b0f1a241f5a8f7db9b9430898a
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2019
ms.locfileid: "67859117"
---
### <a name="throttle-concurrent-requests-per-session"></a>Límite de solicitudes simultáneas por sesión

|   |   |
|---|---|
|Detalles|En .NET Framework 4.6.2 y en versiones anteriores, ASP.NET ejecuta las solicitudes con el mismo Sessionid de manera secuencial y siempre emite el Sessionid mediante cookies de forma predeterminada. Si una página tarda mucho tiempo en responder, reducirá considerablemente el rendimiento del servidor simplemente presionando F5 en el explorador. En la corrección, se ha agregado un contador para realizar el seguimiento de las solicitudes en cola y finalizar las solicitudes cuando superen un límite especificado. El valor predeterminado es 50. Si se alcanza el límite, se registrará una advertencia en el registro de eventos y se podrá grabar una respuesta HTTP 500 en el registro de IIS.|
|Sugerencia|Para restaurar el comportamiento anterior, puede agregar la siguiente configuración al archivo web.config para rechazar el nuevo comportamiento.<pre><code class="lang-xml">&lt;appSettings&gt;&#13;&#10;&lt;add key=&quot;aspnet:RequestQueueLimitPerSession&quot; value=&quot;2147483647&quot;/&gt;&#13;&#10;&lt;/appSettings&gt;&#13;&#10;</code></pre>|
|Ámbito|Borde|
|Versión|4.7|
|Tipo|Redestinación|

