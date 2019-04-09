---
title: <add> Elemento para <listeners> para <source>
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/sources/source/listeners/add
helpviewer_keywords:
- initializeData attribute
- add element for <listeners> for <source>
- <add> element for <listeners> for <source>
ms.assetid: 4ce36ac1-81ef-48e8-b8b2-b5a5b0e2adcb
ms.openlocfilehash: 4d2952e29b09fcf9f81624317e30caf301a61a51
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2019
ms.locfileid: "59165498"
---
# <a name="add-element-for-listeners-for-source"></a>\<Agregar > elemento para \<los agentes de escucha > para \<origen >
Agrega un agente de escucha a la colección `Listeners` para un origen de seguimiento.  
  
 \<configuration>  
\<system.diagnostics>  
\<orígenes >  
\<source>  
\<listeners>  
\<add>  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
<add name="name"   
  type="TraceListenerClassName, Version, Culture, PublicKeyToken"  
  initializeData="data"/>  
```  
  
## <a name="attributes-and-elements"></a>Atributos y elementos  
 En las siguientes secciones se describen los atributos, los elementos secundarios y los elementos primarios.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descripción|  
|---------------|-----------------|  
|`type`|Atributo, se requiere a menos que se hace referencia a un agente de escucha en el `sharedListeners` colección, en el que caso basta con hacer referencia a él por su nombre (consulte la [ejemplo](#example)).<br /><br /> Especifica el tipo del agente de escucha. Debe usar una cadena que cumpla los requisitos especificados en [especificar nombres de tipo completos](../../../../../docs/framework/reflection-and-codedom/specifying-fully-qualified-type-names.md).|  
|`initializeData`|Atributo opcional.<br /><br /> La cadena pasada al constructor de la clase especificada. Un <xref:System.Configuration.ConfigurationException> se produce si la clase no tiene un constructor que toma una cadena.|  
|`name`|Atributo opcional.<br /><br /> Especifica el nombre del agente de escucha.|  
|`traceOutputOptions`|Atributo opcional.<br /><br /> Especifica el <xref:System.Diagnostics.TraceListener.TraceOutputOptions%2A> valor de propiedad para el agente de escucha de seguimiento.|  
|[atributos personalizados]|Atributos opcionales.<br /><br /> Especifica el valor de atributos específicos del agente de escucha identificado por el <xref:System.Diagnostics.TraceListener.GetSupportedAttributes%2A> método para ese agente de escucha. <xref:System.Diagnostics.DelimitedListTraceListener.Delimiter%2A> es un ejemplo de un atributo adicional único para el <xref:System.Diagnostics.DelimitedListTraceListener> clase.|  
  
### <a name="child-elements"></a>Elementos secundarios  
  
|Elemento|Descripción|  
|-------------|-----------------|  
|[\<filter>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/filter-element-for-add-for-listeners-for-source.md)|Agrega un filtro a un agente de escucha en la colección `Listeners` para un origen de seguimiento.|  
  
### <a name="parent-elements"></a>Elementos primarios  
  
|Elemento|Descripción|  
|-------------|-----------------|  
|`configuration`|Elemento raíz de cada archivo de configuración usado por las aplicaciones de Common Language Runtime y .NET Framework.|  
|`system.diagnostics`|Especifica los agentes de escucha de seguimiento que recopilan, almacenan y enrutan mensajes, así como el nivel en el que está establecido un modificador de seguimiento.|  
|`sources`|Contiene orígenes de seguimiento que inician mensajes de seguimiento.|  
|`source`|Contiene un origen de seguimiento que inicia mensajes de seguimiento.|  
|`listeners`|Especifica los agentes de escucha que recopilarán, almacenan y enrutan los mensajes.|  
  
## <a name="remarks"></a>Comentarios  
 Las clases de agente de escucha incluidas en .NET Framework se derivan de la <xref:System.Diagnostics.TraceListener> clase.  
  
 Si no especifica la `name` atributo del agente de escucha de seguimiento, el <xref:System.Diagnostics.TraceListener.Name%2A> el valor predeterminado es propiedad del agente de escucha de seguimiento en una cadena vacía (""). Si la aplicación tiene sólo un agente de escucha, puede agregarlo sin especificar un nombre y quitarlo especificando una cadena vacía para el nombre. Sin embargo, si la aplicación tiene más de un agente de escucha, debe especificar un nombre único para cada agente de escucha de seguimiento, lo que permite identificar y administrar los agentes de escucha de seguimiento individuales en el <xref:System.Diagnostics.TraceSource.Listeners%2A?displayProperty=nameWithType> colección.  
  
> [!NOTE]
>  Agregar más de un agente de escucha de seguimiento del mismo tipo y con el mismo nombre da como resultado del agente de escucha de solo seguimiento de ese tipo y nombre que se va a agregar a la `Listeners` colección. Sin embargo, puede agregar mediante programación varios agentes de escucha idénticos a los `Listeners` colección.  
  
 El valor de la `initializeData` atributo depende del tipo de agente de escucha que cree. No todos los agentes de escucha de seguimiento requieren que se especifique `initializeData`.  
  
> [!NOTE]
>  Cuando se usa el `initializeData` atributo, es posible que obtenga el compilador advertencia "no se declara el atributo 'initializeData'". Esta advertencia se produce porque se validan los valores de configuración con la clase base abstracta <xref:System.Diagnostics.TraceListener>, que no reconoce el `initializeData` atributo. Por lo general, puede omitir esta advertencia para las implementaciones de agente de escucha de seguimiento que tiene un constructor que toma un parámetro.  
  
 En la tabla siguiente se muestran los agentes de escucha de seguimiento que se incluyen con .NET Framework y se describe el valor de sus `initializeData` atributos.  
  
|Clase de agente de escucha de seguimiento|valor del atributo initializeData|  
|--------------------------|------------------------------------|  
|<xref:System.Diagnostics.ConsoleTraceListener?displayProperty=nameWithType>|El `useErrorStream` valor para el <xref:System.Diagnostics.ConsoleTraceListener.%23ctor%2A> constructor.  Establecer el `initializeData` atributo para "`true`"escribir trace y debug de salida a la secuencia de error estándar; establézcalo en"`false`" para escribir en el flujo de salida estándar.|  
|<xref:System.Diagnostics.DelimitedListTraceListener?displayProperty=nameWithType>|El nombre del archivo de la <xref:System.Diagnostics.DelimitedListTraceListener> escribe en.|  
|<xref:System.Diagnostics.EventLogTraceListener?displayProperty=nameWithType>|El nombre de un origen de registro de eventos existente.|  
|<xref:System.Diagnostics.EventSchemaTraceListener?displayProperty=nameWithType>|El nombre del archivo que el <xref:System.Diagnostics.EventSchemaTraceListener> escribe en.|  
|<xref:System.Diagnostics.TextWriterTraceListener?displayProperty=nameWithType>|El nombre del archivo que el <xref:System.Diagnostics.TextWriterTraceListener> escribe en.|  
|<xref:System.Diagnostics.XmlWriterTraceListener?displayProperty=nameWithType>|El nombre del archivo que el <xref:System.Diagnostics.XmlWriterTraceListener> escribe en.|  
  
## <a name="configuration-file"></a>Archivo de configuración  
 Este elemento se puede usar en el archivo de configuración del equipo (Machine.config) y el archivo de configuración de la aplicación.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente muestra cómo usar `<add>` elementos para agregar los agentes de escucha `console` y `textListener` a la `Listeners` recopilación para el origen de seguimiento `TraceSourceApp`. La `textListener` agente de escucha escribe la salida de seguimiento en el archivo myListener.log.  
  
```xml  
<configuration>  
  <system.diagnostics>  
    <sources>  
      <source name="TraceSourceApp" switchName="sourceSwitch"   
        switchType="System.Diagnostics.SourceSwitch">  
        <listeners>  
          <add name="console"   
            type="System.Diagnostics.ConsoleTraceListener"/>  
          <add name="textListener"/>  
          <remove name="Default"/>  
        </listeners>  
      </source>  
    </sources>  
    <sharedListeners>  
      <add name="textListener"   
        type="System.Diagnostics.TextWriterTraceListener"   
        initializeData="myListener.log"/>  
    </sharedListeners>  
    <switches>  
      <add name="sourceSwitch" value="Warning"/>  
    </switches>  
  </system.diagnostics>  
</configuration>   
```  
  
## <a name="see-also"></a>Vea también

- <xref:System.Diagnostics.TraceSource>
- <xref:System.Diagnostics.TraceListener>
- [Esquema de la configuración de seguimiento y depuración](../../../../../docs/framework/configure-apps/file-schema/trace-debug/index.md)
- [Agentes de escucha de seguimiento](../../../../../docs/framework/debug-trace-profile/trace-listeners.md)
