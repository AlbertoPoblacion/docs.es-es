---
title: '&lt;allowAccounts&gt;'
ms.date: 03/30/2017
ms.assetid: 166923a9-a8ac-478f-92f9-529d9667f3a6
ms.openlocfilehash: c1c4630e6191dbbe02688a4e4a9db9e18b8d36d2
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/23/2019
ms.locfileid: "54508423"
---
# <a name="ltallowaccountsgt"></a>&lt;allowAccounts&gt;
Contiene una colección de elementos de configuración que especifique el usuario de cuentas para los procesos que hospedan servicios Windows Communication Foundation (WCF) y tienen concedido acceso de conexión al servicio de uso compartido.  
  
 \<system.serviceModel.activation>  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
<allowAccounts>
  <add securityIdentifier="String" />
</allowAccounts>
```  
  
## <a name="attributes-and-elements"></a>Atributos y elementos  
 En las siguientes secciones se describen los atributos, los elementos secundarios y los elementos primarios.  
  
### <a name="attributes"></a>Atributos  
 Ninguno.  
  
### <a name="child-elements"></a>Elementos secundarios  
  
|Atributo|Descripción|  
|---------------|-----------------|  
|[\<add>](../../../../../docs/framework/configure-apps/file-schema/wcf/add-of-allowaccounts.md)|Agrega una cuenta de usuario para los procesos que hospedan servicios WCF y tienen concedido acceso de conexión al servicio de uso compartido|  
  
### <a name="parent-elements"></a>Elementos primarios  
  
|Elemento|Descripción|  
|-------------|-----------------|  
|[\<NET.Pipe >](../../../../../docs/framework/configure-apps/file-schema/wcf/net-pipe.md) o [ \<net.tcp >](../../../../../docs/framework/configure-apps/file-schema/wcf/net-tcp.md)|Especifica la configuración para la Canalización de Red o servicios de uso compartido de TCP.|  
  
## <a name="see-also"></a>Vea también
- <xref:System.ServiceModel.Activation.Configuration.NetTcpSection.AllowAccounts%2A>
- <xref:System.ServiceModel.Activation.Configuration.NetPipeSection.AllowAccounts%2A>
- <xref:System.ServiceModel.Activation.Configuration.SecurityIdentifierElementCollection>
- <xref:System.ServiceModel.Activation.Configuration.SecurityIdentifierElement>
