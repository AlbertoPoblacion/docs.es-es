---
title: Elemento <listeners> para <trace>
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/trace/listeners
helpviewer_keywords:
- <listeners> element
- listeners element
ms.assetid: 1394c2c3-6304-46db-87c1-8e8b16f5ad5b
ms.openlocfilehash: f9f12d9e61e2472b897169727bbb4fbf9833efd6
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59179119"
---
# <a name="listeners-element-for-trace"></a>\<los agentes de escucha > (elemento) para \<seguimiento >
Especifica un agente de escucha que recopila, almacena y enruta los mensajes. Los agentes de escucha dirigen los resultados de seguimiento a un destino apropiado.  
  
 \<Configuración > elemento  
\<System.Diagnostics > elemento  
\<seguimiento > elemento  
\<los agentes de escucha > (elemento) para \<seguimiento >  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
<listeners>   
  <add>...</add>  
  <clear/>  
  <remove ... />  
</listeners>  
```  
  
## <a name="attributes-and-elements"></a>Atributos y elementos  
 En las siguientes secciones se describen los atributos, los elementos secundarios y los elementos primarios.  
  
### <a name="attributes"></a>Atributos  
 Ninguno.  
  
### <a name="child-elements"></a>Elementos secundarios  
  
|Elemento|Descripción|  
|-------------|-----------------|  
|[\<add>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/add-element-for-listeners-for-trace.md)|Agrega un agente de escucha a la colección `Listeners`.|  
|[\<clear>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/clear-element-for-listeners-for-trace.md)|Borra la colección `Listeners` de un seguimiento.|  
|[\<remove>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/remove-element-for-listeners-for-trace.md)|Quita un agente de escucha el `Listeners` colección.|  
  
### <a name="parent-elements"></a>Elementos primarios  
  
|Elemento|Descripción|  
|-------------|-----------------|  
|`configuration`|Elemento raíz de cada archivo de configuración usado por las aplicaciones de Common Language Runtime y .NET Framework.|  
|`system.diagnostics`|Especifica el elemento raíz de la sección de configuración de ASP.NET.|  
|`trace`|Contiene agentes de escucha que recopilan, almacenan y enrutan los mensajes de seguimiento.|  
  
## <a name="remarks"></a>Comentarios  
 El <xref:System.Diagnostics.Debug> y <xref:System.Diagnostics.Trace> clases comparten el mismo **los agentes de escucha** colección. Si agrega un objeto de escucha a la colección en una de estas clases, la otra clase usa el mismo agente de escucha. Las clases de agente de escucha incluidas en .NET Framework se derivan de la <xref:System.Diagnostics.TraceListener> clase.  
  
## <a name="configuration-file"></a>Archivo de configuración  
 Este elemento se puede usar en el archivo de configuración del equipo (Machine.config) y el archivo de configuración de la aplicación.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente muestra cómo usar el  **\<los agentes de escucha >** elemento para agregar los agentes de escucha `MyListener` y `MyEventListener` a la **los agentes de escucha** colección. `MyListener` crea un archivo denominado `MyListener.log` y escribe el resultado en el archivo. `MyEventListener` crea una entrada en el registro de eventos.  
  
```xml  
<configuration>  
  <system.diagnostics>  
    <trace autoflush="true" indentsize="0">  
      <listeners>  
        <add name="myListener"   
          type="System.Diagnostics.TextWriterTraceListener,   
            system, version=1.0.3300.0, Culture=neutral,   
            PublicKeyToken=b77a5c561934e089"   
          initializeData="c:\myListener.log" />  
        <add name="MyEventListener"  
          type="System.Diagnostics.EventLogTraceListener,   
            system, version=1.0.3300.0, Culture=neutral,   
            PublicKeyToken=b77a5c561934e089"  
          initializeData="MyConfigEventLog"/>  
      </listeners>  
    </trace>  
  </system.diagnostics>  
</configuration>  
```  
  
## <a name="see-also"></a>Vea también

- <xref:System.Diagnostics.TraceListener>
- [Esquema de la configuración de seguimiento y depuración](../../../../../docs/framework/configure-apps/file-schema/trace-debug/index.md)
