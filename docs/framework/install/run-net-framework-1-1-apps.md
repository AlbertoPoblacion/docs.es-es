---
title: Ejecución de aplicaciones de .NET Framework 1.1 en Windows 8, Windows 8.1 o Windows 10
ms.date: 05/26/2017
helpviewer_keywords:
- Windows 8, running .NET Framework 1.1 apps
- .NET Framework 1.1, running on Windows 8
ms.assetid: fb14e195-fea5-4561-b9a8-60a67283edb9
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 3ad78c9a277af23eebe357ef986ea59d16bb444e
ms.sourcegitcommit: 34593b4d0be779699d38a9949d6aec11561657ec
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2019
ms.locfileid: "66833737"
---
# <a name="run-net-framework-11-apps-on-windows-8-windows-81-or-windows-10"></a>Ejecución de aplicaciones de .NET Framework 1.1 en Windows 8, Windows 8.1 o Windows 10

.NET Framework 1.1 no se admite en los sistemas operativos [!INCLUDE[win8](../../../includes/win8-md.md)], [!INCLUDE[win81](../../../includes/win81-md.md)], [!INCLUDE[winserver8](../../../includes/winserver8-md.md)], [!INCLUDE[winblue_server_2](../../../includes/winblue-server-2-md.md)] ni en Windows 10. En algunos casos, se identifica específicamente que .NET Framework 1.1 es necesario para que una aplicación se ejecute. En esos casos, debe ponerse en contacto con el fabricante de software independiente (ISV) para conseguir que la aplicación actualizada se ejecute en .NET Framework 3.5 SP1 o una versión posterior. Para más información, vea [Migrar de .NET Framework 1.1](../../../docs/framework/migration-guide/migrating-from-the-net-framework-1-1.md).

## <a name="install-the-net-framework-11-from-a-cd-or-download-center"></a>Instalación de .NET Framework 1.1 desde un CD o desde el Centro de descarga

No es posible instalar manualmente .NET Framework 1.1 en [!INCLUDE[win8](../../../includes/win8-md.md)], [!INCLUDE[win81](../../../includes/win81-md.md)], [!INCLUDE[winserver8](../../../includes/winserver8-md.md)], [!INCLUDE[winblue_server_2](../../../includes/winblue-server-2-md.md)] ni en Windows 10. Ya no se admite. Si intenta instalar el paquete, se muestra el mensaje de error siguiente: "El programa de instalación no puede continuar porque esta versión de .NET Framework no es compatible con una instalada previamente". Para solucionar este problema, instale [.NET Framework 3.5 SP1](https://www.microsoft.com/download/details.aspx?id=22). Esta versión incluye .NET Framework 2.0 (la versión siguiente a .NET Framework 1.1), que es compatible en [!INCLUDE[win8](../../../includes/win8-md.md)], [!INCLUDE[win81](../../../includes/win81-md.md)] y en Windows 10. Siempre debería intentar instalar primero la aplicación para determinar si se va a actualizar automáticamente a una versión posterior de .NET Framework. De no ser así, póngase en contacto con el ISV para obtener una actualización de la aplicación.

## <a name="see-also"></a>Vea también

- [Migración desde .NET Framework 1.1](../../../docs/framework/migration-guide/migrating-from-the-net-framework-1-1.md)
- [Instalación de .NET Framework 3.5 en Windows 10, Windows 8.1 y Windows 8](../../../docs/framework/install/dotnet-35-windows-10.md)
