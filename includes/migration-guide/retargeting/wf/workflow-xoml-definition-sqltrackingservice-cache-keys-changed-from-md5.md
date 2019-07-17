---
ms.openlocfilehash: 47aa67096f8dcd250521d9c34dde97cb2eb368d7
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2019
ms.locfileid: "67803500"
---
### <a name="workflow-xoml-definition-and-sqltrackingservice-cache-keys-changed-from-md5-to-sha256"></a>La definición XOML de flujo de trabajo y las claves de caché de SqlTrackingService han cambiado de MD5 a SHA256

|   |   |
|---|---|
|Detalles|El tiempo de ejecución de flujo de trabajo mantiene una caché de definiciones de flujo de trabajo definido en XOML. SqlTrackingService también mantiene una caché organizada por cadenas. Estas cachés están organizadas según los valores que incluyen el valor de código hash de suma de comprobación. En .NET Framework 4.7.2 y versiones anteriores, este hash de suma de comprobación usaba el algoritmo MD5, que causaba problemas en sistemas compatibles con FIPS. A partir de .NET Framework 4.8, el algoritmo utilizado es SHA256. No debería haber ningún problema de compatibilidad con este cambio ya que los valores se vuelven a calcular cada vez que se inician el tiempo de ejecución de flujo de trabajo y SqlTrackingService. Sin embargo, hemos proporcionado una interpretación para permitir que los clientes puedan volver a usar el algoritmo hash heredado, en caso necesario.|
|Sugerencia|Si este cambio supone un problema al ejecutar los flujos de trabajo, pruebe a establecer uno o ambos modificadores <code>AppContext</code>:<ul><li>&quot;Switch.System.Workflow.Runtime.UseLegacyHashForWorkflowDefinitionDispenserCacheKey&quot; en true.</li><li>&quot;Switch.System.Workflow.Runtime.UseLegacyHashForSqlTrackingCacheKey&quot; en true.</li></ul>Mediante código:<pre><code class="lang-csharp">System.AppContext.SetSwitch(&quot;Switch.System.Workflow.Runtime.UseLegacyHashForWorkflowDefinitionDispenserCacheKey&quot;, true);&#13;&#10;System.AppContext.SetSwitch(&quot;Switch.System.Workflow.Runtime.UseLegacyHashForSqlTrackingCacheKey&quot;, true);&#13;&#10;</code></pre>O en el archivo de configuración (que debe estar en el archivo de configuración de la aplicación que está creando el objeto <xref:System.Workflow.Runtime.WorkflowRuntime>):<pre><code class="lang-xml">&lt;configuration&gt;&#13;&#10;&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Workflow.Runtime.UseLegacyHashForWorkflowDefinitionDispenserCacheKey=true&quot; /&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Workflow.Runtime.UseLegacyHashForSqlTrackingCacheKeytrue&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;&lt;/configuration&gt;&#13;&#10;</code></pre>|
|Ámbito|Secundaria|
|Versión|4.8|
|Tipo|Redestinación|

