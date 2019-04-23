---
title: Procedimiento para configurar las credenciales en un servicio de federación
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF, federation
- federation
ms.assetid: 149ab165-0ef3-490a-83a9-4322a07bd98a
ms.openlocfilehash: 33df685b4d14130ae00d59012706b7637924c9be
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59295437"
---
# <a name="how-to-configure-credentials-on-a-federation-service"></a>Procedimiento para configurar las credenciales en un servicio de federación
En Windows Communication Foundation (WCF), crear un servicio federado consta de los siguientes procedimientos principales:  
  
1. Configurar un <xref:System.ServiceModel.WSFederationHttpBinding> o un enlace personalizado similar. Para obtener más información acerca de cómo crear un enlace adecuado, vea [Cómo: Crear un WSFederationHttpBinding](../../../../docs/framework/wcf/feature-details/how-to-create-a-wsfederationhttpbinding.md).  
  
2. Configurar el <xref:System.ServiceModel.Security.IssuedTokenServiceCredential> que controla cómo se autentican los tokens emitidos que se presentan al servicio.  
  
 Este tema proporciona detalles sobre el segundo paso. Para obtener más información acerca de cómo funciona un servicio federado, vea [federación](../../../../docs/framework/wcf/feature-details/federation.md).  
  
### <a name="to-set-the-properties-of-issuedtokenservicecredential-in-code"></a>Para establecer las propiedades de IssuedTokenServiceCredential en el código  
  
1. Utilice la propiedad <xref:System.ServiceModel.Description.ServiceCredentials.IssuedTokenAuthentication%2A> de la clase <xref:System.ServiceModel.Description.ServiceCredentials> para devolver una referencia a una instancia <xref:System.ServiceModel.Security.IssuedTokenServiceCredential>. Se obtiene acceso a la propiedad desde la propiedad <xref:System.ServiceModel.ServiceHostBase.Credentials%2A> de la clase <xref:System.ServiceModel.ServiceHostBase>.  
  
2. Establezca la propiedad <xref:System.ServiceModel.Security.IssuedTokenServiceCredential.AllowUntrustedRsaIssuers%2A> en `true` si los tokens emitidos automáticamente como las tarjetas [!INCLUDE[infocard](../../../../includes/infocard-md.md)] se van a autenticar. De manera predeterminada, es `false`.  
  
3. Rellene la colección devuelta por la propiedad <xref:System.ServiceModel.Security.IssuedTokenServiceCredential.KnownCertificates%2A> con instancias de la clase <xref:System.Security.Cryptography.X509Certificates.X509Certificate2>. Cada instancia representa un emisor desde el que el servicio autenticará los tokens.  
  
    > [!NOTE]
    >  A diferencia de la colección del lado del cliente devuelta por la propiedad <xref:System.ServiceModel.Security.X509CertificateRecipientClientCredential.ScopedCertificates%2A>, la colección de certificados conocida no es una colección con clave. El servicio acepta los tokens que los certificados especificados emiten sin tener en cuenta la dirección del cliente que envió el mensaje con el token emitido (sujeto a las restricciones siguientes, que se describirán más adelante).  
  
4. Establezca la propiedad <xref:System.ServiceModel.Security.IssuedTokenServiceCredential.CertificateValidationMode%2A> en uno de los valores de enumeración <xref:System.ServiceModel.Security.X509CertificateValidationMode>. Esto solo se puede hacer en código. De manera predeterminada, es <xref:System.IdentityModel.Selectors.X509CertificateValidator.ChainTrust%2A>.  
  
5. Si la propiedad <xref:System.ServiceModel.Security.IssuedTokenServiceCredential.CertificateValidationMode%2A> está establecida en <xref:System.ServiceModel.Security.X509CertificateValidationMode.Custom>, asigne a continuación una instancia de la clase personalizada <xref:System.IdentityModel.Selectors.X509CertificateValidator> a la propiedad <xref:System.ServiceModel.Security.X509ServiceCertificateAuthentication.CustomCertificateValidator%2A>.  
  
6. Si <xref:System.ServiceModel.Security.IssuedTokenServiceCredential.CertificateValidationMode%2A> está definido en `ChainTrust` o `PeerOrChainTrust`, defina la propiedad <xref:System.ServiceModel.Security.IssuedTokenServiceCredential.RevocationMode%2A> en un valor apropiado de la enumeración <xref:System.Security.Cryptography.X509Certificates.X509RevocationMode>. Tenga en cuenta que el modo de revocación no se utiliza en `PeerTrust` ni en los modos de validación `Custom`.  
  
7. Si es necesario, asigne una instancia de una clase <xref:System.IdentityModel.Tokens.SamlSerializer> personalizada a la propiedad <xref:System.ServiceModel.Security.IssuedTokenServiceCredential.SamlSerializer%2A>. Se necesita un serializador del Lenguaje de marcado de aserción de seguridad (SAML) personalizado, por ejemplo, para analizar las aserciones de SAML personalizadas.  
  
### <a name="to-set-the-properties-of-issuedtokenservicecredential-in-configuration"></a>Para establecer las propiedades de IssuedTokenServiceCredential en la configuración  
  
1. Crear un `<issuedTokenAuthentication>` como elemento secundario de un <`serviceCredentials`> elemento.  
  
2. Establecer el `allowUntrustedRsaIssuers` atributo de la `<issuedTokenAuthentication>` elemento `true` si autentica un token emitido automáticamente, como un [!INCLUDE[infocard](../../../../includes/infocard-md.md)] tarjeta.  
  
3. Cree un elemento `<knownCertificates>` como elemento secundario del elemento de `<issuedTokenAuthentication>`.  
  
4. Cree cero o más elementos `<add>` como elementos secundarios del elemento`<knownCertificates>`y especifique cómo buscar el certificado mediante los atributos`storeLocation`,`storeName`, `x509FindType` y `findValue`.  
  
5. Si es necesario, establezca el `samlSerializer` atributo de la <`issuedTokenAuthentication`> elemento para el nombre de tipo de personalizado <xref:System.IdentityModel.Tokens.SamlSerializer> clase.  
  
## <a name="example"></a>Ejemplo  
 El siguiente ejemplo define las propiedades de un <xref:System.ServiceModel.Security.IssuedTokenServiceCredential> en el código.  
  
 [!code-csharp[C_FederatedService#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_federatedservice/cs/source.cs#2)]
 [!code-vb[C_FederatedService#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_federatedservice/vb/source.vb#2)]  
  
 Para que un servicio federado autentique un cliente, debe cumplirse lo siguiente sobre el token emitido:  
  
-   Cuando la firma digital del token emitido utiliza un identificador de clave de seguridad de RSA, la propiedad <xref:System.ServiceModel.Security.IssuedTokenServiceCredential.AllowUntrustedRsaIssuers%2A> debe ser `true`.  
  
-   Cuando la firma del token emitido utiliza un número de serie de emisor de X.509, un identificador de clave de sujeto (SKI) de X.509 o un identificador de seguridad de huella digital de X.509, un certificado debe firmar el token emitido en la colección devuelta por la propiedad <xref:System.ServiceModel.Security.IssuedTokenServiceCredential.KnownCertificates%2A> de la clase <xref:System.ServiceModel.Security.IssuedTokenServiceCredential>.  
  
-   Cuando se firma el token emitido utilizando un certificado X.509, el certificado debe validarse por la semántica especificada por el valor de la propiedad <xref:System.ServiceModel.Security.X509ServiceCertificateAuthentication.CertificateValidationMode%2A>, sin tener en cuenta si el certificado se envió al usuario de confianza como <xref:System.IdentityModel.Tokens.X509RawDataKeyIdentifierClause> o se obtuvo de la propiedad <xref:System.ServiceModel.Security.IssuedTokenServiceCredential.KnownCertificates%2A>. Para obtener más información acerca de la validación del certificado X.509, consulte [trabajar con certificados](../../../../docs/framework/wcf/feature-details/working-with-certificates.md).  
  
 Por ejemplo, establecer <xref:System.ServiceModel.Security.IssuedTokenServiceCredential.CertificateValidationMode%2A> en <xref:System.ServiceModel.Security.X509CertificateValidationMode.PeerTrust> autenticaría cualquier token emitido cuyo certificado de firma esté en el almacén de certificados `TrustedPeople`. En ese caso, defina la propiedad <xref:System.ServiceModel.Security.IssuedTokenServiceCredential.TrustedStoreLocation%2A> en <xref:System.Security.Cryptography.X509Certificates.StoreLocation.CurrentUser> o <xref:System.Security.Cryptography.X509Certificates.StoreLocation.LocalMachine>. Puede seleccionar otros modos, incluidos <xref:System.ServiceModel.Security.X509CertificateValidationMode.Custom>. Cuando `Custom` está seleccionado, debe asignar una instancia de la clase <xref:System.IdentityModel.Selectors.X509CertificateValidator> a la propiedad <xref:System.ServiceModel.Security.IssuedTokenServiceCredential.CustomCertificateValidator%2A>. El validador personalizado puede validar los certificados utilizando cualquier criterio que le guste. Para obtener más información, vea [Cómo: Crear un servicio que emplee un validador de certificado personalizado](../../../../docs/framework/wcf/extending/how-to-create-a-service-that-employs-a-custom-certificate-validator.md).  
  
## <a name="see-also"></a>Vea también

- [Federación](../../../../docs/framework/wcf/feature-details/federation.md)
- [Federación y confianza](../../../../docs/framework/wcf/feature-details/federation-and-trust.md)
- [Ejemplo de federación](../../../../docs/framework/wcf/samples/federation-sample.md)
- [Cómo: Deshabilitar las sesiones seguras en WSFederationHttpBinding](../../../../docs/framework/wcf/feature-details/how-to-disable-secure-sessions-on-a-wsfederationhttpbinding.md)
- [Cómo: Create a WSFederationHttpBinding](../../../../docs/framework/wcf/feature-details/how-to-create-a-wsfederationhttpbinding.md)
- [Cómo: Crear a un cliente federado](../../../../docs/framework/wcf/feature-details/how-to-create-a-federated-client.md)
- [Trabajo con certificados](../../../../docs/framework/wcf/feature-details/working-with-certificates.md)
- [Modos de autenticación de SecurityBindingElement](../../../../docs/framework/wcf/feature-details/securitybindingelement-authentication-modes.md)
