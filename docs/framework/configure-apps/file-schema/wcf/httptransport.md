---
title: <httpTransport>
ms.date: 03/30/2017
ms.assetid: 8b30c065-b32a-4fa3-8eb4-5537a9c6b897
ms.openlocfilehash: f529cd5290c74999a010381fadfb94ea9a4d515e
ms.sourcegitcommit: 3630c2515809e6f4b7dbb697a3354efec105a5cd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/25/2019
ms.locfileid: "58408943"
---
# <a name="httptransport"></a>\<httpTransport>
Especifica un transporte HTTP para transmitir los mensajes SOAP para un enlace personalizado.  
  
 \<system.serviceModel>  
\<bindings>  
\<customBinding>  
\<binding>  
\<httpTransport>  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
<httpTransport allowCookies="Boolean"
               authenticationScheme="Digest/Negotiate/Ntlm/Basic/Anonymous"
               bypassProxyOnLocal="Boolean"
               hostnameComparisonMode="StrongWildcard/Exact/WeakWildcard"
               keepAliveEnabled="Boolean"
               maxBufferSize="Integer"
               proxyAddress="Uri"
               proxyAuthenticationScheme="None/Digest/Negotiate/Ntlm/Basic/Anonymous"
               realm="String"
               transferMode="Buffered/Streamed/StreamedRequest/StreamedResponse"
               unsafeConnectionNtlmAuthentication="Boolean"
               useDefaultWebProxy="Boolean" />
```  
  
## <a name="attributes-and-elements"></a>Atributos y elementos  
 En las siguientes secciones se describen los atributos, los elementos secundarios y los elementos primarios.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descripción|  
|---------------|-----------------|  
|allowCookies|Un valor booleano que especifica si el cliente acepta las cookies y las propaga en solicitudes futuras. De manera predeterminada, es `false`.<br /><br /> Puede usar este atributo al interactuar con los servicios Web ASMX que utilizan cookies. De esta manera, puede estar seguro de que las cookies devueltas del servidor se copian automáticamente en todas las solicitudes de cliente futuras para ese servicio.|  
|authenticationScheme|Especifica el protocolo utilizado para autenticar solicitudes de cliente que son procesadas por un agente de escucha HTTP. Los valores válidos son los siguientes:<br /><br /> -Digest: Especifica la autenticación implícita.<br />-Negotiate: Negocia con el cliente para determinar el esquema de autenticación. Si cliente y el servidor son compatibles con Kerberos, se utiliza; de lo contrario, se utiliza NTLM.<br />-Ntlm: Especifica la autenticación de NTLM.<br />-Básicas: Especifica la autenticación básica.<br />-Anónimo: Especifica la autenticación anónima.<br /><br /> El valor predeterminado es Anonymous. Este atributo es del tipo <xref:System.Net.AuthenticationSchemes>. Se puede establecer este atributo sólo una vez.|  
|bypassProxyOnLocal|Valor de tipo booleano que indica si se omitirá el servidor proxy para las direcciones locales. De manera predeterminada, es `false`.<br /><br /> Una dirección local es la que está en la LAN local o intranet.<br /><br /> Windows Communication Foundation (WCF) siempre omite el proxy si la dirección del servicio comienza con `http://localhost`.<br /><br /> Debería utilizar el nombre del host en lugar del localhost si desea que los clientes pasen por un proxy al comunicarse con los servicios en el mismo equipo.|  
|hostnameComparisonMode|Especifica el modo de comparación de nombres de host HTTP usado para analizar los URI. Los valores válidos son<br /><br /> -StrongWildcard: ("+") coincide con todos los posibles nombres de host en el contexto de esquema especificado, puerto y URI relativo.<br />-Exact: ningún carácter comodín<br />-WeakWildcard: ("\*") coincide con el nombre de host de todas las posibles en el contexto de esquema especificado, puerto y URI relativo con los que no han coincidido explícitamente o a través del mecanismo de carácter comodín seguro.<br /><br /> Este atributo es del tipo <xref:System.ServiceModel.HostNameComparisonMode>. De manera predeterminada, es <xref:System.ServiceModel.HostNameComparisonMode.StrongWildcard>.|  
|keepAliveEnabled|Un valor booleano que especifica si se debe establecer una conexión continua con el recurso de Internet.|  
|maxBufferSize|Un entero positivo que especifica el tamaño máximo del búfer. El valor predeterminado es 524288.|  
|proxyAddress|Un URI que especifica la dirección del proxy HTTP. Si `useSystemWebProxy` es `true`, este valor debe ser `null`. De manera predeterminada, es `null`.|  
|proxyAuthenticationScheme|Especifica el protocolo utilizado para autenticar solicitudes de cliente que son procesadas por un proxy HTTP. Los valores válidos son los siguientes:<br /><br /> -None: Se realiza ninguna autenticación.<br />-Digest: Especifica la autenticación implícita.<br />-Negotiate: Negocia con el cliente para determinar el esquema de autenticación. Si cliente y el servidor son compatibles con Kerberos, se utiliza; de lo contrario, se utiliza NTLM.<br />-Ntlm: Especifica la autenticación de NTLM.<br />-Básicas: Especifica la autenticación básica.<br />-Anónimo: Especifica la autenticación anónima.<br /><br /> El valor predeterminado es Anonymous. Este atributo es del tipo <xref:System.Net.AuthenticationSchemes>. Tenga en cuenta que <xref:System.Net.AuthenticationSchemes.IntegratedWindowsAuthentication?displayProperty=nameWithType> no se admite.|  
|realm|Una cadena que especifica el dominio kerberos que se utilizará en el proxy/servidor. El valor predeterminado es una cadena vacía.<br /><br /> Los servidores usan los dominios para particionar recursos protegidos. Cada partición puede tener su propio esquema de autenticación y/o base de datos de autorización. Los dominios sólo se utilizan para la autenticación básica e implícita. Cuando un cliente se autentica correctamente, la autenticación es válida para todos los recursos de un dominio kerberos determinado. Para obtener una descripción detallada de dominios Kerberos, consulte RFC 2617 en el [sitio Web IETF](https://www.ietf.org).|  
|transferMode|Especifica si los mensajes se almacenan en búfer, se transmiten o si son una solicitud o una respuesta. Los valores válidos son los siguientes:<br /><br /> -En el búfer: Se almacenan en búfer los mensajes de solicitud y respuesta.<br />-Transmite por secuencias: Se transmiten los mensajes de solicitud y respuesta.<br />-   StreamedRequest: Se transmite el mensaje de solicitud y se almacena en búfer el mensaje de respuesta.<br />-   StreamedResponse: Se almacena en búfer el mensaje de solicitud y se transmite el mensaje de respuesta.<br /><br /> El valor predeterminado es Buffered. Este atributo es del tipo <xref:System.ServiceModel.TransferMode>.|  
|unsafeConnectionNtlmAuthentication|Un valor booleano que especifica si la conexión compartida no segura está habilitada en el servidor. De manera predeterminada, es `false`. Si está habilitado, la autenticación NTLM se realiza una vez en cada conexión TCP.|  
|useDefaultWebProxy|Un valor que especifica si se utiliza la configuración del proxy del equipo en lugar de la configuración específica del usuario. De manera predeterminada, es `true`.|  
  
### <a name="child-elements"></a>Elementos secundarios  
 Ninguna  
  
### <a name="parent-elements"></a>Elementos primarios  
  
|Elemento|Descripción|  
|-------------|-----------------|  
|[\<binding>](../../../../../docs/framework/misc/binding.md)|Define todas las funcionalidades de enlace del enlace personalizado.|  
  
## <a name="remarks"></a>Comentarios  
 El elemento `httpTransport` es el punto inicial para crear un enlace personalizado que implementa el protocolo de transporte HTTP. HTTP es el transporte primario utilizado para fines de interoperabilidad. Se admite este transporte por Windows Communication Foundation (WCF) para garantizar la interoperabilidad con otras pilas de servicios Web que no son de WCF.  
  
## <a name="see-also"></a>Vea también
- <xref:System.ServiceModel.Configuration.HttpTransportElement>
- <xref:System.ServiceModel.Channels.HttpTransportBindingElement>
- <xref:System.ServiceModel.Channels.TransportBindingElement>
- <xref:System.ServiceModel.Channels.CustomBinding>
- [Transportes](../../../../../docs/framework/wcf/feature-details/transports.md)
- [Elección del transporte](../../../../../docs/framework/wcf/feature-details/choosing-a-transport.md)
- [Enlaces](../../../../../docs/framework/wcf/bindings.md)
- [Extensión de enlaces](../../../../../docs/framework/wcf/extending/extending-bindings.md)
- [Enlaces personalizados](../../../../../docs/framework/wcf/extending/custom-bindings.md)
- [\<customBinding>](../../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)
