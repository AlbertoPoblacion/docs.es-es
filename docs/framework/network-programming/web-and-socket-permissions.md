---
title: Permisos de web y socket
ms.date: 03/30/2017
helpviewer_keywords:
- Networking
- positions [.NET Framework], accepting
- sockets, permissions
- network, permissions
- Internet, permissions
- Network Resources
- SocketPermission class, about SocketPermission class
- positions [.NET Framework], connecting
- WebPermission class, about WebPermission class
- permissions [.NET Framework], sockets
- security [.NET Framework], Internet
- positions [.NET Framework], granting
ms.assetid: d51ad8cb-03ae-4a51-bfcd-cfcf6b98afa9
ms.openlocfilehash: 78ad06107155408b2aca854a8251c21a24c6577a
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2019
ms.locfileid: "59166860"
---
# <a name="web-and-socket-permissions"></a>Permisos de web y socket
La seguridad de Internet para las aplicaciones que usan el espacio de nombres <xref:System.Net> se proporciona con las clases <xref:System.Net.WebPermission> y <xref:System.Net.SocketPermission>. La clase **WebPermission** controla el derecho de una aplicación a solicitar datos de un identificador URI o de servir un identificador URI en Internet. La clase **SocketPermission** controla el derecho de una aplicación a usar un <xref:System.Net.Sockets.Socket> para aceptar los datos en un puerto local o de ponerse en contacto con dispositivos remotos mediante un protocolo de transporte en otra dirección, en función del host, el número de puerto y el protocolo de transporte del socket.  
  
 La clase de permiso que se use dependerá del tipo de aplicación. Las aplicaciones que utilizan <xref:System.Net.WebRequest> y sus descendientes deben usar la clase **WebPermission** para administrar los permisos. Las aplicaciones que utilizan el acceso de nivel de socket deben usar la clase **SocketPermission** para administrar los permisos.  
  
 **WebPermission** y **SocketPermission** definen dos permisos: el de aceptación y el de conexión. El permiso de aceptación permite a la aplicación responder a una conexión entrante desde otra entidad. El permiso de conexión permite a la aplicación iniciar una conexión con otra entidad.  
  
 Para las instancias **SocketPermission**, el permiso de aceptación implica que una aplicación puede aceptar conexiones entrantes en una dirección de transporte local, mientras que el permiso de conexión implica que una aplicación puede conectarse a alguna dirección de transporte remota (o local).  
  
 Para las instancias **WebPermission**, el permiso de aceptación implica que una aplicación puede exportar al mundo el identificador URI controlado por **WebPermission**, mientras que el permiso de conexión implica que una aplicación puede obtener acceso a ese URI (ya sea local o remoto).  
  
## <a name="see-also"></a>Vea también

- [Seguridad](../../../docs/standard/security/index.md)
- [Seguridad en la programación para redes](../../../docs/framework/network-programming/security-in-network-programming.md)
