---
title: Cadenas de conexión
ms.date: 12/13/2019
description: Las palabras clave admitidas y los valores de las cadenas de conexión.
ms.openlocfilehash: bb54d152bac62a86c2a49192cf678a745159164e
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/14/2020
ms.locfileid: "79401200"
---
# <a name="connection-strings"></a>Cadenas de conexión

Se utiliza una cadena de conexión para especificar cómo conectarse a la base de datos. Las cadenas de conexión de Microsoft.Data.Sqlite siguen la [sintaxis estándar de ADO.NET](../../../framework/data/adonet/connection-strings.md) como una lista separada por punto y coma de palabras clave y valores.

## <a name="keywords"></a>Palabras clave

Las siguientes palabras clave de cadena de conexión se pueden utilizar con Microsoft.Data.Sqlite:

### <a name="data-source"></a>Data Source

Ruta de acceso al archivo de base de datos. *DataSource* (sin espacio) y *Filename* son alias de esta palabra clave.

SQLite trata las rutas de acceso como relativas al directorio de trabajo actual. También se pueden especificar rutas absolutas.

Si **está vacío**, SQLite crea una base de datos temporal en disco que se elimina cuando se cierra la conexión.

Si `:memory:`, se utiliza una base de datos en memoria. Para obtener más información, consulte [Bases de datos en memoria](in-memory-databases.md).

Las rutas de acceso que comienzan con la cadena de sustitución `|DataDirectory|` se tratan igual que las rutas relativas. Si se establece, las rutas de acceso se toman como relativas al valor de la propiedad del dominio de aplicación DataDirectory.

Esta palabra clave también admite [nombres de archivo URI](https://www.sqlite.org/uri.html).

### <a name="mode"></a>Mode

El modo de conexión.

| Value           | Descripción                                                                                        |
| --------------- | -------------------------------------------------------------------------------------------------- |
| ReadWriteCreate | Abre la base de datos para leerla y escribirla y la crea si no existe. Este es el valor predeterminado. |
| ReadWrite       | Abre la base de datos para leer y escribir.                                                        |
| ReadOnly        | Abre la base de datos en modo de solo lectura.                                                              |
| Memoria          | Abre una base de datos en memoria.                                                                       |

### <a name="cache"></a>Cache

El modo de almacenamiento en caché utilizado por la conexión.

| Value   | Descripción                                                                                    |
| ------- | ---------------------------------------------------------------------------------------------- |
| Valor predeterminado | Utiliza el modo predeterminado de la biblioteca SQLite subyacente. Este es el valor predeterminado.                   |
| Privada | Cada conexión utiliza una memoria caché privada.                                                          |
| Compartido  | Las conexiones comparten una memoria caché. Este modo puede cambiar el comportamiento del bloqueo de transacciones y tablas. |

### <a name="password"></a>Password

La clave de cifrado. Cuando se especifica, se envía `PRAGMA key` inmediatamente después de abrir la conexión.

> [!WARNING]
> La contraseña no tiene ningún efecto cuando la biblioteca SQLite nativa no admite el cifrado.

### <a name="foreign-keys"></a>Foreign Keys

Valor que indica si se deben habilitar las restricciones de clave externa.

| Value   | Descripción
| ------- | --- |
| True    | Envía `PRAGMA foreign_keys = 1` inmediatamente después de abrir la conexión.
| False   | Envía `PRAGMA foreign_keys = 0` inmediatamente después de abrir la conexión.
| (vacío) | No envía `PRAGMA foreign_keys`. Este es el valor predeterminado. |

No es necesario habilitar claves externas si, como en e_sqlite3, se usó SQLITE_DEFAULT_FOREIGN_KEYS para compilar la biblioteca SQLite nativa.

### <a name="recursive-triggers"></a>Recursive triggers

Valor que indica si se deben habilitar desencadenadores recursivos.

| Value | Descripción                                                                 |
| ----- | --------------------------------------------------------------------------- |
| True  | Envía `PRAGMA recursive_triggers` inmediatamente después de abrir la conexión. |
| False | No envía `PRAGMA recursive_triggers`. Este es el valor predeterminado.              |

## <a name="connection-string-builder"></a>Creador de cadenas de conexión

Puede utilizar <xref:Microsoft.Data.Sqlite.SqliteConnectionStringBuilder> como una forma fuertemente tipada de crear cadenas de conexión. También se puede utilizar para evitar ataques de inyección de cadenas de conexión.

[!code-csharp[](../../../../samples/snippets/standard/data/sqlite/EncryptionSample/Program.cs?name=snippet_ConnectionStringBuilder)]

## <a name="examples"></a>Ejemplos

### <a name="basic"></a>Básica

Una cadena de conexión básica con una memoria caché compartida para mejorar la simultaneidad.

```ConnectionString
Data Source=Application.db;Cache=Shared
```

### <a name="encrypted"></a>Cifrados

Una base de datos cifrada.

```ConnectionString
Data Source=Encrypted.db;Password=MyEncryptionKey
```

### <a name="read-only"></a>Solo lectura

Una base de datos de solo lectura que la aplicación no puede modificar.

```ConnectionString
Data Source=Reference.db;Mode=ReadOnly
```

### <a name="in-memory"></a>En memoria

Una base de datos privada en memoria.

```ConnectionString
Data Source=:memory:
```

### <a name="sharable-in-memory"></a>Compartible en memoria

Una base de datos compartible, en memoria, identificada con el nombre *Sharable*.

```ConnectionString
Data Source=Sharable;Mode=Memory;Cache=Shared
```

## <a name="see-also"></a>Consulte también

* [Cadenas de conexión de ADO.NET](../../../framework/data/adonet/connection-strings.md)
* [Bases de datos en memoria](in-memory-databases.md)
* [Transactions](transactions.md)
