---
title: Procedimiento para crear un WSFederationHttpBinding
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF, federation
- federation
ms.assetid: e54897d7-aa6c-46ec-a278-b2430c8c2e10
ms.openlocfilehash: 16b93126157ff129d5e0b815bc951873e7fa760d
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61778357"
---
# <a name="how-to-create-a-wsfederationhttpbinding"></a>Procedimiento para crear un WSFederationHttpBinding

En Windows Communication Foundation (WCF), el <xref:System.ServiceModel.WSFederationHttpBinding> clase ([\<wsFederationHttpBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/wsfederationhttpbinding.md) en configuración) proporciona un mecanismo para exponer un servicio federado. Es decir, un servicio que exige a los clientes su autenticación mediante un token de seguridad emitido por un servicio de token de seguridad. Este tema muestra cómo configurar un <xref:System.ServiceModel.WSFederationHttpBinding> tanto en el código y como en la configuración. Una vez creado el enlace, puede configurar un punto de conexión para que utilice dicho enlace.

 A continuación se describen los pasos básicos:

1. Seleccione un modo de seguridad. <xref:System.ServiceModel.WSFederationHttpBinding> admite `Message`, que proporciona seguridad global en el nivel de mensaje, incluso a través de múltiples saltos, y `TransportWithMessageCredential`, que ofrece el mejor rendimiento para los casos en los que el cliente y el servicio pueden realizar una conexión directa sobre HTTPS.

    > [!NOTE]
    > <xref:System.ServiceModel.WSFederationHttpBinding> también admite `None` como modo de seguridad. Este modo no es seguro y se ofrece solo para fines de depuración. Si un extremo de servicio se implementa con un <xref:System.ServiceModel.WSFederationHttpBinding> con su modo de seguridad establecido en `None`, el enlace de cliente resultante (generado por el [ServiceModel Metadata Utility Tool (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)) es un <xref:System.ServiceModel.WSHttpBinding> con un modo de seguridad de `None`.

     A diferencia de otros enlaces proporcionados por el sistema, no es necesario seleccionar un tipo de credencial de cliente cuando se utiliza `WSFederationHttpBinding`. Esto es porque el tipo de credenciales de cliente siempre es un token emitido. WCF adquiere un token de un emisor especificado y lo presenta al servicio para autenticar al cliente.

2. En clientes federados, se establece la propiedad <xref:System.ServiceModel.FederatedMessageSecurityOverHttp.IssuerAddress%2A> para la dirección URL del servicio de token de seguridad. Establezca <xref:System.ServiceModel.FederatedMessageSecurityOverHttp.IssuerBinding%2A> como el enlace utilizado para comunicar con el servicio de token de seguridad.

3. Opcional. Establezca la propiedad <xref:System.ServiceModel.FederatedMessageSecurityOverHttp.IssuedTokenType%2A> en el Identificador uniforme de recursos (URI) de un tipo de token. En servicios federados, especifique el tipo de token que el servicio espera. En clientes federados, especifique el tipo de token que el cliente solicita al servicio de token de seguridad.

     Si no se especifica ningún tipo de token, los clientes generan las solicitudes de tokens de seguridad (RST) de WS-Trust sin un URI del tipo de token, y los servicios asumen que la autenticación del cliente se realiza utilizando, de manera predeterminada, un token de Lenguaje de marcado de aserción de seguridad (SAML) 1.1.

     El URI para un token SAML 1.1 es `http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV1.1`.

4. Opcional. En servicios federados, establezca la propiedad <xref:System.ServiceModel.FederatedMessageSecurityOverHttp.IssuerMetadataAddress%2A> como la dirección URL de los metadatos de un servicio de token de seguridad. Si el servicio está configurado para publicar metadatos, el extremo de los metadatos permite a los clientes del servicio seleccionar un par enlace/extremo adecuado. Para obtener más información acerca de la publicación de metadatos, vea [la publicación de metadatos](publishing-metadata.md).

 También pueden establecerse otras propiedades, incluidos el tipo de clave utilizado como clave de prueba en el token emitido, el conjunto de algoritmos utilizado entre el cliente y el servicio, si negociar o especificar explícitamente la credencial del servicio, cualquier demanda concreta que el servicio espera que este contenido en el token emitido, y cualquier elemento XML adicional que deba agregarse a la solicitud que el cliente envía al servicio de token de seguridad.

> [!NOTE]
>  La propiedad `NegotiateServiceCredential` es relevante únicamente cuando `SecurityMode` se establece como `Message`. Si `SecurityMode` se establece como `TransportWithMessageCredential`, se omite la propiedad `NegotiateServiceCredential`.

## <a name="to-configure-a-wsfederationhttpbinding-in-code"></a>Para configurar un WSFederationHttpBinding en código

1. Cree una instancia de <xref:System.ServiceModel.WSFederationHttpBinding>.

2. Establezca la propiedad <xref:System.ServiceModel.WSFederationHttpSecurity.Mode%2A> como <xref:System.ServiceModel.WSFederationHttpSecurityMode> o <xref:System.ServiceModel.WSFederationHttpSecurityMode.Message>, según se requiera. Si un conjunto de algoritmos distinto <xref:System.ServiceModel.Security.SecurityAlgorithmSuite.Basic256%2A> es necesario, establezca el <xref:System.ServiceModel.FederatedMessageSecurityOverHttp.AlgorithmSuite%2A> propiedad a un valor tomado de <xref:System.ServiceModel.Security.SecurityAlgorithmSuite>.

3. Establezca la propiedad <xref:System.ServiceModel.FederatedMessageSecurityOverHttp.NegotiateServiceCredential%2A> según corresponda.

4. Establecer el <xref:System.ServiceModel.FederatedMessageSecurityOverHttp.IssuedKeyType%2A> propiedad <xref:System.IdentityModel.Tokens.SecurityKeyType> `SymmetricKey` o.`AsymmetricKey` según sea necesario.

5. Establezca un valor adecuado para la propiedad <xref:System.ServiceModel.FederatedMessageSecurityOverHttp.IssuedTokenType%2A>. Si se establece ningún valor, WCF toma como predeterminado `http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV1.1`, lo que indica tokens SAML 1.1.

6. Obligatorio en el cliente si no se especifica ningún emisor local; opcional en el servicio. Cree <xref:System.ServiceModel.EndpointAddress> que contenga la dirección e información de identidad del servicio de token de seguridad, y asigne la instancia <xref:System.ServiceModel.EndpointAddress> a la propiedad <xref:System.ServiceModel.FederatedMessageSecurityOverHttp.IssuerAddress%2A>.

7. Obligatorio en el cliente si no se especifica ningún emisor local; no se utiliza en el servicio. Crear un <xref:System.ServiceModel.Channels.Binding> para el `SecurityTokenService` y asignar la <xref:System.ServiceModel.Channels.Binding> de instancia para el <xref:System.ServiceModel.FederatedMessageSecurityOverHttp.IssuerBinding%2A> propiedad.

8. No se utiliza en el cliente; opcional en el servicio. Cree una instancia <xref:System.ServiceModel.EndpointAddress> para los metadatos del servicio de token de seguridad, y asígnelo a la propiedad `IssuerMetadataAddress`.

9. Opcional en el cliente y el servicio. Cree y agregue una o más instancias <xref:System.ServiceModel.Security.Tokens.ClaimTypeRequirement> a la colección devuelta por la propiedad <xref:System.ServiceModel.FederatedMessageSecurityOverHttp.ClaimTypeRequirements%2A>.

10. Opcional en el cliente y el servicio. Cree y agregue una o más instancias <xref:System.Xml.XmlElement> a la colección devuelta por la propiedad <xref:System.ServiceModel.FederatedMessageSecurityOverHttp.TokenRequestParameters%2A>.

## <a name="to-create-a-federated-endpoint-in-configuration"></a>Para crear un punto de conexión federado en la configuración

1. Crear un [ \<wsFederationHttpBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/wsfederationhttpbinding.md) como elemento secundario de la [ \<enlaces >](../../../../docs/framework/configure-apps/file-schema/wcf/bindings.md) elemento en el archivo de configuración de la aplicación.

2. Crear un [ \<enlace >](../../../../docs/framework/misc/binding.md) como elemento secundario de [ \<wsFederationHttpBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/wsfederationhttpbinding.md) y establezca el `name` atributo en un valor adecuado.

3. Crear un `<security>` como elemento secundario de la [ \<enlace >](../../../../docs/framework/misc/binding.md) elemento.

4. Establezca el atributo `mode` del elemento `<security>``TransportWithMessageCredential` con un valor de `Message` o , como se requiera.

5. Cree un elemento `<message>` como elemento secundario del elemento de `<security>`.

6. Opcional. Establezca el atributo `algorithmSuite` del elemento `<message>` con un valor adecuado. De manera predeterminada, es `Basic256`.

7. Opcional. Si se requiere una clave de prueba asimétrica, establezca el atributo `issuedKeyType` del elemento `<message>`AsymmetricKey como`AsymmetricKey`. De manera predeterminada, es `SymmetricKey`.

8. Opcional. Establezca el atributo `issuedTokenType` en el elemento `<message>`.

9. Obligatorio en el cliente si no se especifica ningún emisor local; opcional en el servicio. Cree un elemento `<issuer>` como elemento secundario del elemento `<message>`.

10. Establezca el atributo `address` como el elemento `<issuer>`, y especifique la dirección en la que el servicio de token de seguridad acepta las solicitudes de token.

11. Opcional. Agregue un elemento secundario `<identity>` y especifique la identidad del servicio de token de seguridad

12. Para obtener más información, consulte [autenticación e identidad de servicio](service-identity-and-authentication.md).

13. Obligatorio en el cliente si no se especifica ningún emisor local; no se utiliza en el servicio. Crear un [ \<enlace >](../../../../docs/framework/misc/binding.md) elemento en la sección de enlaces que se puede usar para comunicarse con el servicio de token de seguridad. Para obtener más información acerca de cómo crear un enlace, consulte [Cómo: Especificar un enlace de servicio en la configuración](../../../../docs/framework/wcf/how-to-specify-a-service-binding-in-configuration.md).

14. Especifique el enlace creado en el paso anterior estableciendo los atributos `binding` y `bindingConfiguration` del elemento `<issuer>`.

15. No se utiliza en el cliente; opcional en el servicio. Crear un `<issuerMetadata>` como elemento secundario de la <`message`> elemento. A continuación, en un atributo `address` del elemento `<issuerMetadata>`, especifique la dirección en la que el servicio de token de seguridad publicará sus metadatos. De manera opcional, agregue un elemento secundario `<identity>` y especifique la identidad del servicio de token de seguridad

16. Opcional en el cliente y el servicio. Agregue un elemento `<claimTypeRequirements>` como elemento secundario del elemento `<message>`. Especificar demandas necesarias y opcionales que se basa el servicio agregando [ \<Agregar >](../../../../docs/framework/configure-apps/file-schema/wcf/add-of-claimtyperequirements.md) elementos a la `<claimTypeRequirements>` tipo de elemento y especifica la notificación con el `claimType` atributo. Especifique si una notificación determinada es obligatoria u opcional estableciendo el atributo `isOptional`.

## <a name="example"></a>Ejemplo

El ejemplo de código siguiente muestra el código para configurar `WSFederationHttpBinding` de manera imperativa.

[!code-csharp[c_FederationBinding#2](~/samples/snippets/csharp/VS_Snippets_CFX/c_federationbinding/cs/source.cs#2)]
[!code-vb[c_FederationBinding#2](~/samples/snippets/visualbasic/VS_Snippets_CFX/c_federationbinding/vb/source.vb#2)]

## <a name="see-also"></a>Vea también

- [Federación](federation.md)
- [Ejemplo de federación](../../../../docs/framework/wcf/samples/federation-sample.md)
- [Cómo: Deshabilitar las sesiones seguras en WSFederationHttpBinding](how-to-disable-secure-sessions-on-a-wsfederationhttpbinding.md)