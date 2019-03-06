---
title: <transport> de <wsHttpBinding>
ms.date: 03/30/2017
ms.assetid: 21e38acf-450a-4bda-82b6-de305e1f7cd8
ms.openlocfilehash: ea025751020d6d98292f6bc3ecfe9421af0cb793
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/05/2019
ms.locfileid: "57372326"
---
# <a name="transport-of-wshttpbinding"></a>\<transporte > de \<wsHttpBinding >

Define la configuración de autenticación del transporte HTTP.

\<system.serviceModel>\
\<bindings>\
\<wsHttpBinding>\
\<binding>\
\<seguridad > \
\<transport>

## <a name="syntax"></a>Sintaxis

```xml
<wsHttpBinding>
  <binding>
    <security mode="None|Transport|TransportWithMessageCredential|TransportCredentialOnly">
      <transport clientCredentialType="Basic|Certificate|Digest|None|Ntlm|Windows"
                 proxyCredentialType="Basic|Digest|None|Ntlm|Windows"
                 realm="string" />
        <extendedProtectionPolicy policyEnforcement="Never|WhenSupported|Always"
                                  protectionScenario="TransportSelected|TrustedProxy">
          <customServiceNames>
          </customServiceNames>
        </extendedProtectionPolicy>
      </transport>
    </security>
  </binding>
</wsHttpBinding>
```

## <a name="type"></a>Tipo

<xref:System.ServiceModel.HttpTransportSecurity>

## <a name="attributes-and-elements"></a>Atributos y elementos

En las siguientes secciones se describen los atributos, los elementos secundarios y los elementos primarios.

### <a name="attributes"></a>Atributos

|Atributo|Descripción|
|---------------|-----------------|
|`clientCredentialType`|Especifica la credencial utilizada para autenticar el cliente al servicio. Este atributo es del tipo <xref:System.ServiceModel.HttpClientCredentialType>.|
|`proxyCredentialType`|Especifica la credencial usada para autenticar al cliente en un proxy del dominio. Este atributo es del tipo <xref:System.ServiceModel.HttpProxyCredentialType>.|
|`realm`|Una cadena que especifica el dominio de autenticación para autenticación implícita o básica. El valor predeterminado es una cadena vacía.<br /><br /> Un dominio de autenticación especifica por lo menos el nombre del host que realiza la autenticación. También puede especificar una colección de usuarios que tiene acceso. Un usuario puede consultar el dominio de autenticación para determinar cuál de los posibles nombres de usuario y contraseñas se puede utilizar.|
|`policyEnforcement`|Esta enumeración especifica cuándo se debe aplicar <xref:System.Security.Authentication.ExtendedProtection.ExtendedProtectionPolicy>.<br /><br /> 1.  Never: la directiva nunca se aplica (la protección extendida está deshabilitada).<br />2.  WhenSupported: la directiva solamente se aplica si el cliente admite la protección extendida.<br />3.  Always: la directiva siempre se aplica. Los clientes que no admitan la protección extendida no podrán autenticarse.|

## <a name="clientcredentialtype-attribute"></a>Atributo clientCredentialType

|Valor|Descripción|
|-----------|-----------------|
|`None`|La seguridad está deshabilitada.|
|`Basic`|Usa la autenticación básica.|
|`Digest`|Usa la autenticación implícita.|
|`Ntlm`|Utiliza la autenticación NTLM como reserva con un dominio de Windows.|
|`Windows`|Utiliza la autenticación de Windows integrada.|
|`Certificate`|Utiliza los certificados X.509 para autenticar al cliente.|

## <a name="proxycredentialtype-attribute"></a>Atributo proxyCredentialType

|Valor|Descripción|
|-----------|-----------------|
|`None`|La seguridad está deshabilitada.|
|`Basic`|Usa la autenticación básica.|
|`Digest`|Usa la autenticación implícita.|
|`Ntlm`|Utiliza NTLM como reserva con un dominio de Windows.|
|`Windows`|Utiliza la autenticación de Windows integrada.|
|`Certificate`|Utiliza los certificados X.509 para autenticar al cliente.|

### <a name="child-elements"></a>Elementos secundarios

Ninguno.

### <a name="parent-elements"></a>Elementos primarios

|Elemento|Descripción|
|-------------|-----------------|
|[\<security>](../../../../../docs/framework/configure-apps/file-schema/wcf/security-of-wshttpbinding.md)|Representa las funciones de seguridad de la [ \<wsHttpBinding >](../../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md).|

## <a name="see-also"></a>Vea también

- <xref:System.ServiceModel.HttpTransportSecurity>
- <xref:System.ServiceModel.WSHttpSecurity.Transport%2A>
- <xref:System.ServiceModel.Configuration.WSHttpSecurityElement.Transport%2A>
- <xref:System.ServiceModel.Configuration.HttpTransportSecurityElement>
- [Protección de servicios y clientes](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)
- [Enlaces](../../../../../docs/framework/wcf/bindings.md)
- [Configuración de enlaces proporcionados por el sistema](../../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)
- [Utilización de enlaces para configurar servicios y clientes](../../../../../docs/framework/wcf/using-bindings-to-configure-services-and-clients.md)
- [\<binding>](../../../../../docs/framework/misc/binding.md)
