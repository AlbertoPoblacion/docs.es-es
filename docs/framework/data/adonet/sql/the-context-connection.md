---
title: Conexión del contexto
ms.date: 03/30/2017
ms.assetid: e443ca86-9243-4234-a822-ed10a53a9de0
ms.openlocfilehash: 83e9f4a9672d2703514c0a86ad8d41b968c255fd
ms.sourcegitcommit: 558d78d2a68acd4c95ef23231c8b4e4c7bac3902
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/09/2019
ms.locfileid: "59343446"
---
# <a name="the-context-connection"></a>Conexión del contexto
El problema de acceso a los datos internos es una situación bastante común. Es decir, desea tener acceso al mismo servidor en el que se ejecuta el procedimiento almacenado o la función de Common Language Runtime (CLR). Una opción es crear una conexión mediante <xref:System.Data.SqlClient.SqlConnection>, especificar una cadena de conexión que apunte al servidor local y abrir la conexión. Esto requiere especificar las credenciales para iniciar sesión. La conexión está en una sesión de base de datos distinta que el procedimiento almacenado o función, puede tener opciones `SET` distintas, está en una transacción aparte, no ve las tablas temporales, etc. Si el código administrado del procedimiento almacenado o función se ejecuta en el proceso de SQL Server, es porque alguien se ha conectado a ese servidor y ha ejecutado una instrucción SQL para invocarlo. Probablemente desea que el procedimiento almacenado o función se ejecute en el contexto de esa conexión, junto con su transacción, opciones `SET`, etc. Esto se conoce como conexión de contexto.  
  
 La conexión de contexto permite ejecutar instrucciones Transact-SQL en el mismo contexto que el código que se ha invocado en el primer sitio. Para obtener información más detallada, busque la versión de SQL Server que utiliza en los Libros en pantalla de SQL Server.  
  
 **Libros en pantalla de SQL Server**  
  
1. [Conexión del contexto](https://go.microsoft.com/fwlink/?LinkId=115395)  
  
## <a name="see-also"></a>Vea también

- [Proveedores administrados de ADO.NET y centro de desarrolladores de DataSet](https://go.microsoft.com/fwlink/?LinkId=217917)
