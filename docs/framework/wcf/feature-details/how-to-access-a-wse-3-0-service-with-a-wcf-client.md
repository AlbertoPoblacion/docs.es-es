---
title: Procedimiento Obtener acceso a un WSE 3.0 servicio con un cliente WCF
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 1f9bcd9b-8f8f-47fa-8f1e-0d47236eb800
ms.openlocfilehash: 83507a95dbc4bc7499b94a516f569703f21a2726
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59341067"
---
# <a name="how-to-access-a-wse-30-service-with-a-wcf-client"></a>Procedimiento Obtener acceso a un WSE 3.0 servicio con un cliente WCF
Los clientes de Windows Communication Foundation (WCF) son compatibles con Web Services Enhancements (WSE) 3.0 en el nivel de conexión de servicios de Microsoft .NET cuando se configuran los clientes de WCF para usar la versión de agosto de 2004 de la especificación WS-Addressing. Sin embargo, los servicios WSE 3.0 no admiten el protocolo de intercambio (MEX) de metadatos, así que cuando se usa el [ServiceModel Metadata Utility Tool (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) para crear una clase de cliente WCF, la configuración de seguridad no se aplica a generado Cliente WCF. Por lo tanto, debe especificar la configuración de seguridad que el servicio de WSE 3.0 requiere una vez generado el cliente de WCF.  
  
 Puede aplicar esta configuración de seguridad mediante un enlace personalizado para tener en cuenta los requisitos del servicio WSE 3.0 y los requisitos interoperables entre un servicio de WSE 3.0 y un cliente de WCF. Estos requisitos de interoperabilidad incluyen el uso mencionado anteriormente de agosto de 2004 de la especificación WS-Addressing y la protección predeterminada de mensajes de WSE 3.0 de <xref:System.ServiceModel.Security.MessageProtectionOrder.SignBeforeEncrypt>. La protección predeterminada de mensajes de WCF es <xref:System.ServiceModel.Security.MessageProtectionOrder.SignBeforeEncryptAndEncryptSignature>. En este tema se detalla cómo crear un enlace WCF que interopere con un servicio de WSE 3.0. WCF también proporciona un ejemplo que incorpora este enlace. Para obtener más información acerca de este ejemplo, vea [interoperar con servicios Web ASMX](../../../../docs/framework/wcf/samples/interoperating-with-asmx-web-services.md).  
  
### <a name="to-access-a-wse-30-web-service-with-a-wcf-client"></a>Obtener acceso al servicio Web WSE 3.0 con un cliente WCF  
  
1. Ejecute el [ServiceModel Metadata Utility Tool (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) para crear un cliente WCF para el servicio Web WSE 3.0.  
  
     Para un servicio Web WSE 3.0, se crea un cliente de WCF. Dado que WSE 3.0 no admite el protocolo MEX, no se puede utilizar la herramienta para recuperar los requisitos de seguridad del Servicio Web. El desarrollador de aplicaciones debe agregar la configuración de seguridad del cliente.  
  
     Para obtener más información acerca de cómo crear un cliente de WCF, vea el [Cómo: Crear un cliente](../../../../docs/framework/wcf/how-to-create-a-wcf-client.md).  
  
2. Cree una clase que represente un enlace que puede comunicarse con los servicios Web WSE 3.0.  
  
     La clase siguiente forma parte de la [interoperar con WSE](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms752257%28v=vs.90%29) ejemplo:  
  
    1.  Cree una clase que se derive de la clase <xref:System.ServiceModel.Channels.Binding>.  
  
         En el siguiente ejemplo de código se crea una clase denominada `WseHttpBinding`, que se deriva de la clase <xref:System.ServiceModel.Channels.Binding>.  
  
         [!code-csharp[c_WCFClientToWSEService#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_wcfclienttowseservice/cs/wsehttpbinding.cs#1)]
         [!code-vb[c_WCFClientToWSEService#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_wcfclienttowseservice/vb/wsehttpbinding.vb#1)]  
  
    2.  Agregue propiedades a la clase que especifiquen la aserción de llave en mano usada por el servicio WSE, si se requieren las claves derivadas, si se utilizan sesiones seguras, si se requieren confirmaciones de firmas, y la configuración de protección de mensajes. En WSE 3.0, una aserción de llave en mano especifica los requisitos de seguridad para un cliente o servicio Web, similar al modo de autenticación de un enlace en WCF.  
  
         El ejemplo de código siguiente define las propiedades `SecurityAssertion`, `RequireDerivedKeys`, `EstablishSecurityContext` y `MessageProtectionOrder` que especifican la aserción de llave en mano de WSE, si se requieren claves derivadas, si se usan sesiones seguras, si se requieren confirmaciones de firmas y la configuración de protección de mensajes, respectivamente.  
  
         [!code-csharp[c_WCFClientToWSEService#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_wcfclienttowseservice/cs/wsehttpbinding.cs#3)]
         [!code-vb[c_WCFClientToWSEService#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_wcfclienttowseservice/vb/wsehttpbinding.vb#3)]  
  
    3.  Anule el método <xref:System.ServiceModel.Channels.Binding.CreateBindingElements%2A> para definir las propiedades de enlace.  
  
         El ejemplo de código siguiente especifica el transporte, codificación de mensajes y configuración de protección de mensajes obteniendo los valores de las propiedades `SecurityAssertion` y `MessageProtectionOrder`.  
  
         [!code-csharp[c_WCFClientToWSEService#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_wcfclienttowseservice/cs/wsehttpbinding.cs#2)]
         [!code-vb[c_WCFClientToWSEService#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_wcfclienttowseservice/vb/wsehttpbinding.vb#2)]  
  
3. En el código de la aplicación cliente, agregue el código para definir las propiedades de enlace.  
  
     El ejemplo de código siguiente especifica que el cliente de WCF debe usar autenticación y protección de mensajes definidos por el WSE 3.0 `AnonymousForCertificate` aserción de seguridad inmediata. Además, se requieren sesiones seguras y claves derivadas.  
  
     [!code-csharp[c_WCFClientToWSEService#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_wcfclienttowseservice/cs/client.cs#4)]
     [!code-vb[c_WCFClientToWSEService#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_wcfclienttowseservice/vb/client.vb#4)]  
  
## <a name="example"></a>Ejemplo  
 El ejemplo de código siguiente define un enlace personalizado que expone propiedades que corresponden a las propiedades de una aserción de seguridad de llave en mano WSE 3.0. Ese enlace personalizado, que se denomina `WseHttpBinding`, a continuación, se usa para especificar las propiedades de enlace para un cliente WCF que se comunica con el ejemplo de tutorial rápido de WSSecurityAnonymous WSE 3.0.  

## <a name="see-also"></a>Vea también

- <xref:System.ServiceModel.Channels.Binding>
- [Interoperar con WSE](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms752257%28v=vs.90%29)
