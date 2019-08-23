---
title: <authentication>del <serviceCertificate> elemento
ms.date: 03/30/2017
ms.assetid: 733b67b4-08a1-4d25-9741-10046f9357ef
ms.openlocfilehash: d770ba1f9a0a18c927b3a4bf6d4141286e3a380c
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/22/2019
ms.locfileid: "69919983"
---
# <a name="authentication-of-servicecertificate-element"></a>\<> de autenticación \<del elemento de > serviceCertificate
Especifica la configuración utilizada por el proxy del cliente para autenticar certificados del servicio que se obtienen utilizando la negociación de SSL/TLS.  
  
 \<system.ServiceModel>  
\<comportamientos >  
sección endpointBehaviors  
\<comportamiento >  
\<clientCredentials>  
\<serviceCertificate>  
\<> de autenticación  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
<authentication customCertificateValidatorType="String"
                certificateValidationMode="None/PeerTrust/ChainTrust/PeerOrChainTrust/Custom"
                revocationMode="NoCheck/Online/Offline"
                trustedStoreLocation="LocalMachine/CurrentUser" />
```  
  
## <a name="attributes-and-elements"></a>Atributos y elementos  
 En las siguientes secciones se describen los atributos, los elementos secundarios y los elementos primarios  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|DESCRIPCIÓN|  
|---------------|-----------------|  
|customCertificateValidatorType|Cadena. Tipo y ensamblado utilizados para validar un tipo personalizado.|  
|certificateValidationMode|Especifica uno de los tres modos utilizados para validar las credenciales. Si se establece en `Custom`, también debe proporcionarse un customCertificateValidator. El valor predeterminado es `ChainTrust`.|  
|revocationMode|Uno de los modos utilizados para comprobar listas de certificados revocadas (CRL). El valor predeterminado es `Online`.|  
|trustedStoreLocation|Una de las dos ubicaciones de almacenamiento del sistema: `LocalMachine` o `CurrentUser`. Se utiliza este valor cuando un certificado del servicio se negocia al cliente. La validación se realiza en el almacén de **personas de confianza** en la ubicación de almacén especificada. El valor predeterminado es `CurrentUser`.|  
  
## <a name="customcertificatevalidator-attribute"></a>Atributo customCertificateValidator  
  
|Valor|DESCRIPCIÓN|  
|-----------|-----------------|  
|string|Especifica el nombre de tipo y el ensamblado y otros datos utilizados para buscar el tipo.|  
  
## <a name="certificatevalidationmode-attribute"></a>Atributo certificateValidationMode  
  
|Valor|DESCRIPCIÓN|  
|-----------|-----------------|  
|Enumeración|Uno de los siguientes valores: None, confianza, ChainTrust, PeerOrChainTrust, Custom.<br /><br /> Para obtener más información, consulte [trabajar con certificados](../../../wcf/feature-details/working-with-certificates.md).|  
  
## <a name="revocationmode-attribute"></a>Atributo revocationMode  
  
|Valor|DESCRIPCIÓN|  
|-----------|-----------------|  
|Enumeración|Uno de los siguientes valores: Nocheck, en línea, sin conexión.<br /><br /> Para obtener más información, consulte [trabajar con certificados](../../../wcf/feature-details/working-with-certificates.md).|  
  
## <a name="trustedstorelocation-attribute"></a>Atributo trustedStoreLocation  
  
|Valor|DESCRIPCIÓN|  
|-----------|-----------------|  
|Enumeración|Uno de los siguientes valores: LocalMachine o CurrentUser. El valor predeterminado es CurrentUser. Si la aplicación cliente se está ejecutando bajo una cuenta del sistema, entonces el certificado está normalmente en LocalMachine. Si la aplicación cliente se está ejecutando en una cuenta de usuario, entonces el certificado se encuentra normalmente en CurrentUser.|  
  
### <a name="child-elements"></a>Elementos secundarios  
 Ninguno.  
  
### <a name="parent-elements"></a>Elementos primarios  
  
|Elemento|DESCRIPCIÓN|  
|-------------|-----------------|  
|[\<serviceCertificate>](servicecertificate-of-clientcredentials-element.md)|Especifica el certificado que se va a utilizar al autenticar un servicio al cliente.|  
  
## <a name="remarks"></a>Comentarios  
 El atributo `certificateValidationMode` de este elemento de configuración especifica el nivel de confianza utilizado para autenticar certificados. De forma predeterminada, el nivel se establece en `ChainTrust`, que especifica que cada certificado debe encontrarse en una jerarquía de certificados que finalizan en una entidad emisora de certificados de confianza en la parte superior de la cadena. Este es el modo más seguro. También puede establecer el valor en `PeerOrChainTrust`, que especifica que los certificados autoemitidos (confianza del mismo nivel) se aceptan, así como los certificados que están en una cadena de confianza. Se utiliza este valor cuando se desarrollan y depuran clientes y servicios porque los certificados autoemitidos no necesitan adquirirse desde una autoridad de confianza. Al implementar un cliente, utilice en su lugar el valor `ChainTrust`. También puede establecer el valor como `Custom` o `None`. Para utilizar el valor `Custom`, también debe establecer el atributo `customCertificateValidator` en un ensamblado y tipo utilizado para validar el certificado. Para crear su propio validador personalizado, debe heredar a partir de la clase abstracta X509CertificateValidator. Para obtener más información, consulte [Cómo Cree un servicio que emplee un validador](../../../wcf/extending/how-to-create-a-service-that-employs-a-custom-certificate-validator.md)de certificado personalizado.  
  
 El atributo `revocationMode` especifica cómo se comprueba la revocación de los certificados. El valor predeterminado es `online` que indica que se comprobará automáticamente la revocación de los certificados. Para obtener más información, consulte [trabajar con certificados](../../../wcf/feature-details/working-with-certificates.md).  
  
## <a name="example"></a>Ejemplo  
 El siguiente ejemplo realiza dos tareas: En primer lugar, especifica un certificado de servicio para que el cliente lo utilice al comunicarse con puntos de `www.contoso.com` conexión cuyo nombre de dominio está por encima del protocolo http. En segundo lugar, especifica el modo de revocación y ubicación del almacén utilizado durante la autenticación.  
  
```xml  
<serviceCertificate>
  <defaultCertificate findValue="www.contoso.com"
                      storeLocation="LocalMachine"
                      storeName="TrustedPeople"
                      x509FindType="FindByIssuerDistinguishedName" />
  <scopedCertificates>
     <add targetUri="http://www.contoso.com"
          findValue="www.contoso.com"
          storeLocation="LocalMachine"
          storeName="Root"
          x509FindType="FindByIssuerName" />
  </scopedCertificates>
  <authentication revocationMode="Online"
                  trustedStoreLocation="LocalMachine" />
</serviceCertificate>
```  
  
## <a name="see-also"></a>Vea también

- <xref:System.ServiceModel.Configuration.X509RecipientCertificateClientElement>
- <xref:System.ServiceModel.Security.X509CertificateRecipientClientCredential>
- <xref:System.ServiceModel.Security.X509CertificateRecipientClientCredential.Authentication%2A>
- <xref:System.ServiceModel.Security.X509ServiceCertificateAuthentication>
- [Comportamientos de seguridad](../../../wcf/feature-details/security-behaviors-in-wcf.md)
- [Trabajo con certificados](../../../wcf/feature-details/working-with-certificates.md)
- [Procedimientos: Crear un servicio que emplee un validador de certificado personalizado](../../../wcf/extending/how-to-create-a-service-that-employs-a-custom-certificate-validator.md)
- [\<authentication>](authentication-of-clientcertificate-element.md)
- [Protección de clientes](../../../wcf/securing-clients.md)
- [Protección de servicios y clientes](../../../wcf/feature-details/securing-services-and-clients.md)
