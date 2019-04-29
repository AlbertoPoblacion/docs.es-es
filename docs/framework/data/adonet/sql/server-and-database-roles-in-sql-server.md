---
title: Roles de servidor y base de datos en SQL Server
ms.date: 03/30/2017
ms.assetid: 5482dfdb-e498-4614-8652-b174829eed13
ms.openlocfilehash: e2d0de08f23bc3767e11de31c4ded4a326d060a9
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61645973"
---
# <a name="server-and-database-roles-in-sql-server"></a>Roles de servidor y base de datos en SQL Server
Todas las versiones de SQL Server usan la seguridad basada en roles, que permite asignar permisos a un rol, o grupo de usuarios, en lugar de asignarlos a usuarios individuales. Los roles fijos de servidor y base de datos cuentan con un conjunto fijo de permisos asignados.  
  
## <a name="fixed-server-roles"></a>Roles fijos de servidor  
 Los roles fijos de servidor cuentan con un conjunto fijo de permisos y ámbito de servidor. Están pensadas para su uso en la administración de SQL Server y los permisos asignadas a ellas no se pueden modificar. Se pueden asignar inicios de sesión a los roles fijos de servidor sin necesidad de disponer de una cuenta de usuario en una base de datos.  
  
> [!IMPORTANT]
>  El rol fijo de servidor `sysadmin` incluye a todos los demás roles y cuenta con un ámbito ilimitado. No agregue entidades de seguridad a este rol a menos que sean de total confianza. Los miembros del rol `sysadmin` disponen de permisos administrativos irrevocables en todas las bases de datos y recursos del servidor.  
  
 Sea selectivo a la hora de agregar usuarios a los roles fijos de servidor. Por ejemplo, el rol `bulkadmin` permite a los usuarios insertar el contenido de cualquier archivo local en una tabla, lo que puede poner en peligro la integridad de los datos. Para obtener una lista completa de los roles fijos de servidor y permisos, vea los libros en pantalla de SQL Server.  
  
## <a name="fixed-database-roles"></a>Roles fijos de base de datos  
 Los roles fijos de base de datos incluyen un conjunto predefinido de permisos diseñados para permitir administrar grupos de permisos con facilidad. Los miembros del rol `db_owner` pueden realizar todas las actividades de configuración y mantenimiento de la base de datos.  
  
 Para obtener más información sobre los roles predefinidos en SQL Server, vea los siguientes recursos.  
  
|Recurso|Descripción|  
|--------------|-----------------|  
|[Funciones de nivel de servidor](/sql/relational-databases/security/authentication-access/server-level-roles)|Describe funciones fijas de servidor y los permisos asociados con ellos en SQL Server.|  
|[Roles de nivel de base de datos](/sql/relational-databases/security/authentication-access/database-level-roles)|Describe los roles fijos de base de datos y los permisos asociados a ellas.|  
  
## <a name="database-roles-and-users"></a>Roles y usuarios de base de datos  
 Para trabajar con objetos de base de datos, se deben asignar inicios de sesión a cuentas de usuario de base de datos. Estos usuarios de base de datos se podrán agregar entonces a roles de base de datos y heredarán los conjuntos de permisos asociados con estos roles. Se pueden conceder todos los permisos.  
  
 A la hora de diseñar la seguridad para la aplicación, también debe tener en cuenta el rol `public`, la cuenta de usuario `dbo` y la cuenta `guest`.  
  
### <a name="the-public-role"></a>Rol public  
 El rol `public` está contenido en todas las bases de datos, incluidas las bases de datos del sistema. No se puede eliminar y no se pueden agregar ni quitar usuarios de ella. Todos los usuarios y los demás roles heredan los permisos concedidos al rol `public`, ya que pertenecen de forma predeterminada al rol `public`. Por tanto, solo debe conceder al rol `public` los permisos que desee que tengan todos los usuarios.  
  
### <a name="the-dbo-user-account"></a>Cuenta de usuario dbo  
 `dbo`, o propietario de base de datos, es una cuenta de usuario con permisos implícitos para realizar todas las actividades en la base de datos. Los miembros del rol fijo del servidor `sysadmin` se asignan automáticamente a `dbo`.  
  
> [!NOTE]
>  `dbo` También es el nombre de un esquema, como se describe en [propiedad y separación usuario-esquema en SQL Server](../../../../../docs/framework/data/adonet/sql/ownership-and-user-schema-separation-in-sql-server.md).  
  
 La cuenta de usuario `dbo` se confunde a menudo con el rol fijo de base de datos `db_owner`. El ámbito de `db_owner` es una base de datos y el ámbito de `sysadmin` es el servidor completo. La pertenencia al rol `db_owner` no proporciona privilegios de usuario `dbo`.  
  
### <a name="the-guest-user-account"></a>Cuenta de usuario guest  
 Después de que un usuario se haya autenticado y se le haya permitido iniciar sesión en una instancia de SQL Server, debe existir una cuenta de usuario independiente en cada base de datos a la que tenga acceso el usuario. Si se exige una cuenta de usuario en cada base de datos, se impide que los usuarios se conecten a una instancia de SQL Server y puedan tener acceso a todas las bases de datos de un servidor. La existencia de una cuenta de usuario `guest` en la base de datos evita este requisito, ya que permite que un inicio de sesión sin cuenta de usuario de base de datos tenga acceso a una base de datos.  
  
 La cuenta `guest` es una cuenta integrada en todas las versiones de SQL Server. De forma predeterminada, está deshabilitada en las bases de datos nuevas. Si está habilitada, se puede deshabilitar mediante la revocación de su permiso CONNECT, que se lleva a cabo con la ejecución de la instrucción REVOKE CONNECT FROM GUEST de Transact-SQL.  
  
> [!IMPORTANT]
>  Se debe evitar el uso de la cuenta `guest`, ya que todos los inicios de sesión que no dispongan de permisos de base de datos propios obtendrán los permisos de base de datos concedidos a esta cuenta. Si debe usar la cuenta `guest`, concédale los permisos mínimos.  
  
 Para obtener más información sobre los inicios de sesión, los usuarios y los roles de SQL Server, vea los siguientes recursos.  
  
|Recurso|Descripción|  
|--------------|-----------------|  
|[Introducción a los permisos del motor de base de datos](/sql/relational-databases/security/authentication-access/getting-started-with-database-engine-permissions)|Contiene vínculos a temas que describen las entidades de seguridad, los roles, las credenciales, los elementos que pueden protegerse y los permisos.|  
|[Entidades de seguridad](/sql/relational-databases/security/authentication-access/principals-database-engine)|Describe las entidades de seguridad y contiene vínculos a temas que describen los roles de servidor y de base de datos.|  
  
## <a name="see-also"></a>Vea también

- [Proteger aplicaciones de ADO.NET](../../../../../docs/framework/data/adonet/securing-ado-net-applications.md)
- [Escenarios de seguridad de aplicaciones en SQL Server](../../../../../docs/framework/data/adonet/sql/application-security-scenarios-in-sql-server.md)
- [Autenticación en SQL Server](../../../../../docs/framework/data/adonet/sql/authentication-in-sql-server.md)
- [Propiedad y separación de esquemas de usuario en SQL Server](../../../../../docs/framework/data/adonet/sql/ownership-and-user-schema-separation-in-sql-server.md)
- [Autorización y permisos en SQL Server](../../../../../docs/framework/data/adonet/sql/authorization-and-permissions-in-sql-server.md)
- [Proveedores administrados de ADO.NET y Centro para desarrolladores de DataSet](https://go.microsoft.com/fwlink/?LinkId=217917)
