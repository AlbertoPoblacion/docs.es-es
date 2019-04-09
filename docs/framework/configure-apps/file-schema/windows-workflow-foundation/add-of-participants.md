---
title: <add> de <participants>
ms.date: 03/30/2017
ms.topic: reference
ms.assetid: 3c730850-6f8e-4102-acb8-8effb4e09463
ms.openlocfilehash: 291d1a006bc16769e36774dd9507017cb555e547
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2019
ms.locfileid: "59079128"
---
# <a name="add-of-participants"></a>\<Agregar > de \<participantes >
Configure un participante del seguimiento que escucha los registros de seguimiento que se emiten del tiempo de ejecución directamente y los procesa del modo en que cada uno esté configurado. Esto incluye la escritura en un resultado concreto (p. ej., un archivo, la consola o ETW), procesar o agregar los registros, o cualquier otra combinación que pueda resultar necesaria.  
  
 Para obtener más información de seguimiento de flujo de trabajo y los participantes de seguimiento, vea [seguimiento y traza del flujo de trabajo](../../../../../docs/framework/windows-workflow-foundation/workflow-tracking-and-tracing.md) y [participantes de seguimiento](../../../../../docs/framework/windows-workflow-foundation/tracking-participants.md).  
  
\<system.serviceModel>  
\<tracking>  
\<participants>  
\<add>  
  
## <a name="syntax"></a>Sintaxis  
  
```xml
<tracking>
  <participants>
    <add name="String" profileName="String" type="String" />
  </participants>
</tracking>   
```  
  
## <a name="attributes-and-elements"></a>Atributos y elementos  
 En las siguientes secciones se describen los atributos, los elementos secundarios y los elementos primarios.  
  
### <a name="attributes"></a>Atributos  
  
|Elemento|Descripción|  
|-------------|-----------------|  
|name|Cadena que especifica el nombre de un participante de seguimiento.|  
|profileName|Una cadena que especifica el nombre del perfil de seguimiento que define los registros de seguimiento a los que se ha suscrito el participante de seguimiento.|  
|type|Una cadena que especifica el tipo de un participante de seguimiento.|  
  
### <a name="child-elements"></a>Elementos secundarios  
 Ninguno.  
  
### <a name="parent-elements"></a>Elementos primarios  
  
|Elemento|Descripción|  
|-------------|-----------------|  
|[\<participants>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/participants.md)|Una lista de los participantes de seguimiento|  
  
## <a name="remarks"></a>Comentarios  
 Los participantes de seguimiento se usan para obtener los datos de seguimiento emitidos del flujo de trabajo y almacenarlos en los distintos medios. Del mismo modo, cualquier procesamiento posterior en los Registros de seguimiento también puede realizarse dentro del participante de seguimiento.  
  
 Varios participantes de seguimiento pueden utilizar los eventos de seguimiento de forma simultánea. Cada participante de seguimiento puede asociarse con un perfil de seguimiento distinto.  
  
 Se proporciona un participante de seguimiento estándar que escribe los registros de seguimiento en una sesión de ETW. El participante se configura en un servicio de flujo de trabajo agregando un comportamiento específico del seguimiento en un archivo de configuración. Habilitar un participante de seguimiento de ETW permite realizar un seguimiento de los registros que se van a ver en el visor de eventos. Si eso no cumple sus requisitos, también puede escribir un participante de seguimiento personalizado.  
  
## <a name="example"></a>Ejemplo  
 El siguiente ejemplo de configuración muestra el participante de seguimiento de ETW estándar que se está configurando en el archivo Web.config.  
  
 El identificador del proveedor que el participante de seguimiento de ETW usa para escribir los registros de seguimiento en ETW se define en el  **\<diagnósticos >** sección. El participante de seguimiento tiene un perfil asociado para especificar los registros de seguimiento a los que se ha suscrito. Esto viene definido por el **profileName** atributo de la  **\<Agregar >** elemento. Una vez que se definen, el participante de seguimiento se agrega a la  **\<etwTracking >** comportamiento del servicio. Esto agregará los participantes de seguimiento seleccionados a las extensiones de la instancia de flujo de trabajo para que puedan empezar a recibir los registros de seguimiento.  
  
```xml  
<configuration>   
  <system.web>   
    <compilation targetFrameworkMoniker=".NETFramework,Version=v4.0"/>   
  </system.web>   
  <system.serviceModel>   
    <diagnostics etwProviderId="52A3165D-4AD9-405C-B1E8-7D9A257EAC9F" />                
    <tracking>   
      <participants>   
        <add name="EtwTrackingParticipant"   
             type="System.Activities.Tracking.EtwTrackingParticipant, System.Activities, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35"   
             profileName="HealthMonitoring_Tracking_Profile"/>   
      </participants>   
    </tracking>   
    <behaviors>   
      <serviceBehaviors>   
        <behavior>   
          <etwTracking profileName="Sample Tracking Profile"/>  
        </behavior>   
      </serviceBehaviors>   
    </behaviors>   
  </system.serviceModel>   
</configuration>  
```  
  
## <a name="see-also"></a>Vea también

- <xref:System.ServiceModel.Activities.Tracking.Configuration.TrackingSection>
- <xref:System.ServiceModel.Activities.Description.EtwTrackingBehavior>
- <xref:System.ServiceModel.Activities.Configuration.EtwTrackingBehaviorElement>
- [Seguimiento y traza del flujo de trabajo](../../../../../docs/framework/windows-workflow-foundation/workflow-tracking-and-tracing.md)
- [Participantes de seguimiento](../../../../../docs/framework/windows-workflow-foundation/tracking-participants.md)
