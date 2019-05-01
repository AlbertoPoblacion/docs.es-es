---
title: Procedimiento para establecer una confirmación de firma
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- signature confirmation
- WCF, security
ms.assetid: 2424c137-c7c2-4aa9-8d5d-a066e12fefda
ms.openlocfilehash: 56e8720a6130d2908fbfb83bd243a54fae9a2406
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61972931"
---
# <a name="how-to-set-up-a-signature-confirmation"></a>Procedimiento para establecer una confirmación de firma
*Confirmación de firma* es un mecanismo para un iniciador de mensaje para asegurarse de que se generó una respuesta recibida en respuesta al mensaje original del remitente. La confirmación de la firma se define en la especificación WS-Security 1.1. Si un extremo admite WS-Security 1.0, no puede utilizar la confirmación de firma.  
  
 Los procedimientos siguientes especifican cómo habilitar la confirmación de firma mediante un <xref:System.ServiceModel.Channels.AsymmetricSecurityBindingElement>. Puede utilizar el mismo procedimiento con <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement>. El procedimiento se basa en los pasos básicos que se encuentra en [Cómo: Crear un enlace personalizado mediante SecurityBindingElement](../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md).  
  
### <a name="to-enable-signature-confirmation-in-code"></a>Para habilitar la confirmación de firma en código  
  
1. Cree una instancia de la clase <xref:System.ServiceModel.Channels.BindingElementCollection>.  
  
2. Cree una instancia de la <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement> clase.  
  
3. Establezca <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement.RequireSignatureConfirmation%2A> en `true`.  
  
4. Agregue el elemento de seguridad a la colección de enlaces.  
  
5. Crear un enlace personalizado, como se especifica en [Cómo: Crear un enlace personalizado mediante SecurityBindingElement](../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md).  
  
### <a name="to-enable-signature-confirmation-in-configuration"></a>Para habilitar la confirmación de firma en configuración  
  
1. Agregue un elemento `<customBinding>` a la sección`<bindings>` del archivo de configuración.  
  
2. Agregue un elemento `<binding>` y establezca el atributo de nombre en un valor adecuado.  
  
3. Agregue un elemento de codificación adecuado. El siguiente ejemplo agrega un elemento `<TextMessageEncoding>`.  
  
4. Agregue un elemento secundario `<security>` y establezca el atributo`requireSignatureConfirmation` en`true`.  
  
5. Opcional. Para habilitar la confirmación de firma durante el arranque, agregue un [ \<secureConversationBootstrap >](../../../../docs/framework/configure-apps/file-schema/wcf/secureconversationbootstrap.md) elemento secundario y establezca el `equireSignatureConfirmation` atributo `true`.  
  
6. Agregue un elemento de transporte adecuado. En el ejemplo siguiente se agrega un [ \<httpTransport >](../../../../docs/framework/configure-apps/file-schema/wcf/httptransport.md):  
  
    ```xml  
    <bindings>  
      <customBinding>  
        <binding name="SignatureConfirmationBinding">  
          <security requireSignatureConfirmation="true">  
            <secureConversationBootstrap requireSignatureConfirmation="true" />  
              </security>  
           <textMessageEncoding />  
             <httpTransport />  
        </binding>  
      </customBinding>  
    </bindings>  
    ```  
  
## <a name="example"></a>Ejemplo  
 El siguiente código crea una instancia del <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement> y establece la propiedad <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement.RequireSignatureConfirmation%2A> en `true`. Observe que este ejemplo no utiliza el elemento `<secureConversationBootstrap>` mostrado en el ejemplo anterior. Este ejemplo muestra la confirmación de firma al utilizar un token de Windows (protocolo Kerberos). En este caso, la firma del cliente se devuelve en todas las respuestas del servicio y es confirmada por el cliente.  
  
 [!code-csharp[c_SignatureConfirmation#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_signatureconfirmation/cs/source.cs#1)]
 [!code-vb[c_SignatureConfirmation#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_signatureconfirmation/vb/source.vb#1)]  
  
## <a name="see-also"></a>Vea también

- <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement>
- <xref:System.ServiceModel.Channels.AsymmetricSecurityBindingElement>
- <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateMutualCertificateBindingElement%2A>
- [Cómo: Crear un enlace personalizado mediante SecurityBindingElement](../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md)
- [Cómo: Crear un SecurityBindingElement para un modo de autenticación especificado](../../../../docs/framework/wcf/feature-details/how-to-create-a-securitybindingelement-for-a-specified-authentication-mode.md)
