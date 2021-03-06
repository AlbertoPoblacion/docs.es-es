---
title: ¿Qué&#39;s nuevas en ADO.NET
ms.date: 03/30/2017
ms.assetid: 3bb65d38-cce2-46f5-b979-e5c505e95e10
ms.openlocfilehash: cfb1546ccddc6a4f6f3668210832db3d7a88f632
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/23/2019
ms.locfileid: "54501600"
---
# <a name="what39s-new-in-adonet"></a>¿Qué&#39;s nuevas en ADO.NET
Las siguientes características son nuevas en [!INCLUDE[vstecado](../../../../includes/vstecado-md.md)] en [!INCLUDE[net_v45](../../../../includes/net-v45-md.md)].  
  
## <a name="sqlclient-data-provider"></a>Proveedor de datos SqlClient  
 Las siguientes características son nuevas en el [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] proveedor de datos para SQL Server en [!INCLUDE[net_v45](../../../../includes/net-v45-md.md)]:  
  
-   Las palabras clave de cadena de conexión ConnectRetryCount y ConnectRetryInterval (<xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A>) permiten controlar la característica de resistencia de conexión inactiva.  
  
-   Compatibilidad con Streaming desde SQL Server a una aplicación es compatible con escenarios donde los datos en el servidor no están estructurados.  Consulte [compatibilidad con Streaming de SqlClient](../../../../docs/framework/data/adonet/sqlclient-streaming-support.md) para obtener más información.  
  
-   Se ha agregado compatibilidad con programación asincrónica.  Consulte [programación asincrónica](../../../../docs/framework/data/adonet/asynchronous-programming.md) para obtener más información.  
  
-   Los errores de conexión se guardarán ahora en el registro de eventos extendidos. Para obtener más información, consulte [Traza de datos en ADO.NET](../../../../docs/framework/data/adonet/data-tracing.md).  
  
-   SqlClient ahora es compatible con alta disponibilidad de SQL Server, característica de recuperación ante desastres AlwaysOn. Para obtener más información, consulte [compatibilidad de SqlClient para alta disponibilidad y recuperación ante desastres](../../../../docs/framework/data/adonet/sql/sqlclient-support-for-high-availability-disaster-recovery.md).  
  
-   Se puede pasar una contraseña como un <xref:System.Security.SecureString> cuando se usa la autenticación de SQL Server. Vea <xref:System.Data.SqlClient.SqlCredential> para obtener más información.  
  
-   Cuando `TrustServerCertificate` es false y `Encrypt` es true, el nombre del servidor (o dirección IP) en un certificado SSL de SQL Server debe coincidir exactamente con el nombre de servidor (o dirección IP) especificado en la cadena de conexión. De lo contrario, se producirá un error en el intento de conexión. Para obtener más información, vea la descripción de la opción de conexión `Encrypt` en <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A>.  
  
     Si este cambio hace que una aplicación existente ya no pueda conectarse, puede corregir la aplicación usando uno de los siguientes:  
  
    -   Emita un certificado que especifique el nombre corto en el campo Nombre común (CN) o Nombre alternativo del sujeto (SAN). Esta solución funcionará para la creación de reflejo de la base de datos.  
  
    -   Agregue un alias que asigne el nombre corto al nombre de dominio completo.  
  
    -   Use el nombre de dominio completo en la cadena de conexión.  
  
-   SqlClient admite Protección ampliada. Para obtener más información acerca de la protección ampliada, vea [conectarse a la base de datos de motor con protección ampliada](https://go.microsoft.com/fwlink/?LinkId=219978).  
  
-   SqlClient admite conexiones a bases de datos LocalDB. Para obtener más información, consulte [compatibilidad de SqlClient para LocalDB](../../../../docs/framework/data/adonet/sql/sqlclient-support-for-localdb.md).  
  
-   `Type System Version=SQL Server 2012;` es el nuevo valor para pasar a la propiedad de conexión `Type System Version`. El valor `Type System Version=Latest;` ahora está obsoleto y se ha hecho equivalente a `Type System Version=SQL Server 2008;`. Para obtener más información, consulta <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A>.  
  
-   SqlClient proporciona compatibilidad adicional para columnas dispersas, una característica que se agregó en SQL Server 2008. Si su aplicación ya tiene acceso a datos de una tabla que usa columnas dispersas, debería ver un aumento del rendimiento. La columna IsColumnSet de <xref:System.Data.SqlClient.SqlDataReader.GetSchemaTable%2A> indica si una columna es una columna dispersa que es miembro de un conjunto de columnas. <xref:System.Data.SqlClient.SqlConnection.GetSchema%2A> indica si una columna es una columna dispersa (vea [colecciones de esquemas de SQL Server](../../../../docs/framework/data/adonet/sql-server-schema-collections.md) para obtener más información). Para obtener más información sobre las columnas dispersas, vea [usar columnas dispersas](https://go.microsoft.com/fwlink/?LinkId=224244).  
  
-   El ensamblado Microsoft.SqlServer.Types.dll, que contiene los tipos de datos espaciales, se ha actualizado de la versión 10.0 a la versión 11.0. Las aplicaciones que hacen referencia a este ensamblado pueden producir errores. Para obtener más información, consulte [cambios recientes en las características del motor de base de datos](https://go.microsoft.com/fwlink/?LinkId=224367).  
  
## <a name="adonet-entity-framework"></a>ADO.NET Entity Framework  
 [!INCLUDE[net_v45](../../../../includes/net-v45-md.md)] agrega las API que permiten nuevos escenarios al trabajar con Entity Framework 5.0. Para obtener más información sobre las mejoras y características que se agregaron a Entity Framework 5.0, consulte los temas siguientes: [¿Qué novedades](https://go.microsoft.com/fwlink/?LinkID=251106) y [versiones de Entity Framework y control de versiones](https://go.microsoft.com/fwlink/?LinkId=234899).  
  
## <a name="see-also"></a>Vea también
- [ADO.NET](../../../../docs/framework/data/adonet/index.md)
- [Información general sobre ADO.NET](../../../../docs/framework/data/adonet/ado-net-overview.md)
- [SQL Server y ADO.NET](../../../../docs/framework/data/adonet/sql/index.md)
- [Novedades de Servicios de datos de WCF](https://msdn.microsoft.com/library/cf22cad5-b8d9-472b-8d7c-b863b64eaae8)
- [Proveedores administrados de ADO.NET y Centro para desarrolladores de DataSet](https://go.microsoft.com/fwlink/?LinkId=217917)
