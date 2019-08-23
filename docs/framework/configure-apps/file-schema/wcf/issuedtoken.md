---
title: <issuedToken>
ms.date: 03/30/2017
ms.assetid: b6eae4b7-a6cd-4e1a-b0f6-f407022550b0
ms.openlocfilehash: 68e3a0802a10b14148188a81ee24ed901caa147f
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/22/2019
ms.locfileid: "69925378"
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
  
|Atributo|DESCRIPCIÓN|  
|---------------|-----------------|  
|`cacheIssuedTokens`|Atributo booleano opcional que especifica si los tokens están almacenados en memoria caché. El valor predeterminado es `true`.|  
|`defaultKeyEntropyMode`|Atributo de cadena opcional que especifica los valores aleatorios (entropías) que se usan para las operaciones del protocolo en enlace. Los valores incluyen `ClientEntropy`, `ServerEntropy` y `CombinedEntropy`. El valor predeterminado es `CombinedEntropy`. Este atributo es del tipo <xref:System.ServiceModel.Security.SecurityKeyEntropyMode>.|  
|`issuedTokenRenewalThresholdPercentage`|Atributo de entero opcional que especifica el porcentaje de un intervalo de tiempo válido (proporcionado por el emisor del token) que puede pasar antes de que se renueve un token. Los valores van de 0 a 100. El valor predeterminado es 60, que especifica el 60% de los pasos de tiempo antes de intentar una renovación.|  
|`issuerChannelBehaviors`|Atributo opcional que especifica los comportamientos del canal que se va a usar al comunicar con el emisor.|  
|`localIssuerChannelBehaviors`|Atributo opcional que especifica los comportamientos del canal que se va a usar al comunicar con el emisor local.|  
|`maxIssuedTokenCachingTime`|Atributo Timespan opcional que especifica la duración que los tokens emitidos están almacenados en memoria caché cuando el emisor del token (un STS) no especifica una hora. El valor predeterminado es "10675199.02:48:05.4775807".|  
  
### <a name="child-elements"></a>Elementos secundarios  
  
|Elemento|DESCRIPCIÓN|  
|-------------|-----------------|  
|[\<localIssuer>](localissuer.md)|Especifica la dirección del emisor local del token y el enlace usado para comunicarse con el punto de conexión.|  
|[\<issuerChannelBehaviors>](issuerchannelbehaviors-element.md)|Especifica los comportamientos del punto de conexión que se va a usar al ponerse en contacto con un emisor local.|  
  
### <a name="parent-elements"></a>Elementos primarios  
  
|Elemento|DESCRIPCIÓN|  
|-------------|-----------------|  
|[\<clientCredentials>](clientcredentials.md)|Especifica las credenciales usadas para autenticar un cliente a un servicio.|  
  
## <a name="remarks"></a>Comentarios  
 Un token emitido es un tipo de credencial personalizado usado, por ejemplo, al autenticar con un servicio de token seguro (STS) en un escenario aliado. De forma predeterminada, el token es un token de SAML. Para obtener más información, vea [Federación y tokens emitidos](../../../wcf/feature-details/federation-and-issued-tokens.md). y [Federación y tokens emitidos](../../../wcf/feature-details/federation-and-issued-tokens.md).  
  
 Esta sección contiene los elementos utilizados para configurar un emisor local de tokens, o los comportamientos utilizados con un servicio de token seguro. Para obtener instrucciones sobre cómo configurar un cliente para utilizar un emisor local, [consulte Cómo: Configurar un emisor](../../../wcf/feature-details/how-to-configure-a-local-issuer.md)local.  
  
## <a name="see-also"></a>Vea también

- <xref:System.ServiceModel.Configuration.IssuedTokenClientElement>
- <xref:System.ServiceModel.Configuration.ClientCredentialsElement>
- <xref:System.ServiceModel.Description.ClientCredentials>
- <xref:System.ServiceModel.Configuration.ClientCredentialsElement.IssuedToken%2A>
- <xref:System.ServiceModel.Description.ClientCredentials.IssuedToken%2A>
- <xref:System.ServiceModel.Security.IssuedTokenClientCredential>
- [Comportamientos de seguridad](../../../wcf/feature-details/security-behaviors-in-wcf.md)
- [Protección de servicios y clientes](../../../wcf/feature-details/securing-services-and-clients.md)
- [Federación y tokens emitidos](../../../wcf/feature-details/federation-and-issued-tokens.md)
- [Protección de clientes](../../../wcf/securing-clients.md)
- [Cómo: Creación de un cliente federado](../../../wcf/feature-details/how-to-create-a-federated-client.md)
- [Cómo: Configuración de un emisor local](../../../wcf/feature-details/how-to-configure-a-local-issuer.md)
- [Federación y tokens emitidos](../../../wcf/feature-details/federation-and-issued-tokens.md)
