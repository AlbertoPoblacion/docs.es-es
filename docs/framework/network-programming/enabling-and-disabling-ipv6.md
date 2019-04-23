---
title: Habilitar y deshabilitar IPv6
ms.date: 03/30/2017
ms.assetid: 6408d3ef-c9ba-49d9-b15e-fe74bd3ef031
ms.openlocfilehash: 73dee0cb57674c8a2fa4ba2246162870ab1e3a10
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59083691"
---
# <a name="enabling-and-disabling-ipv6"></a>Habilitar y deshabilitar IPv6
Para usar el protocolo IPv6, asegúrese de que está ejecutando una versión del sistema operativo que admita IPv6 y asegúrese de que el sistema operativo y las clases de red están configurados correctamente.  
  
## <a name="configuration-steps"></a>Pasos de la configuración  
 En la tabla siguiente se muestran varias configuraciones  
  
|¿El sistema operativo está habilitado para IPv6?|¿Las clases de red están habilitadas para IPv6?|Descripción|  
|-------------------------------------|---------------------------------------|-----------------|  
|No|No|Puede analizar las direcciones de IPv6.|  
|No|Sí|Puede analizar las direcciones de IPv6.|  
|Sí|No|Puede analizar las direcciones de IPv6 y resolver las direcciones de IPv6 mediante métodos de resolución de nombres que no se hayan marcado como obsoletos.|  
|Sí|Sí|Puede analizar y resolver las direcciones de IPv6 con todos los métodos, incluidos los que se hayan marcado como obsoletos.|  
  
 Tenga en cuenta que para habilitar la compatibilidad con IPv6 para todas las clases del espacio de nombres System.Net, debe modificar el archivo de configuración del equipo o el archivo de configuración de la aplicación. El archivo de configuración de la aplicación tiene prioridad sobre el archivo de configuración del equipo.  
  
 Para obtener un ejemplo de cómo modificar el archivo de configuración de equipo, *machine.config*, para permitir la compatibilidad con Ipv6, vea [Cómo: Modificar el archivo de configuración de equipo para habilitar la compatibilidad con Ipv6](../../../docs/framework/network-programming/how-to-modify-the-computer-configuration-file-to-enable-ipv6-support.md). Además, asegúrese de que la compatibilidad con IPv6 está habilitada para el sistema operativo.  
  
 .NET Framework tiene un modificador de configuración establecido en un archivo de configuración como se muestra a continuación:  
  
```xml  
<system.net>  
  ...  
  <settings>  
    ...  
    <ipv6 enabled="true"/>  
    ...  
  </settings>  
  ...  
</system.net>  
```  
  
 Para .NET Framework versión 1.1 y anterior, el valor del modificador de la configuración **ipv6 enabled** especifica si los miembros de la clase <xref:System.Net.Dns?displayProperty=nameWithType> devuelven las direcciones de IPv6.  
  
 En la versión 2.0 de .NET Framework y versiones posteriores, si Windows admite IPv6, entonces los miembros de la clase <xref:System.Net.Dns?displayProperty=nameWithType> (por ejemplo, el método <xref:System.Net.Dns.GetHostEntry%2A?displayProperty=nameWithType>), devolverán las direcciones de IPv6 con una limitación. Los miembros obsoletos del DNS <xref:System.Net.Dns?displayProperty=nameWithType> (por ejemplo, el método <xref:System.Net.Dns.Resolve%2A?displayProperty=nameWithType>) leerán y reconocerán el valor en el archivo de configuración para la configuración habilitada para IPv6.  
  
## <a name="see-also"></a>Vea también

- [Protocolo de Internet versión 6](../../../docs/framework/network-programming/internet-protocol-version-6.md)
- [Sockets](../../../docs/framework/network-programming/sockets.md)
- [Esquema de la configuración de red](../../../docs/framework/configure-apps/file-schema/network/index.md)
- [Elemento \<ipv6> (configuración de red)](../../../docs/framework/configure-apps/file-schema/network/ipv6-element-network-settings.md)
