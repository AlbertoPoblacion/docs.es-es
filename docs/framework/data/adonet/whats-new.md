---
title: Novedades de ADO.NET
ms.date: 03/30/2017
ms.assetid: 3bb65d38-cce2-46f5-b979-e5c505e95e10
ms.openlocfilehash: 0a02ca3885524c5fcf8def603acdce33a972d283
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/07/2019
ms.locfileid: "70791264"
---
# <a name="whats-new-in-adonet"></a>Novedades de ADO.NET

Las siguientes características son nuevas en ADO.NET en el .NET Framework 4,5.

## <a name="sqlclient-data-provider"></a>Proveedor de datos SqlClient

Las siguientes características son nuevas en el proveedor de datos de .NET Framework para SQL Server en .NET Framework 4,5:

- Las palabras clave de cadena de conexión ConnectRetryCount y ConnectRetryInterval (<xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A>) permiten controlar la característica de resistencia de conexión inactiva.

- La compatibilidad con streaming desde SQL Server a una aplicación admite escenarios en los que los datos del servidor no están estructurados.  Consulte [compatibilidad con la transmisión por secuencias de SqlClient](sqlclient-streaming-support.md) para obtener más información.

- Se ha agregado compatibilidad con programación asincrónica.  Vea [programación asincrónica](asynchronous-programming.md) para obtener más información.

- Los errores de conexión se guardarán ahora en el registro de eventos extendidos. Para obtener más información, consulte [Traza de datos en ADO.NET](data-tracing.md).

- SqlClient ahora tiene compatibilidad con la característica de recuperación ante desastres, AlwaysOn de SQL Server. Para obtener más información, vea [compatibilidad de SqlClient con la alta disponibilidad y la recuperación ante desastres](./sql/sqlclient-support-for-high-availability-disaster-recovery.md).

- Una contraseña se puede pasar como cuando <xref:System.Security.SecureString> se usa la autenticación de SQL Server. Vea <xref:System.Data.SqlClient.SqlCredential> para obtener más información.

- Cuando `TrustServerCertificate` es false y `Encrypt` es true, el nombre del servidor (o la dirección IP) de un certificado SSL SQL Server debe coincidir exactamente con el nombre del servidor (o la dirección IP) especificado en la cadena de conexión. De lo contrario, se producirá un error en el intento de conexión. Para obtener más información, vea la descripción de la opción de conexión `Encrypt` en <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A>.

  Si este cambio hace que una aplicación existente ya no pueda conectarse, puede corregir la aplicación usando uno de los siguientes:

  - Emita un certificado que especifique el nombre corto en el campo Nombre común (CN) o Nombre alternativo del sujeto (SAN). Esta solución funcionará para la creación de reflejo de la base de datos.

  - Agregue un alias que asigne el nombre corto al nombre de dominio completo.

  - Use el nombre de dominio completo en la cadena de conexión.

- SqlClient admite Protección ampliada. Para obtener más información acerca de la protección ampliada, consulte [conexión a la motor de base de datos mediante la protección ampliada](https://go.microsoft.com/fwlink/?LinkId=219978).

- SqlClient admite conexiones a bases de datos LocalDB. Para obtener más información, vea [compatibilidad de SqlClient con LocalDB](./sql/sqlclient-support-for-localdb.md).

- `Type System Version=SQL Server 2012;` es el nuevo valor para pasar a la propiedad de conexión `Type System Version`. El valor `Type System Version=Latest;` ahora está obsoleto y se ha hecho equivalente a `Type System Version=SQL Server 2008;`. Para obtener más información, consulta <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A>.

- SqlClient proporciona compatibilidad adicional para columnas dispersas, una característica que se agregó en SQL Server 2008. Si su aplicación ya tiene acceso a datos de una tabla que usa columnas dispersas, debería ver un aumento del rendimiento. La columna IsColumnSet de <xref:System.Data.SqlClient.SqlDataReader.GetSchemaTable%2A> indica si una columna es una columna dispersa que es miembro de un conjunto de columnas. <xref:System.Data.SqlClient.SqlConnection.GetSchema%2A>indica si una columna es una columna dispersa (vea [SQL Server colecciones de esquemas](sql-server-schema-collections.md) para obtener más información). Para obtener más información sobre las columnas dispersas, vea [usar columnas dispersas](https://go.microsoft.com/fwlink/?LinkId=224244).

- El ensamblado Microsoft.SqlServer.Types.dll, que contiene los tipos de datos espaciales, se ha actualizado de la versión 10.0 a la versión 11.0. Las aplicaciones que hacen referencia a este ensamblado pueden producir errores. Para obtener más información, vea [cambios importantes en las características de motor de base de datos](https://go.microsoft.com/fwlink/?LinkId=224367).

## <a name="adonet-entity-framework"></a>ADO.NET Entity Framework

El .NET Framework 4,5 agrega API que permiten nuevos escenarios cuando se trabaja con el Entity Framework 5,0. Para obtener más información acerca de las mejoras y características que se agregaron al Entity Framework 5,0, vea los temas siguientes: [Novedades y](https://go.microsoft.com/fwlink/?LinkID=251106) [Entity Framework versiones y control de versiones](https://go.microsoft.com/fwlink/?LinkId=234899).

## <a name="see-also"></a>Vea también

- [ADO.NET](index.md)
- [Información general sobre ADO.NET](ado-net-overview.md)
- [SQL Server y ADO.NET](./sql/index.md)
- [Novedades de WCF Data Services 5,0](https://docs.microsoft.com/previous-versions/dotnet/wcf-data-services/ee373845(v=vs.103))
