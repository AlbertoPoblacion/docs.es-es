---
title: '&lt;modificadores&gt; elemento'
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/switches
- http://schemas.microsoft.com/.NetConfiguration/v2.0#switches
helpviewer_keywords:
- <switches> element
- switches element
- trace switches, <switches> element
ms.assetid: 4cf36786-b89a-40e2-a0f1-86bb9b783343
ms.openlocfilehash: ed5d30408b2c0f45f3bef091f4828bd812a63a7a
ms.sourcegitcommit: b351b0781a035616c90c68ccae6dd60aae66a953
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2019
ms.locfileid: "55083358"
---
# <a name="ltswitchesgt-element"></a>&lt;modificadores&gt; elemento
Contiene modificadores de seguimiento y el nivel en el que están establecidos.  
  
 \<configuration>  
\<system.diagnostics>  
\<switches>  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
      <switches>   
</switches>  
```  
  
## <a name="attributes-and-elements"></a>Atributos y elementos  
 En las siguientes secciones se describen los atributos, los elementos secundarios y los elementos primarios.  
  
### <a name="attributes"></a>Atributos  
 Ninguno.  
  
### <a name="child-elements"></a>Elementos secundarios  
  
|Elemento|Descripción|  
|-------------|-----------------|  
|[\<add>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/add-element-for-switches.md)|Especifica el nivel en el que está establecido un modificador de seguimiento.|  
  
### <a name="parent-elements"></a>Elementos primarios  
  
|Elemento|Descripción|  
|-------------|-----------------|  
|`configuration`|Elemento raíz de cada archivo de configuración usado por las aplicaciones de Common Language Runtime y .NET Framework.|  
|`System.diagnostics`|Especifica los agentes de escucha de seguimiento que recopilan, almacenan y enrutan mensajes, así como el nivel en el que está establecido un modificador de seguimiento.|  
  
## <a name="remarks"></a>Comentarios  
 Puede cambiar el nivel de un modificador de seguimiento colocándola en un archivo de configuración. Si el modificador es un <xref:System.Diagnostics.BooleanSwitch>, puede activar y desactivar. Si el modificador es un <xref:System.Diagnostics.TraceSwitch>, puede asignar distintos niveles para especificar los tipos de seguimiento de mensajes o de depuración genera la aplicación.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente muestra cómo usar el  **\<cambiar >** elemento va a establecer el `General` modificador de seguimiento para el <xref:System.Diagnostics.TraceLevel> nivel y habilitar el `Data` modificador de seguimiento booleano.  
  
```xml  
<configuration>  
   <system.diagnostics>  
      <switches>  
         <add name="General" value="4" />  
         <add name="Data" value="1" />  
      </switches>  
   </system.diagnostics>  
</configuration>  
```  
  
## <a name="see-also"></a>Vea también
- <xref:System.Diagnostics.Switch>
- <xref:System.Diagnostics.TraceSwitch>
- <xref:System.Diagnostics.BooleanSwitch>
- [Esquema de la configuración de seguimiento y depuración](../../../../../docs/framework/configure-apps/file-schema/trace-debug/index.md)
