---
title: <rsa>
ms.date: 03/30/2017
ms.assetid: ae1f2267-e40d-42ff-8abf-06ab7067bdb9
ms.openlocfilehash: 0e307069bd3a98153cc66147ba7bcf511cf13a8e
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61670667"
---
# <a name="rsa"></a>\<rsa>
Un cliente WCF seguro que se conecta a un punto de conexión con esta identidad comprueba que las notificaciones presentadas por el servidor contienen una notificación que incluye la clave pública RSA utilizada para construir esta identidad.  
  
 \<identity>  
\<rsa>  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
<rsa value="String" />
```  
  
## <a name="attributes-and-elements"></a>Atributos y elementos  
 En las siguientes secciones se describen los atributos, los elementos secundarios y los elementos primarios  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descripción|  
|---------------|-----------------|  
|value|Cadena opcional. El valor de clave pública de RSA con la que se va a comparar en el cliente.|  
  
### <a name="child-elements"></a>Elementos secundarios  
 Ninguna  
  
### <a name="parent-elements"></a>Elementos primarios  
  
|Elemento|Descripción|  
|-------------|-----------------|  
|[\<identity>](../../../../../docs/framework/configure-apps/file-schema/wcf/identity.md)|Especifica la identidad del servicio que va a autenticar el cliente.|  
  
## <a name="remarks"></a>Comentarios  
 Una comprobación de RSA le permite restringir específicamente la autenticación a un certificado único basado en su clave RSA o que generó su propio valor de clave de RSA. Esto habilita una autenticación más estricta de una clave RSA específica en el gasto del servicio que ya no trabaja con clientes existentes si se cambia el valor de clave de RSA.  
  
 Para obtener más información sobre el uso de identidad para validar un servicio a un cliente, consulte [autenticación e identidad de servicio](../../../../../docs/framework/wcf/feature-details/service-identity-and-authentication.md).  
  
## <a name="example"></a>Ejemplo  
 El código de configuración siguiente especifica el valor de clave pública de un certificado X.509 que se usa para autenticar un servidor.  
  
```xml  
<identity>
  <rsa value="0000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000" />
</identity>
```  
  
## <a name="see-also"></a>Vea también

- <xref:System.ServiceModel.Configuration.IdentityElement>
- <xref:System.ServiceModel.EndpointAddress>
- <xref:System.ServiceModel.EndpointAddress.Identity%2A>
- <xref:System.ServiceModel.RsaEndpointIdentity>
- [Identidad del servicio y autenticación](../../../../../docs/framework/wcf/feature-details/service-identity-and-authentication.md)
- [\<identity>](../../../../../docs/framework/configure-apps/file-schema/wcf/identity.md)
