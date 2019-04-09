---
title: <issuedToken>
ms.date: 03/30/2017
ms.assetid: b6eae4b7-a6cd-4e1a-b0f6-f407022550b0
ms.openlocfilehash: 83061b283c9430af7bcda9cbc832811fa805ed4c
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2019
ms.locfileid: "59104954"
---
# <a name="issuedtoken"></a>\<issuedToken>
Especifica un token personalizado usado para autenticar un cliente en un servicio.  
  
 \<system.ServiceModel>  
\<comportamientos >  
sección endpointBehaviors  
\<comportamiento >  
\<clientCredentials>  
\<issuedToken>  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
<issuedToken cacheIssuedTokens="Boolean"
             defaultKeyEntropyMode="ClientEntropy/ServerEntropy/CombinedEntropy"
             issuedTokenRenewalThresholdPercentage = "0 to 100"
             issuerChannelBehaviors="String"
             localIssuerChannelBehaviors="String"
             maxIssuedTokenCachingTime="TimeSpan">
</issuedToken>
```  
  
## <a name="attributes-and-elements"></a>Atributos y elementos  
 En las siguientes secciones se describen los atributos, los elementos secundarios y los elementos primarios.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descripción|  
|---------------|-----------------|  
|`cacheIssuedTokens`|Atributo booleano opcional que especifica si los tokens están almacenados en memoria caché. De manera predeterminada, es `true`.|  
|`defaultKeyEntropyMode`|Atributo de cadena opcional que especifica los valores aleatorios (entropías) que se usan para las operaciones del protocolo en enlace. Los valores incluyen `ClientEntropy`, `ServerEntropy` y `CombinedEntropy`. El valor predeterminado es `CombinedEntropy`. Este atributo es del tipo <xref:System.ServiceModel.Security.SecurityKeyEntropyMode>.|  
|`issuedTokenRenewalThresholdPercentage`|Atributo de entero opcional que especifica el porcentaje de un intervalo de tiempo válido (proporcionado por el emisor del token) que puede pasar antes de que se renueve un token. Los valores van de 0 a 100. El valor predeterminado es 60, que especifica el 60% de los pasos de tiempo antes de intentar una renovación.|  
|`issuerChannelBehaviors`|Atributo opcional que especifica los comportamientos del canal que se va a usar al comunicar con el emisor.|  
|`localIssuerChannelBehaviors`|Atributo opcional que especifica los comportamientos del canal que se va a usar al comunicar con el emisor local.|  
|`maxIssuedTokenCachingTime`|Atributo Timespan opcional que especifica la duración que los tokens emitidos están almacenados en memoria caché cuando el emisor del token (un STS) no especifica una hora. El valor predeterminado es "10675199.02:48:05.4775807".|  
  
### <a name="child-elements"></a>Elementos secundarios  
  
|Elemento|Descripción|  
|-------------|-----------------|  
|[\<localIssuer>](../../../../../docs/framework/configure-apps/file-schema/wcf/localissuer.md)|Especifica la dirección del emisor local del token y el enlace usado para comunicarse con el punto de conexión.|  
|[\<issuerChannelBehaviors>](../../../../../docs/framework/configure-apps/file-schema/wcf/issuerchannelbehaviors-element.md)|Especifica los comportamientos del punto de conexión que se va a usar al ponerse en contacto con un emisor local.|  
  
### <a name="parent-elements"></a>Elementos primarios  
  
|Elemento|Descripción|  
|-------------|-----------------|  
|[\<clientCredentials>](../../../../../docs/framework/configure-apps/file-schema/wcf/clientcredentials.md)|Especifica las credenciales usadas para autenticar un cliente a un servicio.|  
  
## <a name="remarks"></a>Comentarios  
 Un token emitido es un tipo de credencial personalizado usado, por ejemplo, al autenticar con un servicio de token seguro (STS) en un escenario aliado. De forma predeterminada, el token es un token de SAML. Para obtener más información, consulte [federación y Tokens emitidos](../../../../../docs/framework/wcf/feature-details/federation-and-issued-tokens.md). y [federación y Tokens emitidos](../../../../../docs/framework/wcf/feature-details/federation-and-issued-tokens.md).  
  
 Esta sección contiene los elementos utilizados para configurar un emisor local de tokens, o los comportamientos utilizados con un servicio de token seguro. Para que obtener instrucciones sobre cómo configurar un cliente para utilizar un emisor local, vea [Cómo: Configurar un emisor Local](../../../../../docs/framework/wcf/feature-details/how-to-configure-a-local-issuer.md).  
  
## <a name="see-also"></a>Vea también

- <xref:System.ServiceModel.Configuration.IssuedTokenClientElement>
- <xref:System.ServiceModel.Configuration.ClientCredentialsElement>
- <xref:System.ServiceModel.Description.ClientCredentials>
- <xref:System.ServiceModel.Configuration.ClientCredentialsElement.IssuedToken%2A>
- <xref:System.ServiceModel.Description.ClientCredentials.IssuedToken%2A>
- <xref:System.ServiceModel.Security.IssuedTokenClientCredential>
- [Comportamientos de seguridad](../../../../../docs/framework/wcf/feature-details/security-behaviors-in-wcf.md)
- [Protección de servicios y clientes](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)
- [Federación y tokens emitidos](../../../../../docs/framework/wcf/feature-details/federation-and-issued-tokens.md)
- [Protección de clientes](../../../../../docs/framework/wcf/securing-clients.md)
- [Filtrar para crear un cliente federado](../../../../../docs/framework/wcf/feature-details/how-to-create-a-federated-client.md)
- [Filtrar para configurar un emisor local](../../../../../docs/framework/wcf/feature-details/how-to-configure-a-local-issuer.md)
- [Federación y tokens emitidos](../../../../../docs/framework/wcf/feature-details/federation-and-issued-tokens.md)
