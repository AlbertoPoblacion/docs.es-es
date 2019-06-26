---
title: Información general de la seguridad del transporte
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 00959326-aa9d-44d0-af61-54933d4adc7f
ms.openlocfilehash: 450d10c0356a8c22741275e2c1e1a842c1fd4627
ms.sourcegitcommit: bab17fd81bab7886449217356084bf4881d6e7c8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2019
ms.locfileid: "67402050"
---
# <a name="transport-security-overview"></a>Información general de la seguridad del transporte
Mecanismos de seguridad de transporte en Windows Communication Foundation (WCF) dependen el enlace y el transporte que se va a usar. Por ejemplo, al utilizar la clase <xref:System.ServiceModel.WSHttpBinding>, el transporte es HTTP y el mecanismo principal para garantizar el transporte es Capa de sockets seguros (SSL) sobre HTTP, normalmente denominado HTTPS. En este tema se describe los mecanismos de seguridad de transporte principales utilizados en los enlaces proporcionados por el sistema WCF.  
  
> [!NOTE]
>  Cuando se usa la seguridad SSL con .NET Framework 3.5 y versiones posteriores, un cliente WCF utiliza tanto los certificados intermedios en su almacén de certificados y los certificados intermedios reciben durante la negociación de SSL para realizar la validación de la cadena de certificados en el servicio certificado. .NET Framework 3.0 solo usa los certificados intermedios instalados en el almacén de certificados local.  
  
> [!WARNING]
>  Cuando se utiliza la seguridad de transporte, puede sobrescribirse la propiedad <xref:System.Threading.Thread.CurrentPrincipal%2A?displayProperty=nameWithType>. Para evitar que esto suceda, establezca el <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior.PrincipalPermissionMode%2A?displayProperty=nameWithType> a <xref:System.ServiceModel.Description.PrincipalPermissionMode.None?displayProperty=nameWithType>. <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior> es un comportamiento de servicio que se puede establecer en la descripción del servicio.  
  
## <a name="basichttpbinding"></a>BasicHttpBinding  
 De manera predeterminada, la clase <xref:System.ServiceModel.BasicHttpBinding> no proporciona seguridad. Este enlace está diseñado para la interoperabilidad con proveedores de servicios Web que no implementan seguridad. Sin embargo, puede activar la seguridad definiendo la propiedad <xref:System.ServiceModel.BasicHttpSecurity.Mode%2A> en cualquier valor excepto <xref:System.ServiceModel.BasicHttpSecurityMode.None>. Para habilitar la seguridad del transporte, defina la propiedad en <xref:System.ServiceModel.BasicHttpSecurityMode.Transport>.  
  
### <a name="interoperation-with-iis"></a>Interoperación con IIS  
 La clase <xref:System.ServiceModel.BasicHttpBinding> se utiliza principalmente para interoperar con los servicios Web existentes e Internet Information Services (IIS) hospeda muchos de esos servicios. Por consiguiente, la seguridad en el transporte para este enlace está diseñada para la interoperación perfecta con sitios de IIS. Esto se realiza definiendo el modo de seguridad en <xref:System.ServiceModel.BasicHttpSecurityMode.Transport> y estableciendo a continuación el tipo de credencial del cliente. Los valores del tipo de la credencial se corresponden con los mecanismos de seguridad del directorio de IIS. El código siguiente muestra el modo que se ha establecido y el tipo de credencial definido en Windows. Puede utilizar esta configuración cuando el cliente y el servidor están en el mismo dominio de Windows.  
  
 [!code-csharp[c_ProgrammingSecurity#10](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_programmingsecurity/cs/source.cs#10)] 
 [!code-vb[c_ProgrammingSecurity#10](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_programmingsecurity/vb/source.vb#10)]  
  
 O bien, en la configuración:  
  
```xml  
<bindings>  
  <basicHttpBinding>  
    <binding name="SecurityByTransport">  
      <security mode="Transport">  
        <transport clientCredentialType="Windows" />  
       </security>  
     </binding>  
  </basicHttpBinding>  
</bindings>  
```  
  
 Las secciones siguientes tratan otros tipos de credenciales de clientes.  
  
#### <a name="basic"></a>Básico  
 Se corresponde con el método de autenticación básico de IIS. Cuando se utiliza este modo, el servidor IIS debe configurarse con cuentas de usuario de Windows y permisos de sistema de archivos NTFS adecuados. Para obtener más información acerca de IIS 6.0, consulte [Enabling Basic Authentication and Configuring the Realm Name](https://go.microsoft.com/fwlink/?LinkId=88592). Para obtener más información acerca de [!INCLUDE[iisver](../../../../includes/iisver-md.md)], consulte [IIS 7.0 Beta: Configurar la autenticación básica](https://go.microsoft.com/fwlink/?LinkId=88593).  
  
#### <a name="certificate"></a>Certificado  
 IIS tiene una opción para exigir a los clientes que inicien sesión con un certificado. La característica también le permite a IIS asignar un certificado de cliente a una cuenta de Windows. Para obtener más información acerca de IIS 6.0, consulte [Enabling Client Certificates in IIS 6.0](https://go.microsoft.com/fwlink/?LinkId=88594). Para obtener más información acerca de [!INCLUDE[iisver](../../../../includes/iisver-md.md)], consulte [IIS 7.0 Beta: Configuración de certificados de servidor en IIS 7.0](https://go.microsoft.com/fwlink/?LinkId=88595).  
  
#### <a name="digest"></a>Implícita  
 La autenticación implícita es similar a la autenticación básica, pero proporciona la ventaja de enviar las credenciales como un hash, en lugar de como texto no cifrado. Para obtener más información acerca de IIS 6.0, consulte [la autenticación implícita en IIS 6.0](https://go.microsoft.com/fwlink/?LinkID=88443). Para obtener más información acerca de [!INCLUDE[iisver](../../../../includes/iisver-md.md)], consulte [IIS 7.0 Beta: Configurar la autenticación implícita](https://go.microsoft.com/fwlink/?LinkId=88596).  
  
#### <a name="windows"></a>Windows  
 Esto se corresponde a la autenticación integrada de Windows en IIS. Cuando se establece en este valor, también se espera que el servidor exista en un dominio de Windows que utiliza el protocolo Kerberos como su controlador de dominio. Si el servidor no está en un dominio respaldado por Kerberos, o si se producen errores en el sistema Kerberos, puede utilizar el valor de NT LAN Manager (NTLM) descrito en la sección siguiente. Para obtener más información acerca de IIS 6.0, consulte [autenticación integrada de Windows en IIS 6.0](https://go.microsoft.com/fwlink/?LinkId=88597). Para obtener más información acerca de [!INCLUDE[iisver](../../../../includes/iisver-md.md)], consulte [IIS 7.0 Beta: Configuración de certificados de servidor en IIS 7.0](https://go.microsoft.com/fwlink/?LinkId=88595).  
  
#### <a name="ntlm"></a>NTLM  
 Esto permite al servidor usar NTLM para la autenticación si se produce un error en el protocolo Kerberos. Para obtener más información sobre cómo configurar IIS en IIS 6.0, consulte [forzar la autenticación NTLM](https://go.microsoft.com/fwlink/?LinkId=88598). Para [!INCLUDE[iisver](../../../../includes/iisver-md.md)], la autenticación de Windows incluye la autenticación NTLM. Para obtener más información, consulte [IIS 7.0 Beta: Configuración de certificados de servidor en IIS 7.0](https://go.microsoft.com/fwlink/?LinkID=88595).  
  
## <a name="wshttpbinding"></a>WsHttpBinding  
 La clase <xref:System.ServiceModel.WSHttpBinding> está diseñada para la interoperación con servicios que implementan las especificaciones de WS-*. La seguridad de transporte para este enlace es Capa de sockets seguros (SSL) sobre HTTP o HTTPS. Para crear una aplicación de WCF que usa SSL, utilice IIS para hospedar la aplicación. Alternativamente, si está creando una aplicación autohospedada, utilice la herramienta HttpCfg.exe para enlazar un certificado X.509 con un puerto concreto en un equipo. El número de puerto se especifica como parte de la aplicación de WCF como una dirección de punto de conexión. Al utilizar el modo de transporte, la dirección del extremo debe incluir el protocolo HTTPS o se producirá una excepción en el tiempo de ejecución. Para obtener más información, consulte [seguridad de transporte HTTP](../../../../docs/framework/wcf/feature-details/http-transport-security.md).  
  
 En el caso de la autenticación del cliente, defina la propiedad <xref:System.ServiceModel.HttpTransportSecurity.ClientCredentialType%2A> de la clase <xref:System.ServiceModel.HttpTransportSecurity> en uno de los valores de enumeración de <xref:System.ServiceModel.HttpClientCredentialType>. Los valores de enumeración son idénticos a los tipos de credencial de cliente para <xref:System.ServiceModel.BasicHttpBinding> y están diseñados para que se hospeden con servicios de IIS.  
  
 El ejemplo siguiente muestra el enlace que se va a usar con un tipo de credencial de cliente de Windows.  
  
 [!code-csharp[c_ProgrammingSecurity#11](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_programmingsecurity/cs/source.cs#11)]
 [!code-vb[c_ProgrammingSecurity#11](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_programmingsecurity/vb/source.vb#11)]  
  
## <a name="wsdualhttpbinding"></a>WSDualHttpBinding  
 Este enlace solo proporciona seguridad en el nivel de mensaje pero no seguridad en el nivel de transporte.  
  
## <a name="nettcpbinding"></a>NetTcpBinding  
 La clase <xref:System.ServiceModel.NetTcpBinding> usa TCP para el transporte del mensaje. Se proporciona seguridad para el modo de transporte al implementar Seguridad de la capa de transporte (TLS) sobre TCP. El sistema operativo proporciona la implementación de TLS.  
  
 También puede especificar el tipo de credencial del cliente estableciendo la propiedad <xref:System.ServiceModel.TcpTransportSecurity.ClientCredentialType%2A> de la clase <xref:System.ServiceModel.TcpTransportSecurity> en uno de los valores de la enumeración <xref:System.ServiceModel.TcpClientCredentialType>, tal y como se muestra en el código siguiente.  
  
 [!code-csharp[c_ProgrammingSecurity#12](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_programmingsecurity/cs/source.cs#12)]
 [!code-vb[c_ProgrammingSecurity#12](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_programmingsecurity/vb/source.vb#12)]  
  
#### <a name="client"></a>Cliente  
 En el cliente, debe especificar un certificado mediante el método <xref:System.ServiceModel.Security.X509CertificateInitiatorClientCredential.SetCertificate%2A> de la clase <xref:System.ServiceModel.Security.X509CertificateInitiatorClientCredential>.  
  
> [!NOTE]
>  Si está utilizando la seguridad de Windows, no se requiere un certificado.  
  
 El código siguiente usa la huella digital del certificado, que lo identifica de forma única. Para más información, consulte [Trabajar con certificados](../../../../docs/framework/wcf/feature-details/working-with-certificates.md).  
  
 [!code-csharp[c_ProgrammingSecurity#13](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_programmingsecurity/cs/source.cs#13)]
 [!code-vb[c_ProgrammingSecurity#13](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_programmingsecurity/vb/source.vb#13)]  
  
 Como alternativa, especifique el certificado en la configuración del cliente mediante un [ \<clientCredentials >](../../../../docs/framework/configure-apps/file-schema/wcf/clientcredentials.md) elemento en la sección de comportamientos.  
  
```xml  
<behaviors>  
  <behavior>  
   <clientCredentials>  
     <clientCertificate findValue= "101010101010101010101010101010000000000"   
      storeLocation="LocalMachine" storeName="My"   
      X509FindType="FindByThumbPrint"/>  
     </clientCertificate>  
   </clientCredentials>  
 </behavior>  
</behaviors>    
```  
  
## <a name="netnamedpipebinding"></a>NetNamedPipeBinding  
 La clase <xref:System.ServiceModel.NetNamedPipeBinding> está diseñada para la comunicación eficaz dentro de la máquina. Es decir, para los procesos que se ejecuten en el mismo equipo, aunque los canales de canalización con nombre se puedan crear entre dos equipos de la misma red. Este enlace solo proporciona la seguridad de nivel de transporte. Al crear aplicaciones mediante este enlace, las direcciones del punto de conexión deben incluir "net.pipe" como protocolo de la dirección del punto de conexión.  
  
## <a name="wsfederationhttpbinding"></a>WSFederationHttpBinding  
 Cuando se usa seguridad de transporte, este enlace usa SSL sobre HTTP, lo que se conoce como HTTPS con un token emitido (<xref:System.ServiceModel.WSFederationHttpSecurityMode.TransportWithMessageCredential>). Para obtener más información acerca de las aplicaciones de federación, consulte [federación y Tokens emitidos](../../../../docs/framework/wcf/feature-details/federation-and-issued-tokens.md).  
  
## <a name="netpeertcpbinding"></a>NetPeerTcpBinding  
 La clase <xref:System.ServiceModel.NetPeerTcpBinding> es un transporte seguro que está diseñado para la comunicación eficaz utilizando la característica de conexión de red de punto a punto. Tal y como indica el nombre de la clase y el enlace, TCP es el protocolo. Cuando el modo de seguridad se establece en Transporte, el enlace implementa TLS sobre TCP. Para obtener más información acerca de la característica punto a punto, vea [Peer-to-Peer Networking](../../../../docs/framework/wcf/feature-details/peer-to-peer-networking.md).  
  
## <a name="msmqintegrationbinding-and-netmsmqbinding"></a>MsmqIntegrationBinding y NetMsmqBinding  
 Para obtener una descripción completa de transporte, seguridad con Message Queue Server (anteriormente denominado MSMQ), consulte [proteger mensajes utilizando seguridad de transporte](../../../../docs/framework/wcf/feature-details/securing-messages-using-transport-security.md).  
  
## <a name="see-also"></a>Vea también

- [Programación de la seguridad de WCF](../../../../docs/framework/wcf/feature-details/programming-wcf-security.md)
