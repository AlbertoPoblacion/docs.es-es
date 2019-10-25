---
ms.openlocfilehash: acef6d7177ee5ad7e18dc8ba1e383d6f76263623
ms.sourcegitcommit: 2e95559d957a1a942e490c5fd916df04b39d73a9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/16/2019
ms.locfileid: "72394450"
---
### <a name="signalr-javascript-client-package-name-changed"></a>SignalR: se ha cambiado el nombre del paquete de cliente de JavaScript

En ASP.NET Core 3.0, versión preliminar 7, el nombre del paquete de cliente de JavaScript de SignalR ha cambiado de `@aspnet/signalr` a `@microsoft/signalr`. El cambio de nombre refleja el hecho de que SignalR es útil más allá de las aplicaciones de ASP.NET Core, gracias a Azure SignalR Service.

Para reaccionar a este cambio, cambie las referencias en los archivos *package.json*, las instrucciones `require` y las instrucciones `import` de ECMAScript. No se cambiará ninguna API como parte de este cambio de nombre.

Para obtener información, consulte [aspnet/AspNetCore#11637](https://github.com/aspnet/AspNetCore/issues/11637).

#### <a name="version-introduced"></a>Versión introducida

3.0

#### <a name="old-behavior"></a>Comportamiento anterior

El paquete de cliente se llamaba `@aspnet/signalr`.

#### <a name="new-behavior"></a>Comportamiento nuevo

El paquete de cliente se llama `@microsoft/signalr`.

#### <a name="reason-for-change"></a>Motivo del cambio

El cambio de nombre clarifica que SignalR es útil más allá de las aplicaciones de ASP.NET Core, gracias a Azure SignalR Service.

#### <a name="recommended-action"></a>Acción recomendada

Cambie al paquete `@microsoft/signalr` nuevo.

#### <a name="category"></a>Categoría

ASP.NET Core

#### <a name="affected-apis"></a>API afectadas

None

<!-- 

#### Affected APIs

Not detectable via API analysis

-->
