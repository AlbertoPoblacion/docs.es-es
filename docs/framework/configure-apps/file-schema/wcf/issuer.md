---
title: '&lt;issuer&gt;'
ms.date: 03/30/2017
ms.assetid: 8c49c6ae-fa1a-4179-a84b-613c3216dcde
ms.openlocfilehash: 8313d7e361356e5159d1f2d531a6dd34ae7ff4d7
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/23/2019
ms.locfileid: "54612182"
---
# <a name="ltissuergt"></a>&lt;issuer&gt;
Especifica el servicio de token de seguridad (STS) que emite los tokens de seguridad.  
  
 \<system.serviceModel>  
\<bindings>  
\<wsFederationHttpBinding>  
\<binding>  
\<security>  
\<message>  
\<issuer>  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
<issuer address="Uri">
  <headers>
    <add name="String"
         namespace="String" />
  </headers>
  <identity>
    <certificate encodedValue="String" />
    <certificateReference findValue="String"
                          isChainIncluded="Boolean"
                          storeName="AddressBook/AuthRoot/CertificateAuthority/Disallowed/My/Root/TrustedPeople/TrustedPublisher"
                          storeLocation="LocalMachine/CurrentUser"
                          x509FindType="System.Security.Cryptography.X509certificates.X509findtype" />
    <dns value="String" />
    <rsa value="String" />
    <servicePrincipalName value="String" />
    <usePrincipalName value="String" />
  </identity>
</issuer>
```  
  
## <a name="attributes-and-elements"></a>Atributos y elementos  
 En las siguientes secciones se describen los atributos, los elementos secundarios y los elementos primarios  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descripción|  
|---------------|-----------------|  
|address|Cadena necesaria. La dirección URL del STS.|  
  
### <a name="child-elements"></a>Elementos secundarios  
  
|Elemento|Descripción|  
|-------------|-----------------|  
|[\<headers>](../../../../../docs/framework/configure-apps/file-schema/wcf/headers-element.md)|Una colección de encabezados de dirección para los puntos de conexión que el generador puede crear.|  
|[\<identity>](../../../../../docs/framework/configure-apps/file-schema/wcf/identity.md)|Al utilizar un token emitido, especifica valores que permiten al cliente autenticar el servidor.|  
  
### <a name="parent-elements"></a>Elementos primarios  
  
|Elemento|Descripción|  
|-------------|-----------------|  
|[\<message>](../../../../../docs/framework/configure-apps/file-schema/wcf/message-element-of-wsfederationhttpbinding.md)|Define la configuración de la seguridad de nivel de mensaje para el [ \<wsFederationHttpBinding >](../../../../../docs/framework/configure-apps/file-schema/wcf/wsfederationhttpbinding.md) elemento.|  
  
## <a name="see-also"></a>Vea también
- <xref:System.ServiceModel.FederatedMessageSecurityOverHttp>
- <xref:System.ServiceModel.Configuration.FederatedMessageSecurityOverHttpElement.Issuer%2A>
- <xref:System.ServiceModel.Configuration.IssuedTokenParametersEndpointAddressElement>
- [Identidad del servicio y autenticación](../../../../../docs/framework/wcf/feature-details/service-identity-and-authentication.md)
- [Federación y tokens emitidos](../../../../../docs/framework/wcf/feature-details/federation-and-issued-tokens.md)
- [Identidad del servicio y autenticación](../../../../../docs/framework/wcf/feature-details/service-identity-and-authentication.md)
- [Federación y tokens emitidos](../../../../../docs/framework/wcf/feature-details/federation-and-issued-tokens.md)
- [Funcionalidades de seguridad con enlaces personalizados](../../../../../docs/framework/wcf/feature-details/security-capabilities-with-custom-bindings.md)
- [Federación y tokens emitidos](../../../../../docs/framework/wcf/feature-details/federation-and-issued-tokens.md)
