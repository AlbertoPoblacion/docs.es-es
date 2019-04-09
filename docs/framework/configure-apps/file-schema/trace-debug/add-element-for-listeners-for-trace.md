---
title: <add> Elemento para <listeners> para <trace>
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/trace/listeners/add
helpviewer_keywords:
- initializeData attribute
- <add> element for <listeners>
- add element for <listeners>
ms.assetid: 81e804a3-ef11-4d39-bbde-bfa012c179e2
ms.openlocfilehash: ba0ffc4f95b9af7fcd319068501ce0bb9714c2ad
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2019
ms.locfileid: "59089587"
---
# <a name="add-element-for-listeners-for-trace"></a>\<Agregar > elemento para \<los agentes de escucha > para \<seguimiento >
Agrega un agente de escucha para el **los agentes de escucha** colección.  
  
 \<configuration>  
\<system.diagnostics>  
\<trace>  
\<listeners>  
\<add>  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
<add name="name"   
     type="trace listener class name, Version, Culture, PublicKeyToken"  
     initializeData="data"/>  
```  
  
## <a name="attributes-and-elements"></a>Atributos y elementos  
 En las siguientes secciones se describen los atributos, los elementos secundarios y los elementos primarios.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descripción|  
|---------------|-----------------|  
|**type**|Atributo necesario.<br /><br /> Especifica el tipo del agente de escucha. Debe usar una cadena que cumpla los requisitos especificados en [especificar nombres de tipo completos](../../../../../docs/framework/reflection-and-codedom/specifying-fully-qualified-type-names.md).|  
|**initializeData**|Atributo opcional.<br /><br /> La cadena pasada al constructor de la clase especificada.|  
|**name**|Atributo opcional.<br /><br /> Especifica el nombre del agente de escucha.|  
  
### <a name="child-elements"></a>Elementos secundarios  
  
|Elemento|Descripción|  
|-------------|-----------------|  
|[\<filter>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/filter-element-for-add-for-listeners-for-trace.md)|Agrega un filtro a un agente de escucha en el `Listeners` colección para un seguimiento.|  
  
### <a name="parent-elements"></a>Elementos primarios  
  
|Elemento|Descripción|  
|-------------|-----------------|  
|`configuration`|Elemento raíz de cada archivo de configuración usado por las aplicaciones de Common Language Runtime y .NET Framework.|  
|`listeners`|Especifica un agente de escucha que recopila, almacena y enruta los mensajes. Los agentes de escucha dirigen los resultados de seguimiento a un destino apropiado.|  
|`system.diagnostics`|Especifica el elemento raíz de la sección de configuración de ASP.NET.|  
|`trace`|Contiene agentes de escucha que recopilan, almacenan y enrutan los mensajes de seguimiento.|  
  
## <a name="remarks"></a>Comentarios  
 El <xref:System.Diagnostics.Debug> y <xref:System.Diagnostics.Trace> clases comparten el mismo **los agentes de escucha** colección. Si agrega un objeto de escucha a la colección en una de estas clases, la otra clase usa el mismo agente de escucha. El agente de escucha clases se derivan de la <xref:System.Diagnostics.TraceListener>.  
  
 Si no especifica la `name` atributo del agente de escucha de seguimiento, la <xref:System.Diagnostics.TraceListener.Name%2A> de los valores predeterminados del agente de escucha de seguimiento en una cadena vacía (""). Si la aplicación tiene sólo un agente de escucha, puede agregarlo sin especificar un nombre y quitarlo especificando una cadena vacía para el nombre. Sin embargo, si la aplicación tiene más de un agente de escucha, debe especificar nombres únicos para cada agente de escucha de seguimiento, lo que permite identificar y administrar los agentes de escucha de seguimiento individuales dentro de la <xref:System.Diagnostics.Debug.Listeners%2A> y <xref:System.Diagnostics.Trace.Listeners%2A> colecciones.  
  
> [!NOTE]
>  Agregar más de un agente de escucha de seguimiento del mismo tipo y con el mismo nombre da como resultado del agente de escucha de solo seguimiento de ese tipo y nombre que se va a agregar a la `Listeners` colección. Sin embargo, puede agregar mediante programación varios agentes de escucha idénticos a los `Listeners` colección.  
  
 El valor de la **initializeData** atributo depende del tipo de agente de escucha que cree. No todos los agentes de escucha de seguimiento requieren que se especifique **initializeData**.  
  
> [!NOTE]
>  Cuando se usa el `initializeData` atributo, es posible que obtenga el compilador advertencia "no se declara el atributo 'initializeData'". Esta advertencia se produce porque se validan los valores de configuración con la clase base abstracta <xref:System.Diagnostics.TraceListener>, que no reconoce el `initializeData` atributo. Por lo general, puede omitir esta advertencia para las implementaciones de agente de escucha de seguimiento que tiene un constructor que toma un parámetro.  
  
 En la tabla siguiente se muestran los agentes de escucha de seguimiento que se incluyen con .NET Framework y se describe el valor de sus **initializeData** atributos.  
  
|Clase de agente de escucha de seguimiento|valor del atributo initializeData|  
|--------------------------|------------------------------------|  
|<xref:System.Diagnostics.ConsoleTraceListener?displayProperty=nameWithType>|El `useErrorStream` valor para el <xref:System.Diagnostics.ConsoleTraceListener.%23ctor%2A> constructor.  Establecer el `initializeData` atributo para "`true`" escribir, trace y debug de salida a <xref:System.Console.Error%2A?displayProperty=nameWithType>; "`false`" para escribir en <xref:System.Console.Out%2A?displayProperty=nameWithType>.|  
|<xref:System.Diagnostics.DelimitedListTraceListener?displayProperty=nameWithType>|El nombre del archivo de la <xref:System.Diagnostics.DelimitedListTraceListener> escribe en.|  
|<xref:System.Diagnostics.EventLogTraceListener?displayProperty=nameWithType>|El nombre del nombre de un origen de registro de eventos existente.|  
|<xref:System.Diagnostics.EventSchemaTraceListener?displayProperty=nameWithType>|El nombre del archivo que el <xref:System.Diagnostics.EventSchemaTraceListener> escribe en.|  
|<xref:System.Diagnostics.TextWriterTraceListener?displayProperty=nameWithType>|El nombre del archivo que el <xref:System.Diagnostics.TextWriterTraceListener> escribe en.|  
|<xref:System.Diagnostics.XmlWriterTraceListener?displayProperty=nameWithType>|El nombre del archivo que el <xref:System.Diagnostics.XmlWriterTraceListener> escribe en.|  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente muestra cómo usar  **\<Agregar >** elementos para agregar los agentes de escucha `MyListener` y `MyEventListener` a la **los agentes de escucha** colección. `MyListener` crea un archivo denominado `MyListener.log` y escribe el resultado en el archivo. `MyEventListener` crea una entrada en el registro de eventos.  
  
```xml  
<configuration>  
   <system.diagnostics>  
      <trace autoflush="true" indentsize="0">  
         <listeners>  
            <add name="myListener" type="System.Diagnostics.TextWriterTraceListener, system, version=1.0.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" initializeData="c:\myListener.log" />  
            <add name="MyEventListener"  
                 type="System.Diagnostics.EventLogTraceListener, system, version=1.0.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"                 initializeData="MyConfigEventLog"/>  
            <add name="configConsoleListener"  
                 type="System.Diagnostics.ConsoleTraceListener, system, version=1.0.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"/>  
         </listeners>  
      </trace>  
   </system.diagnostics>  
</configuration>  
```  
  
## <a name="see-also"></a>Vea también

- <xref:System.Diagnostics.Trace>
- <xref:System.Diagnostics.Debug>
- <xref:System.Diagnostics.EventLogTraceListener>
- <xref:System.Diagnostics.ConsoleTraceListener>
- <xref:System.Diagnostics.TextWriterTraceListener>
- [Esquema de la configuración de seguimiento y depuración](../../../../../docs/framework/configure-apps/file-schema/trace-debug/index.md)
- [Agentes de escucha de seguimiento](../../../../../docs/framework/debug-trace-profile/trace-listeners.md)
