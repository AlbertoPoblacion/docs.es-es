---
title: Datos binarios y datos de valores grandes de SQL Server
ms.date: 03/30/2017
ms.assetid: e00827b3-7511-4b2d-91d7-851ca86cc6b5
ms.openlocfilehash: 4b7a3f16726d6363cd702fb912bb7be281a25000
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59192971"
---
# <a name="sql-server-binary-and-large-value-data"></a>Datos binarios y datos de valores grandes de SQL Server
SQL Server proporciona el especificador `max`, que amplía la capacidad de almacenamiento de los tipos de datos `varchar`, `nvarchar` y `varbinary`. `varchar(max)`, `nvarchar(max)`, y `varbinary(max)` se denominan colectivamente *tipos de datos de valores grandes*. Puede utilizar los tipos de datos de valores grandes para almacenar hasta 2^31-1 bytes de datos.  
  
 SQL Server 2008 incorpora el atributo FILESTREAM, que no es un tipo de datos, sino un atributo que se puede definir en una columna, y permite almacenar datos de valores grandes en el sistema de archivos en lugar de almacenarlos en la base de datos.  
  
## <a name="in-this-section"></a>En esta sección  
 [Modificación de datos de valores grandes (max) en ADO.NET](../../../../../docs/framework/data/adonet/sql/modifying-large-value-max-data.md)  
 Describe cómo trabajar con tipos de datos de valores grandes.  
  
 [Datos FILESTREAM](../../../../../docs/framework/data/adonet/sql/filestream-data.md)  
 Describe cómo trabajar con datos de valores grandes almacenados en SQL Server 2008 con el atributo FILESTREAM.  
  
## <a name="see-also"></a>Vea también

- [Tipos de datos de SQL Server y ADO.NET](../../../../../docs/framework/data/adonet/sql/sql-server-data-types.md)
- [Operaciones de datos de SQL Server en ADO.NET](../../../../../docs/framework/data/adonet/sql/sql-server-data-operations.md)
- [Recuperar y modificar datos en ADO.NET](../../../../../docs/framework/data/adonet/retrieving-and-modifying-data.md)
- [Proveedores administrados de ADO.NET y Centro para desarrolladores de DataSet](https://go.microsoft.com/fwlink/?LinkId=217917)
