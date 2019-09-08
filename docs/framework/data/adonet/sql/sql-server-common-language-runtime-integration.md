---
title: Integración con Common Language Runtime de SQL Server
ms.date: 03/30/2017
ms.assetid: c7a324c4-160d-44c2-b593-641af06eca61
ms.openlocfilehash: 77b40c6a1576b87d9bb4a7eb4b1ee3df8828b892
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/07/2019
ms.locfileid: "70780860"
---
# <a name="sql-server-common-language-runtime-integration"></a>Integración con Common Language Runtime de SQL Server
SQL Server 2005 introdujo la integración del componente Common Language Runtime (CLR) de .NET Framework para Microsoft Windows. Esto significa que ahora se pueden escribir procedimientos almacenados, desencadenadores, tipos definidos por el usuario, funciones definidas por el usuario, agregados definidos por el usuario y funciones con valores de tabla de transmisión por secuencias mediante cualquier lenguaje de .NET Framework, como Microsoft Visual Basic .NET y Microsoft Visual C#. El espacio de nombres <xref:Microsoft.SqlServer.Server> contiene un conjunto de nuevas interfaces de programación de aplicaciones (API) que permiten que el código administrado interactúe con el entorno de Microsoft SQL Server.  
  
 En esta sección se describen las características y comportamientos que son específicos de la integración Common Language Runtime (CLR) de SQL Server, así como las extensiones específicas en proceso de SQL Server a ADO.NET.  
  
 El objetivo de esta sección es proporcionar suficiente información para iniciarse en la programación con la integración CLR de SQL Server; no pretende tratar el tema en toda su extensión. Para obtener información más detallada, busque la versión de SQL Server que utiliza en los Libros en pantalla de SQL Server.  
  
 **Libros en pantalla de SQL Server**  
  
1. [Conceptos de programación de la integración con Common Language Runtime (CLR)](https://go.microsoft.com/fwlink/?LinkId=115240)  
  
## <a name="in-this-section"></a>En esta sección  
 [Introducción a la integración con CLR de SQL Server](introduction-to-sql-server-clr-integration.md)  
 Proporciona una introducción a la integración CLR de SQL Server. También proporciona vínculos a temas adicionales.  
  
 [Funciones definidas por el usuario de CLR](clr-user-defined-functions.md)  
 Describe cómo implementar y utilizar los diferentes tipos de funciones CLR: con valores de tabla, escalares y funciones de agregado definidas por el usuario.  
  
 [Tipos CLR definidos por el usuario](clr-user-defined-types.md)  
 Describe cómo implementar y utilizar tipos definidos por el usuario CLR. También proporciona vínculos a temas adicionales.  
  
 [Procedimientos almacenados de CLR](clr-stored-procedures.md)  
 Describe cómo implementar y utilizar procedimientos almacenados CLR. También proporciona vínculos a temas adicionales.  
  
 [Desencadenadores de CLR](clr-triggers.md)  
 Describe cómo implementar y utilizar desencadenadores CLR. También proporciona vínculos a temas adicionales.  
  
 [Conexión del contexto](the-context-connection.md)  
 Describe la conexión de contexto.  
  
 [Comportamiento específico en proceso de SQL Server en ADO.NET](sql-server-in-process-specific-behavior-of-adonet.md)  
 Describe las extensiones específicas en proceso de SQL Server a ADO.NET, y la conexión de contexto. También proporciona vínculos a temas adicionales.  
  
## <a name="see-also"></a>Vea también

- [SQL Server y ADO.NET](index.md)
- [Información general sobre ADO.NET](../ado-net-overview.md)
