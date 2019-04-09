---
title: <service>
ms.date: 03/30/2017
ms.assetid: 13123dd6-c4a9-4a04-a984-df184b851788
ms.openlocfilehash: 68bddc01b02d9885b3f0fc4c2cbc5c3249de03f4
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2019
ms.locfileid: "59197963"
---
# <a name="service"></a>\<service>
El elemento `service` contiene los valores para un servicio de Windows Communication Foundation (WCF). También contiene puntos de conexión que exponen el servicio.  
  
 \<system.ServiceModel>  
\<services>  
\<service>  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
<service behaviorConfiguration="String"
         name="String">
</service>
```  
  
## <a name="attributes-and-elements"></a>Atributos y elementos  
 En las siguientes secciones se describen los atributos, los elementos secundarios y los elementos primarios.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descripción|  
|---------------|-----------------|  
|behaviorConfiguration|Una cadena que contiene el nombre de comportamiento que se va a usar para instanciar el servicio. El nombre de comportamiento debe estar en el ámbito en el punto definido del servicio. El valor predeterminado es una cadena vacía.|  
|name|Atributo String necesario que especifica el tipo del servicio del que se van a crear instancias. Este valor debe equivaler a un tipo válido. El formato debe ser `Namespace.Class.`|  
  
### <a name="child-elements"></a>Elementos secundarios  
  
|Elemento|Descripción|  
|-------------|-----------------|  
|[\<endpoint>](../../../../../docs/framework/configure-apps/file-schema/wcf/endpoint-element.md)|Una colección de elementos `endpoint` que exponen este servicio.|  
|[\<host >](../../../../../docs/framework/configure-apps/file-schema/wcf/host.md)|Especifica el host de esta instancia del servicio. Este elemento es del tipo <xref:System.ServiceModel.Configuration.HostElement>.|  
  
### <a name="parent-elements"></a>Elementos primarios  
  
|Elemento|Descripción|  
|-------------|-----------------|  
|[\<services>](../../../../../docs/framework/configure-apps/file-schema/wcf/services.md)|Elemento raíz de todos los elementos de configuración de WCF.|  
  
## <a name="remarks"></a>Comentarios  
 Los servicios se definen en la sección de `services` del archivo de configuración. Un ensamblado puede contener cualquier número de servicios. Cada servicio tiene su propia sección de configuración de `service`. Esta sección y su contenido definen el contrato de servicios, comportamiento y puntos de conexión del servicio determinado.  
  
 El elemento `behaviorConfiguration` también es opcional. Identifica el comportamiento que el servicio utiliza. El comportamiento especificado en este atributo debe vincular a un comportamiento en ámbito en el mismo archivo de configuración.  
  
 Cada servicio expone uno o más extremos, que tienen su propia dirección y enlace. Todos los enlaces usados dentro del archivo de configuración se deben definir en el ámbito del archivo. Los enlaces se vinculan a los puntos de conexión a través de la combinación de los atributos `name` y `bindingConfiguration`. El atributo `name` describe la sección en la que está definido el enlace. El atributo `bindingConfiguration` define qué configuración se usa dentro de la sección de enlaces. Una sección de enlace puede definir varias configuraciones.  
  
## <a name="example"></a>Ejemplo  
 Éste es un ejemplo de una configuración de servicio.  
  
```xml  
<service behaviorConfiguration="testChannelBehavior"
         name="HelloWorld">
  <endpoint address="/HelloWorld2/"
            name="test"
            bindingNamespace="http://www.cohowinery.com/"
            binding="basicHttpBinding"
            contract="IHelloWorld" />
</service>
```  
  
## <a name="see-also"></a>Vea también

- <xref:System.ServiceModel.Configuration.ServiceElement>
- [Configuración de servicios](../../../../../docs/framework/wcf/configuring-services.md)
