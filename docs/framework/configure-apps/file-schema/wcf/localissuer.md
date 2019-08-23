---
title: <localIssuer>
ms.date: 03/30/2017
ms.assetid: 26bdd0df-0e7d-4b9e-bbeb-f28c53769385
ms.openlocfilehash: 4ec5a99139112ae600c1c2bc44feb6d3f62da1e0
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/22/2019
ms.locfileid: "69931736"
---
# <a name="localissuer"></a>\<localIssuer>
Especifica la dirección y el enlace del emisor local que se van a usar para obtener un token de seguridad.  
  
 \<system.ServiceModel>  
\<comportamientos >  
sección endpointBehaviors  
\<comportamiento >  
\<clientCredentials>  
\<issuedToken>  
\<localIssuer>  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
<localIssuer address="String"
             binding="String"
             bindingConfiguration="String" />
```  
  
## <a name="attributes-and-elements"></a>Atributos y elementos  
 En las siguientes secciones se describen los atributos, los elementos secundarios y los elementos primarios  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|DESCRIPCIÓN|  
|---------------|-----------------|  
|dirección|Cadena necesaria. Especifica el URI del emisor local.|  
|enlace|Cadena opcional. Uno de los enlaces proporcionados por el sistema. Para obtener una lista, vea [enlaces proporcionados](../../../wcf/system-provided-bindings.md)por el sistema.|  
|bindingConfiguration|Cadena opcional. Especifica una configuración de enlace situada en el archivo de configuración.|  
  
### <a name="child-elements"></a>Elementos secundarios  
  
|Elemento|DESCRIPCIÓN|  
|-------------|-----------------|  
|[\<identity>](identity.md)|Especifica la información de identidad para el emisor local.|  
|[\<headers>](headers-element.md)|Colección de encabezados de dirección necesaria para poder direccionar el emisor local correctamente. Puede utilizar la palabra clave `add` para agregar un encabezado a esta colección.|  
  
### <a name="parent-elements"></a>Elementos primarios  
  
|Elemento|DESCRIPCIÓN|  
|-------------|-----------------|  
|[\<issuedToken>](issuedtoken.md)|Especifica un token personalizado usado para autenticar un cliente en un servicio.|  
  
## <a name="remarks"></a>Comentarios  
 Al obtener un token emitido de un Servicio de token de seguridad  (STS), la aplicación cliente se debe configurar con el enlace y la dirección que se van a usar para comunicarse con el STS. Cuando no proporciona una dirección URL para el servicio de token de seguridad, o cuando la dirección del emisor de un enlace federado `http://schemas.microsoft.com/2005/12/ServiceModel/Addressing/Anonymous` es `null`o, el canal de Windows Communication Foundation (WCF) del cliente usa los valores especificados por. <xref:System.ServiceModel.WSFederationHttpBinding> `address` y`binding` para comunicarse con el STS para obtener el token emitido. Para obtener más información sobre la configuración de un emisor local [, consulte Cómo: Configurar un emisor](../../../wcf/feature-details/how-to-configure-a-local-issuer.md)local.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente establece `address`, `binding`y atributos `bindingConfiguration` de un elemento `localIssuer`.  
  
```xml  
<system.serviceModel>
  <behaviors>
    <endpointBehaviors>
      <behavior name="MyEndpointBehavior">
        <clientCredentials>
          <issuedToken cacheIssuedTokens="false"
                       defaultKeyEntropyMode="ClientEntropy">
            <localIssuer address="net.tcp://cohowinery/tokens"
                         binding="netTcpBinding"
                         bindingConfiguration="myTcpBindingConfig" />
          </issuedToken>
        </clientCredentials>
      </behavior>
    </endpointBehaviors>
  </behaviors>
</system.serviceModel>
```  
  
## <a name="see-also"></a>Vea también

- <xref:System.ServiceModel.Configuration.IssuedTokenClientElement.LocalIssuer%2A>
- <xref:System.ServiceModel.Configuration.IssuedTokenParametersEndpointAddressElement>
- <xref:System.ServiceModel.Security.IssuedTokenClientCredential>
- [Comportamientos de seguridad](../../../wcf/feature-details/security-behaviors-in-wcf.md)
- [Cómo: Configuración de un emisor local](../../../wcf/feature-details/how-to-configure-a-local-issuer.md)
- [Identidad del servicio y autenticación](../../../wcf/feature-details/service-identity-and-authentication.md)
- [Comportamientos de seguridad](../../../wcf/feature-details/security-behaviors-in-wcf.md)
- [Federación y tokens emitidos](../../../wcf/feature-details/federation-and-issued-tokens.md)
- [Protección de servicios y clientes](../../../wcf/feature-details/securing-services-and-clients.md)
- [Protección de clientes](../../../wcf/securing-clients.md)
- [Procedimientos: Creación de un cliente federado](../../../wcf/feature-details/how-to-create-a-federated-client.md)
- [Federación y tokens emitidos](../../../wcf/feature-details/federation-and-issued-tokens.md)
