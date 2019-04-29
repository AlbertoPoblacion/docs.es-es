---
title: <serviceSecurityAudit>
ms.date: 03/30/2017
ms.assetid: ba517369-a034-4f8e-a2c4-66517716062b
ms.openlocfilehash: 384a1cdb6d39f4d6ecd2353a15c0da7c6d2e82bd
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61758124"
---
# <a name="servicesecurityaudit"></a>\<serviceSecurityAudit>
Especifica valores que habilitan la auditoría de eventos de seguridad durante las operaciones del servicio.  
  
 \<system.ServiceModel>  
\<comportamientos >  
\<serviceBehaviors>  
\<comportamiento >  
\<serviceSecurityAudit>  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
<serviceSecurityAudit auditLogLocation="Default/Application/Security"
                      messageAuthenticationAuditLevel="None/Success/Failure/SuccessOrFailure"
                      serviceAuthorizationAuditLevel="None/Success/Failure/SuccessOrFailure"
                      suppressAuditFailure="Boolean" />
```  
  
## <a name="attributes-and-elements"></a>Atributos y elementos  
 En las siguientes secciones se describen los atributos, los elementos secundarios y los elementos primarios.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descripción|  
|---------------|-----------------|  
|auditLogLocation|Especifica la ubicación del registro de auditoría. Los valores válidos son los siguientes:<br /><br /> -Default: Eventos de seguridad se escriben en el registro de aplicaciones en Windows XP y en el registro de eventos en Windows Server 2003 y Windows Vista.<br />-Aplicación: Eventos de auditoría se escriben en el registro de eventos de aplicación.<br />-Security: Eventos de auditoría se escriben en el registro de eventos de seguridad.<br /><br /> El valor predeterminado es Default. Para obtener más información, consulta <xref:System.ServiceModel.AuditLogLocation>.|  
|suppressAuditFailure|Un valor booleano que especifica el comportamiento para suprimir errores al escribir en el registro de auditoría.<br /><br /> Se debería notificar a las aplicaciones de los errores de escritura en el registro de auditoría. Si su aplicación no está diseñada para administrar errores de auditoría, debería usar este atributo para suprimir errores de escritura en el registro de auditoría.<br /><br /> Si este atributo es `true`, el sistema administra excepciones distintas de OutOfMemoryException, StackOverFlowException, ThreadAbortException y ArgumentException que son el resultado de los intentos de escribir los eventos de auditoría y no se propagan a la aplicación. Si este atributo es `false`, todas las excepciones que son el resultado de los intentos por escribir los eventos de auditoría se pasan a la aplicación.<br /><br /> De manera predeterminada, es `true`.|  
|serviceAuthorizationAuditLevel|Especifica los tipos de eventos de autorización que se graban en el registro de auditoría. Los valores válidos son los siguientes:<br /><br /> -None: Se realiza ninguna auditoría de eventos de autorización de servicio.<br />-Correcto: Solo los eventos de autorización de servicio correcta se auditan.<br />-Error: Solo los eventos de error servicio autorización se auditan.<br />-   SuccessOrFailure: Se auditan los eventos de autorización de servicio correctos y erróneos.<br /><br /> El valor predeterminado es None. Para obtener más información, consulta <xref:System.ServiceModel.AuditLevel>.|  
|messageAuthenticationAuditLevel|Especifica el tipo de eventos de auditoría de autenticación de mensajes registrados. Los valores válidos son los siguientes:<br /><br /> -None: Se genera ningún evento de auditoría.<br />-Correcto: Solo los eventos de seguridad correctos (validación completa incluida la validación de firma de mensajes, cifrado y validación del token) se registran.<br />-Error: Solo los eventos de error se registran.<br />-   SuccessOrFailure: Se registran los eventos correctos y erróneos.<br /><br /> El valor predeterminado es None. Para obtener más información, consulta <xref:System.ServiceModel.AuditLevel>.|  
  
### <a name="child-elements"></a>Elementos secundarios  
 Ninguno.  
  
### <a name="parent-elements"></a>Elementos primarios  
  
|Elemento|Descripción|  
|-------------|-----------------|  
|[\<behavior>](../../../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md)|Especifica un elemento de comportamiento.|  
  
## <a name="remarks"></a>Comentarios  
 Este elemento de configuración se utiliza para auditar los eventos de autenticación de Windows Communication Foundation (WCF). Cuando la auditoría está habilitada, se pueden auditar intentos de autenticación correctos (o ambos) o fallidos. Los eventos se escriben en uno de tres registros de eventos: aplicación, seguridad o registro predeterminado para la versión de sistema operativo. Los registros de eventos  se pueden ver utilizando el Visor de eventos de Windows.  
  
 Para obtener un ejemplo detallado del uso de este elemento de configuración, consulte [comportamiento de auditoría de servicio](../../../../../docs/framework/wcf/samples/service-auditing-behavior.md).  
  
 De forma predeterminada, en Windows XP los eventos de auditoría se pueden ver en el registro de aplicaciones, mientras que en Windows Server 2003 y Windows Vista, los eventos de auditoría se pueden ver en el registro de seguridad. Se puede especificar la ubicación de los eventos de auditoría estableciendo el atributo `auditLogLocation` en 'Aplicación' o 'Seguridad'. Para obtener más información, vea [Cómo: Auditar eventos de seguridad](../../../../../docs/framework/wcf/feature-details/how-to-audit-wcf-security-events.md). Si los eventos se escriben en el registro de seguridad, LocalSecurityPolicy -> habilitar el acceso a objetos debe establecerse para "Success" y "Failure".  
  
 Al examinar el registro de eventos, el origen de los eventos de auditoría es "ServiceModel Audit 3.0.0.0". Los registros de auditoría de autenticación de mensajes tienen una categoría de "MessageAuthentication" mientras que los registros de auditoría de autorización tienen una categoría de 'ServiceAuthorization'.  
  
 Los eventos de auditoría de autenticación de mensajes incluyen si el mensaje se manipuló, si el mensaje ha expirado y si el cliente puede autenticar el servicio. Proporcionan información sobre si la autenticación fue correcta o no con la identidad del cliente y el punto de conexión al que se envió el mensaje, junto con la acción asociada al mensaje.  
  
 Los eventos de auditoría de autorización de servicio incluyen la decisión de la autorización realizada por un administrador de autorización del servicio. Proporcionan información acerca de si la autorización fue correcta o no con la identidad del cliente, el punto de conexión, el mensaje se envió a la acción asociada con el mensaje, el identificador del contexto de autorización que se generó a partir de la mensaje entrante y el tipo del Administrador de autorización que tomó la decisión de acceso.  
  
## <a name="example"></a>Ejemplo  
  
```xml  
<system.serviceModel>
  <behaviors>
    <serviceBehaviors>
      <behavior name="NewBehavior">
        <serviceSecurityAudit auditLogLocation="Application"
                              suppressAuditFailure="true"
                              serviceAuthorizationAuditLevel="Success"
                              messageAuthenticationAuditLevel="Success" />
      </behavior>
    </serviceBehaviors>
  </behaviors>
</system.serviceModel>
```  
  
## <a name="see-also"></a>Vea también

- <xref:System.ServiceModel.Configuration.ServiceSecurityAuditElement>
- <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior>
- [Comportamientos de seguridad](../../../../../docs/framework/wcf/feature-details/security-behaviors-in-wcf.md)
- [Auditoría](../../../../../docs/framework/wcf/feature-details/auditing-security-events.md)
- [Cómo: Auditar eventos de seguridad](../../../../../docs/framework/wcf/feature-details/how-to-audit-wcf-security-events.md)
- [Comportamiento de auditoría de servicio](../../../../../docs/framework/wcf/samples/service-auditing-behavior.md)
