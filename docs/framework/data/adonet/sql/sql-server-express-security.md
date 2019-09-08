---
title: Seguridad de SQL Server Express
ms.date: 03/30/2017
ms.assetid: cf9cf6d9-4b05-43e9-ac7b-6cefbfcd6d4e
ms.openlocfilehash: 55f1d141e50ed7afd851d7330cfaf2e3b6380f18
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/07/2019
ms.locfileid: "70791691"
---
# <a name="sql-server-express-security"></a>Seguridad de SQL Server Express
Microsoft SQL Server Express Edition (SQL Server Express) se basa en Microsoft SQL Server y es compatible con la mayoría de las características del motor de base de datos. Está diseñado de manera que las características que no sean esenciales y la conectividad de red están desactivadas de manera predeterminada. Con ello se reduce la superficie expuesta a los ataques de usuarios malintencionados.  
  
 SQL Server Express se instala normalmente como una instancia con nombre. El nombre predeterminado de dicha instancia es `SQLExpress`. Una instancia con nombre se identifica mediante el nombre de red del equipo sumado al nombre de la instancia que se especifica durante la instalación.  
  
## <a name="network-access"></a>Acceso a la red  
 Por razones de seguridad, los protocolos de red se deshabilitan de forma predeterminada en SQL Server Express. Con ello se evitan los ataques de usuarios externos que podrían poner en peligro el equipo que hospeda la instancia de SQL Server Express. Se debe habilitar de forma explícita la conectividad de red e iniciar el servicio de SQL Server Browser para conectar a una instancia de SQL Server Express desde otro equipo.  
  
 Una vez habilitada la conectividad de red, la instancia de SQL Server Express tiene los mismos requisitos de seguridad que las de las otras ediciones de SQL Server.  
  
## <a name="user-instances"></a>Instancias de usuario  
 Una instancia de usuario es una instancia independiente del motor de base de datos de SQL Server Express que se genera mediante una instancia principal de SQL Server Express. La finalidad más importante de una instancia de usuario es que los usuarios que ejecutan Windows con una cuenta de privilegios mínimos puedan tener privilegios de administrador del sistema (`sysadmin`) en la instancia de SQL Server Express de su equipo local. Las instancias de usuario no están pensadas para usuarios que son administradores del sistema en sus propios equipos.  
  
 Una instancia de usuario se genera desde una instancia principal de SQL Server o SQL Server Express en nombre de un usuario. Se ejecuta como un proceso del usuario en el contexto de seguridad de Windows del usuario, no como un servicio. No se permiten inicios de sesión de SQL Server; únicamente se admiten los inicios de sesión de Windows. De esta manera se evita que haya software que se ejecuta en una instancia de usuario que efectúe cambios en todo el sistema para los que el usuario no debería tener permisos. La instancia de usuario también es conocida como instancia secundaria o de cliente, y a veces es denominada utilizando el acrónimo RANU (del inglés "run as normal user", ejecutar como usuario normal).  
  
 Cada instancia de usuario se aísla de su instancia principal y de otras instancias de usuario que se ejecuten en el mismo equipo. Las bases de datos instaladas en instancias de usuario se abren sólo en modo usuario único; no se pueden conectar varios usuarios. La replicación, las consultas distribuidas y las conexiones remotas se deshabilitan para instancias de usuario. Al conectar a una instancia de usuario, los usuarios no tienen ningún privilegio especial  en la instancia principal de SQL Server Express.  
  
## <a name="external-resources"></a>Recursos externos  
 Para obtener más información acerca de SQL Server Express, vea los siguientes recursos.  
  
|||  
|-|-|  
|[Libros en pantalla de Microsoft SQL Server 2005 Express Edition](https://docs.microsoft.com/previous-versions/sql/sql-server-2005/ms165706(v=sql.90))|Documentación completa sobre SQL Server Express 2005 Express Edition.|  
|[Instancias de usuario para usuarios que no son administradores](https://docs.microsoft.com/previous-versions/sql/sql-server-2008/ms143684(v=sql.100)) en libros en pantalla de SQL Server|Describe cómo crear e implementar instancias de usuario.|  
|[Instancias de usuario de SQL Server Express](sql-server-express-user-instances.md)|Describe las capacidades de instancia de usuario en una aplicación de ADO.NET. Proporciona información sobre cómo habilitar una instancia de usuario, cómo conectar a una instancia de usuario utilizando <xref:System.Data.SqlClient.SqlConnection>, ciclo de vida y casos de instancia de usuario.|  
  
## <a name="see-also"></a>Vea también

- [Seguridad de SQL Server](sql-server-security.md)
- [Instancias de usuario de SQL Server Express](sql-server-express-user-instances.md)
- [Información general sobre ADO.NET](../ado-net-overview.md)
