---
title: Funciones del sistema
ms.date: 03/30/2017
ms.assetid: b7c71b58-09e6-44ce-a3e5-a0fdb892fb86
ms.openlocfilehash: 552f374bc1824a16fb323cd19abe79c1914295a7
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2019
ms.locfileid: "70248234"
---
# <a name="system-functions"></a>Funciones del sistema
El Proveedor de datos .NET Framework para SQL Server (SqlClient) proporciona las funciones del sistema siguientes:  
  
|Función|DESCRIPCIÓN|  
|--------------|-----------------|  
|`CHECKSUM (` `value`, [`value`, [`value`]]`)`|Devuelve el valor de suma. `CHECKSUM` se ha pensado para utilizarlo en la compilación de índices hash.<br /><br /> **Argumentos**<br /><br /> `value`: `Boolean`, ,`Byte` ,,`Int64`, ,`String`,,,, O`Guid`. `Single` `Decimal` `Double` `DateTime` `Int16` `Int32` `Binary` Puede especificar uno, dos o tres valores.<br /><br /> **Valor devuelto**<br /><br /> Valor absoluto de la expresión especificada.<br /><br /> **Ejemplo**<br /><br /> `SqlServer.CHECKSUM(10,100,1000.0)`|  
|`CURRENT_TIMESTAMP ()`|Genera la fecha actual y la hora en el formato interno de SQL Server para los valores `DateTime` con una precisión de 7 en SQL Server 2008 y una precisión de 3 en SQL Server 2005.<br /><br /> **Valor devuelto**<br /><br /> La fecha y la hora actuales del sistema como un `DateTime`.<br /><br /> **Ejemplo**<br /><br /> `SqlServer.CURRENT_TIMESTAMP()`|  
|`CURRENT_ USER``()`|Devuelve el nombre del usuario actual.<br /><br /> **Valor devuelto**<br /><br /> Valor de tipo `String` ASCII.<br /><br /> **Ejemplo**<br /><br /> `SqlServer.CURRENT_USER()`|  
|`DATALENGTH` `(` `expression` `)`|Devuelve el número de bytes utilizados para representar cualquier expresión.<br /><br /> **Argumentos**<br /><br /> `expression`: `Boolean` ,`Byte`, ,`Int32`, ,`Single`, ,`String`,,,,, O`Binary` `DateTime` `Double` `Int64` `Decimal` `Int16` `Time` `DateTimeOffset` `Guid`.<br /><br /> **Valor devuelto**<br /><br /> Tamaño de las propiedades en forma de un valor `Int32`.<br /><br /> **Ejemplo**<br /><br /> `SELECT VALUE SqlServer.DATALENGTH(P.Name)FROM`<br /><br /> `AdventureWorksEntities.Product AS P`|  
|`HOST_NAME()`|Devuelve el nombre de la estación de trabajo.<br /><br /> **Valor devuelto**<br /><br /> Valor de tipo `String` Unicode.<br /><br /> **Ejemplo**<br /><br /> `SqlServer.HOST_NAME()`|  
|`ISDATE(` `expression` `)`|Determina si una expresión de entrada es una fecha válida.<br /><br /> **Argumentos**<br /><br /> `expression`: `Boolean` ,`Byte`, ,`Int32`, ,`Single`, ,`String`,,,,, O`Binary` `DateTime` `Double` `Int64` `Decimal` `Int16` `Time` `DateTimeOffset` `Guid`.<br /><br /> **Valor devuelto**<br /><br /> Una clase `Int32`. Uno (1) si la expresión de entrada es una fecha válida. De lo contrario, es cero (0).<br /><br /> **Ejemplo**<br /><br /> `SqlServer.ISDATE('1/1/2006')`|  
|`ISNUMERIC(` `expression` `)`|Determina si una expresión es de un tipo numérico válido.<br /><br /> **Argumentos**<br /><br /> `expression`: `Boolean` ,`Byte`, ,`Int32`, ,`Single`, ,`String`,,,,, O`Binary` `DateTime` `Double` `Int64` `Decimal` `Int16` `Time` `DateTimeOffset` `Guid`.<br /><br /> **Valor devuelto**<br /><br /> Una clase `Int32`. Uno (1) si la expresión de entrada es una fecha válida. De lo contrario, es cero (0).<br /><br /> **Ejemplo**<br /><br /> `SqlServer.ISNUMERIC('21')`|  
|`NEWID()`|Crea un valor único de tipo Guid.<br /><br /> **Valor devuelto**<br /><br /> Objeto `Guid`.<br /><br /> **Ejemplo**<br /><br /> `SqlServer.NEWID()`|  
|`USER_NAME(` `id` `)`|Devuelve un nombre de usuario de base de datos a partir de un número de identificación especificado.<br /><br /> **Argumentos**<br /><br /> `expression`: Número de identificación `Int32` asociado al usuario de una base de datos.<br /><br /> **Valor devuelto**<br /><br /> Valor de tipo `String` Unicode.<br /><br /> **Ejemplo**<br /><br /> `SqlServer.USER_NAME(0)`|  
  
 Para obtener más información sobre las funciones de cadena que SqlClient admite, consulte la documentación de la versión de SQL Server que especificó en el manifiesto del proveedor SqlClient:  
  
|SQL Server 2000|SQL Server 2005|SQL Server 2008|  
|---------------------|---------------------|---------------------|  
|[Funciones del sistema Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=115918)|[Funciones del sistema Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=115917)|[Funciones del sistema (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=115919)|  
  
## <a name="see-also"></a>Vea también

- [Lenguaje Entity SQL](./language-reference/entity-sql-language.md)
- [SqlClient para las funciones de Entity Framework](sqlclient-for-ef-functions.md)
