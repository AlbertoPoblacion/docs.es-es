---
title: <scopedCertificates> Elemento
ms.date: 03/30/2017
ms.assetid: c7b6fc35-d4b2-4c18-98bd-83e09591f1d3
ms.openlocfilehash: 73e78a6ca27ed45e1eadc7121987b75f79bc6aa5
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2019
ms.locfileid: "59145205"
---
# <a name="scopedcertificates-element"></a>\<scopedCertificates > elemento
Representa una colección de certificados X.509 proporcionada por servicios concretos (con ámbito) para la autenticación. Esta colección se utiliza normalmente para especificar los certificados de servicio para los servicios de token de seguridad en un escenario asociado externo.  
  
 \<system.ServiceModel>  
\<comportamientos >  
sección endpointBehaviors  
\<comportamiento >  
\<clientCredentials>  
\<serviceCertificate>  
\<scopedCertificates > elemento  
\<Agregar > elemento para \<scopedCertificates >  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
<scopedCertificates>
  <add findValue="String"
       storeLocation="CurrentUser/LocalMachine"
       storeName=" CurrentUser/LocalMachine"
       targetUri="string"
       x509Type="FindByThumbprint/FindBySubjectName/FindBySubjectDistinguishedName/FindByIssuerName/FindByIssuerDistinguishedName/FindBySerialNumber/FindByTimeValid/FindByTimeNotYetValid/FindBySerialNumber/FindByTimeExpired/FindByTemplateName/FindByApplicationPolicy/FindByCertificatePolicy/FindByExtension/FindByKeyUsage/FindBySubjectKeyIdentifier" />
</scopedCertificates>
```  
  
## <a name="attributes-and-elements"></a>Atributos y elementos  
 En las siguientes secciones se describen los atributos, los elementos secundarios y los elementos primarios.  
  
### <a name="attributes"></a>Atributos  
 Ninguno.  
  
### <a name="child-elements"></a>Elementos secundarios  
  
|Elemento|Descripción|  
|-------------|-----------------|  
|[\<add>](../../../../../docs/framework/configure-apps/file-schema/wcf/add-of-scopedcertificates-element.md)|Agrega un certificado X.509 a la colección de certificados con ámbito.|  
  
### <a name="parent-elements"></a>Elementos primarios  
  
|Elemento|Descripción|  
|-------------|-----------------|  
|[\<serviceCertificate>](../../../../../docs/framework/configure-apps/file-schema/wcf/servicecertificate-of-servicecredentials.md)|Especifica el certificado que se va a utilizar al autenticar un servicio al cliente.|  
  
## <a name="remarks"></a>Comentarios  
 Esta colección le permite al cliente configurar los certificados de servicio que se van a utilizar basándose en la dirección URL del servicio con el que se comunica. Esto es especialmente útil en escenarios del token emitidos donde un cliente puede estar comunicándose con varios servicios (el servicio final, así como los servicios del token de seguridad intermediarios). Para los enlaces que utilizan la seguridad del mensaje basada en certificados, este certificado se utiliza para cifrar los mensajes del servicio y se espera que sea utilizado por el servicio para firmar las respuestas para el cliente.  
  
 Si un enlace requiere un certificado para el servicio y no se encuentra ningún certificado concreto para la dirección URL del servicio en ScopedCertificates, se utilizará el certificado predeterminado.  
  
 Para obtener más información, vea la sección "Certificados con ámbito" de [Cómo: Crear un cliente federado](../../../../../docs/framework/wcf/feature-details/how-to-create-a-federated-client.md).  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente especifica un certificado de servicio para el cliente que se usará al comunicarse con puntos de conexión cuyo nombre de dominio es `http://www.contoso.com` a través del protocolo HTTP.  
  
```xml  
<serviceCertificate>
  <scopedCertificates>
    <add targetUri="http://www.contoso.com"
         findValue="www.contoso.com"
         storeLocation="LocalMachine"
         storeName="Root"
         x509FindType="FindByIssuerName" />
  </scopedCertificates>
</serviceCertificate>
```  
  
## <a name="see-also"></a>Vea también

- <xref:System.ServiceModel.Configuration.X509RecipientCertificateClientElement.ScopedCertificates%2A>
- <xref:System.ServiceModel.Configuration.X509ScopedServiceCertificateElementCollection>
- <xref:System.ServiceModel.Configuration.X509ScopedServiceCertificateElement>
- <xref:System.ServiceModel.Security.X509CertificateRecipientClientCredential>
- <xref:System.ServiceModel.Security.X509CertificateRecipientClientCredential.ScopedCertificates%2A>
- [Trabajar con certificados](../../../../../docs/framework/wcf/feature-details/working-with-certificates.md)
- [Filtrar para crear un cliente federado](../../../../../docs/framework/wcf/feature-details/how-to-create-a-federated-client.md)
- [\<add>](../../../../../docs/framework/configure-apps/file-schema/wcf/add-of-scopedcertificates-element.md)
- [Protección de clientes](../../../../../docs/framework/wcf/securing-clients.md)
- [Protección de servicios y clientes](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)
