---
title: <peerAuthentication> Elemento
ms.date: 03/30/2017
ms.assetid: 09a8a9ff-e395-42f6-8ceb-9d44bdc1cbe1
ms.openlocfilehash: 1e99f6d117604f9ba2672972a4b09e7fe9f96792
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2019
ms.locfileid: "59092973"
---
# <a name="peerauthentication-element"></a>\<peerAuthentication > elemento
Especifica las opciones de autenticación de clientes punto a punto.  
  
 Para obtener más información acerca de la programación de punto a punto, vea [Peer-to-Peer Networking](../../../../../docs/framework/wcf/feature-details/peer-to-peer-networking.md).  
  
 \<system.ServiceModel>  
\<comportamientos >  
\<endpointBehaviors>  
\<comportamiento >  
\<clientCredentials>  
\<peer>  
\<PeerAuthentication>  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
<peerAuthentication customCertificateValidatorType="namespace.typeName, [,AssemblyName] [,Version=version number] [,Culture=culture] [,PublicKeyToken=token]"
                    certificateValidationMode="ChainTrust/None/PeerTrust/PeerOrChainTrust/Custom"
                    revocationMode="NoCheck/Online/Offline"
                    trustedStoreLocation="CurrentUser/LocalMachine" />
```  
  
## <a name="attributes-and-elements"></a>Atributos y elementos  
 En las siguientes secciones se describen los atributos, los elementos secundarios y los elementos primarios  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descripción|  
|---------------|-----------------|  
|`customCertificateValidatorType`|Cadena opcional. Tipo y ensamblado utilizados para validar un tipo personalizado. Se debe establecer este atributo cuando `certificateValidationMode` está establecido en `Custom`.|  
|`certifcateValidationMode`|Enumeración opcional. Especifica uno de los tres modos utilizados para validar las credenciales. Si se establece en `Custom`, también debe proporcionarse un `customCertificateValidator`. De manera predeterminada, es `ChainTrust`.|  
|`revocationMode`|Enumeración opcional. Uno de los modos utilizados para comprobar listas de certificados revocadas (CRL). De manera predeterminada, es `Online`.|  
|`trustedStoreLocation`|Enumeración opcional. Una de las dos ubicaciones de almacenamiento del sistema: `LocalMachine` o `CurrentUser`. Se utiliza este valor cuando un certificado del servicio se negocia al cliente. Se realiza la validación contra el **personas de confianza** almacenar en la ubicación del almacén especificado. De manera predeterminada, es `CurrentUser`.|  
  
## <a name="customcertificatevalidatortype-attribute"></a>Atributo customCertificateValidatorType  
  
|Valor|Descripción|  
|-----------|-----------------|  
|String|Especifica el nombre de tipo y el ensamblado y otros datos utilizados para buscar el tipo. Como mínimo, se requieren un espacio de nombres y un nombre de tipo. La información opcionales incluye: nombre de ensamblado, número de versión, referencia cultural y token de clave pública.|  
  
## <a name="certificatevalidationmode-attribute"></a>Atributo certificateValidationMode  
  
|Valor|Descripción|  
|-----------|-----------------|  
|Enumeración|Uno de los siguientes valores: `None`, `PeerTrust`, `ChainTrust`, `PeerOrChainTrust`, `Custom`. De manera predeterminada, es `ChainTrust`.<br /><br /> Para obtener más información, consulte [trabajar con certificados](../../../../../docs/framework/wcf/feature-details/working-with-certificates.md).|  
  
## <a name="revocationmode-attribute"></a>Atributo revocationMode  
  
|Valor|Descripción|  
|-----------|-----------------|  
|Enumeración|Uno de los siguientes valores: `NoCheck`, `Online`, `Offline`. De manera predeterminada, es `Online`.<br /><br /> Para obtener más información, consulte [trabajar con certificados](../../../../../docs/framework/wcf/feature-details/working-with-certificates.md).|  
  
## <a name="trustedstorelocation-attribute"></a>Atributo trustedStoreLocation  
  
|Valor|Descripción|  
|-----------|-----------------|  
|Enumeración|Uno de los siguientes valores: `LocalMachine` o `CurrentUser`. De manera predeterminada, es `CurrentUser`. Si la aplicación cliente se está ejecutando bajo una cuenta del sistema, entonces el certificado está normalmente bajo `LocalMachine`. Si la aplicación cliente se está ejecutando en una cuenta de usuario, entonces el certificado se encuentra normalmente en `CurrentUser`.|  
  
### <a name="child-elements"></a>Elementos secundarios  
 Ninguno.  
  
### <a name="parent-elements"></a>Elementos primarios  
  
|Elemento|Descripción|  
|-------------|-----------------|  
|[\<peer>](../../../../../docs/framework/configure-apps/file-schema/wcf/peer-of-clientcredentials-element.md)|Especifica una credencial utilizada para autenticar el cliente a un servicio del mismo nivel.|  
  
## <a name="remarks"></a>Comentarios  
 El elemento `<authentication>` corresponde a la clase <xref:System.ServiceModel.Security.X509PeerCertificateAuthentication>. Este elemento especifica un validador, que se invoca durante la autenticación entre vecinos en la malla. Cuando un nuevo par intenta establecer una conexión de vecino, pasa su propia credencial al par que responde. El validador del contestador se invoca para comprobar la credencial de la parte remota. Cuando una conexión del mismo nivel se establece en la malla, se autentican ambos pares mutuamente, lo que significa que se invocan los validadores en ambos extremos.  
  
## <a name="example"></a>Ejemplo  
 El código siguiente establece el modo de validación de certificados en `PeerOrChainTrust`.  
  
```xml  
<behaviors>
  <endpointBehaviors>
    <behavior name="MyEndpointBehavior">
      <clientCredentials>
        <peer>
          <certificate findValue="www.contoso.com"
                       storeLocation="LocalMachine"
                       x509FindType="FindByIssuerName" />
          <peerAuthentication certificateValidationMode="PeerOrChainTrust" />
          <messageSenderAuthentication certificateValidationMode="None" />
        </peer>
      </clientCredentials>
    </behavior>
  </endpointBehaviors>
</behaviors>
```  
  
## <a name="see-also"></a>Vea también

- <xref:System.ServiceModel.Configuration.PeerCredentialElement>
- <xref:System.ServiceModel.Security.X509PeerCertificateAuthentication>
- <xref:System.ServiceModel.Security.PeerCredential.PeerAuthentication%2A>
- <xref:System.ServiceModel.Configuration.PeerCredentialElement.PeerAuthentication%2A>
- <xref:System.ServiceModel.Configuration.X509PeerCertificateAuthenticationElement>
- [Trabajar con certificados](../../../../../docs/framework/wcf/feature-details/working-with-certificates.md)
- [Conexión de redes punto a punto](../../../../../docs/framework/wcf/feature-details/peer-to-peer-networking.md)
- [Autenticación del mensaje del canal del mismo nivel](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/aa967730(v=vs.90))
- [Autenticación personalizada de canal del mismo nivel](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms751447(v=vs.90))
- [Protección de las aplicaciones de canal del mismo nivel](../../../../../docs/framework/wcf/feature-details/securing-peer-channel-applications.md)
