---
title: Elemento <Thread_UseAllCpuGroups>
ms.date: 03/30/2017
ms.assetid: d30fe7c5-8469-46e2-b804-e3eec7b24256
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 236953cc1a430a1dd2a2fbb633c7ef06e6ba200f
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61704692"
---
# <a name="threaduseallcpugroups-element"></a>\<Thread_UseAllCpuGroups > elemento
Especifica si el runtime distribuye subprocesos administrados en todos los grupos de CPU.  
  
 \<configuration>  
\<runtime>  
<Thread_UseAllCpuGroups>  
  
## <a name="syntax"></a>Sintaxis  
  
```xml
<Thread_UseAllCpuGroups    
   enabled="true|false"/>  
```  
  
## <a name="attributes-and-elements"></a>Atributos y elementos  
 En las siguientes secciones se describen los atributos, los elementos secundarios y los elementos primarios.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descripción|  
|---------------|-----------------|  
|`enabled`|Atributo necesario.<br /><br /> Especifica si el runtime distribuye subprocesos administrados en todos los grupos de CPU.|  
  
## <a name="enabled-attribute"></a>Atributo enabled  
  
|Valor|Descripción|  
|-----------|-----------------|  
|`false`|El runtime no distribuye los subprocesos administrados en varios grupos de CPU. Este es el valor predeterminado.|  
|`true`|El runtime distribuye subprocesos administrados en varios grupos de CPU, si el equipo tiene varios grupos de CPU y la [ \<GCCpuGroup >](../../../../../docs/framework/configure-apps/file-schema/runtime/gccpugroup-element.md) elemento está habilitado.|  
  
### <a name="child-elements"></a>Elementos secundarios  
 Ninguno.  
  
### <a name="parent-elements"></a>Elementos primarios  
  
|Elemento|Descripción|  
|-------------|-----------------|  
|`configuration`|Elemento raíz de cada archivo de configuración usado por las aplicaciones de Common Language Runtime y .NET Framework.|  
|`runtime`|Contiene información del enlace del ensamblado y de la recolección de elementos no utilizados.|  
  
## <a name="remarks"></a>Comentarios  
 Cuando un equipo tiene varios grupos de CPU, si se habilita este elemento, el runtime pueda distribuir subprocesos administrados en todos los grupos de CPU. Para usar esta característica, debe habilitar también la [ \<GCCpuGroup >](../../../../../docs/framework/configure-apps/file-schema/runtime/gccpugroup-element.md) elemento, que extiende la recolección para todos los grupos de CPU y tiene todos los núcleos en cuenta al crear y equilibra montones. Habilitar la [ \<GCCpuGroup >](../../../../../docs/framework/configure-apps/file-schema/runtime/gccpugroup-element.md) elemento requiere la habilitación de la [ \<gcServer >](../../../../../docs/framework/configure-apps/file-schema/runtime/gcserver-element.md) elemento. Si estos elementos no están habilitados, habilite el `<Thread_UseAllCpuGroups>` elemento no tiene ningún efecto.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente muestra cómo habilitar la compatibilidad con varios grupos de CPU.  
  
```xml  
<configuration>  
   <runtime>  
      <Thread_UseAllCpuGroups enabled="true"/>  
      <GCCpuGroup enabled="true"/>  
      <gcServer enabled="true"/>  
   </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>Vea también

- [Esquema de la configuración de Common Language Runtime](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)
- [Esquema de los archivos de configuración](../../../../../docs/framework/configure-apps/file-schema/index.md)
- [\<GCCpuGroup > elemento](../../../../../docs/framework/configure-apps/file-schema/runtime/gccpugroup-element.md)
