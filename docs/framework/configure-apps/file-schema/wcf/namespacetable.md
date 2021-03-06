---
title: '&lt;namespaceTable&gt;'
ms.date: 03/30/2017
ms.assetid: 64801766-01b7-4c65-9ce6-70ad5af67689
ms.openlocfilehash: fb2b324a2c128b470f1a9a21343408280c5e1862
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/23/2019
ms.locfileid: "54743249"
---
# <a name="ltnamespacetablegt"></a>&lt;namespaceTable&gt;

Representa una sección de configuración para definir un conjunto de elementos que contienen el espacio de nombres para prefijar asignaciones que se pueden utilizar a continuación en filtros XPath para el enrutamiento.

**\<system.serviceModel>**   
&nbsp;&nbsp;**\<enrutamiento >**   
&nbsp;&nbsp;&nbsp;&nbsp;**\<namespaceTable>**
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
<system.serviceModel>
  <routing>
    <namespaceTable>
      <add namespace="String"
           prefix="String" />
    </namespaceTable>
  </routing>
</system.serviceModel>
```  
  
## <a name="attributes-and-elements"></a>Atributos y elementos

En las siguientes secciones se describen los atributos, los elementos secundarios y los elementos primarios.

### <a name="attributes"></a>Atributos

Ninguna

### <a name="child-elements"></a>Elementos secundarios

|     | Descripción |
| --- | ----------- |
| [**\<filter>**](../../../../../docs/framework/configure-apps/file-schema/wcf/filter.md) | Define una asignación de prefijo de espacio de nombres usado para expresiones XPath. |

### <a name="parent-elements"></a>Elementos primarios

|     | Descripción |
| --- | ----------- |
| [**\<enrutamiento >**](../../../../../docs/framework/configure-apps/file-schema/wcf/routing.md) | Representa una sección de configuración para definir un conjunto de filtros de enrutamiento, que determinan el tipo de Windows Communication Foundation (WCF)<xref:System.ServiceModel.Dispatcher.MessageFilter> que se usará al evaluar los mensajes entrantes, así como el enrutamiento de las tablas que definen los extremos de destino enviar mensajes cuando coincida un filtro. |

## <a name="see-also"></a>Vea también

- <xref:System.ServiceModel.Routing.Configuration.NamespaceElementCollection?displayProperty=nameWithType>
