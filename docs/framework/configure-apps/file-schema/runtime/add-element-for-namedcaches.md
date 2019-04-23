---
title: Elemento <add> para <namedCaches>
ms.date: 03/30/2017
helpviewer_keywords:
- add element for <namedCaches>
- <add> element for <namedCaches>
ms.assetid: ce2a63a8-c829-4742-a6ea-72ee5d89f169
ms.openlocfilehash: 9a7e370f9cce0e9ddf6dbe49984b7597e041eb84
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59094533"
---
# <a name="add-element-for-namedcaches"></a>\<Agregar > elemento para \<namedCaches >
Agrega un `namedCache` entrada para el `namedCaches` colección de una memoria caché.  
  
 \<system.runtime.caching>  
\<memoryCache>  
\<namedCaches>  
\<add>  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
<namedCaches>  
    <add name="default" />  
      <!-- child elements -->  
 </namedCaches>  
```  
  
## <a name="type"></a>Tipo  
 `None`  
  
## <a name="attributes-and-elements"></a>Atributos y elementos  
 En las siguientes secciones se describen los atributos, los elementos secundarios y los elementos primarios.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descripción|  
|-|-|  
|`CacheMemoryLimitMegabytes`|Un valor entero que especifica el tamaño máximo permitido (en megabytes) que una instancia de un <xref:System.Runtime.Caching.MemoryCache> pueden crecer hasta. El valor predeterminado es 0, lo que significa que el <xref:System.Runtime.Caching.MemoryCache> heurística de ajuste automático de tamaño de la clase se utiliza de forma predeterminada.|  
|`Name`|Nombre de la memoria caché.|  
|`PhysicalMemoryLimitPercentage`|Un valor de número entero entre 0 y 100 que especifica el porcentaje máximo de memoria instalada físicamente del equipo que puede consumir la memoria caché. El valor predeterminado es 0, lo que significa que el <xref:System.Runtime.Caching.MemoryCache> heurística de ajuste automático de tamaño de la clase se utiliza de forma predeterminada.|  
|`PollingInterval`|Valor que indica el intervalo de tiempo después del cual la implementación de caché compara la carga de memoria actual con los límites de memoria absoluto y de porcentaje que están establecidos para la instancia de caché. Este valor se escribe en formato "Hh".|  
  
### <a name="child-elements"></a>Elementos secundarios  
 `None`  
  
### <a name="parent-elements"></a>Elementos primarios  
  
|Elemento|Descripción|  
|-------------|-----------------|  
|[\<namedCaches>](../../../../../docs/framework/configure-apps/file-schema/runtime/namedcaches-element-cache-settings.md)|Contiene una colección de valores de configuración para la instancia con nombre <xref:System.Runtime.Caching.MemoryCache> instancias.|  
  
## <a name="remarks"></a>Comentarios  
 El `add` elemento agrega una entrada a la `namedCaches` colección de una memoria caché. Puede usar el [borrar](../../../../../docs/framework/configure-apps/file-schema/runtime/clear-element-for-namedcaches.md) elemento antes de usar el `add` elemento que esté seguro de que no hay ninguna otra denominada caché en la colección. Este elemento se puede usar en el archivo machine.config y en el archivo Web.config.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente muestra cómo definir la configuración para el valor predeterminado `namedCache` entrada para el `namedCaches` colección de una memoria caché.  
  
```xml  
<configuration>  
  
  <system.runtime.caching>  
    <memoryCache>  
      <namedCaches>  
          <add name="default"   
               cacheMemoryLimitMegabytes="0"   
               physicalMemoryPercentage="0"  
               pollingInterval="00:02:00" />  
      </namedCaches>  
    </memoryCache>  
  </system.runtime.caching>  
  
</configuration>  
```  
  
## <a name="see-also"></a>Vea también

- [\<namedCaches > elemento (configuración de caché)](../../../../../docs/framework/configure-apps/file-schema/runtime/namedcaches-element-cache-settings.md)
