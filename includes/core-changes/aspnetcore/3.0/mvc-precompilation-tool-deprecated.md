---
ms.openlocfilehash: 641233df165a1c2208a2185f2b6e99077f9a59d3
ms.sourcegitcommit: 2e95559d957a1a942e490c5fd916df04b39d73a9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/16/2019
ms.locfileid: "72394388"
---
### <a name="mvc-precompilation-tool-deprecated"></a>MVC: herramienta de precompilación en desuso

En ASP.NET Core 1.1, se presentó el paquete `Microsoft.AspNetCore.Mvc.Razor.ViewCompilation` (herramienta de precompilación MVC) para agregar compatibilidad con la compilación en tiempo de publicación de archivos Razor (archivos *.cshtml*). En ASP.NET Core 2.1, se presentó el [SDK de Razor](/aspnet/core/razor-pages/sdk?view=aspnetcore-2.1) para ampliar las características de la herramienta de precompilación. El SDK de Razor agregaba compatibilidad con los archivos Razor en tiempo de compilación y publicación. El SDK comprueba la exactitud de los archivos *.cshtml* en tiempo de compilación mientras mejora el tiempo de inicio de la aplicación. El SDK de Razor está activado de forma predeterminada y no se requiere ningún gesto para empezar a usarlo.

En ASP.NET Core 3.0, se quitó la herramienta de precompilación MVC de ASP.NET Core 1.1. Las versiones anteriores del paquete seguirán recibiendo correcciones de seguridad y de errores importantes en la versión de revisión. 

#### <a name="version-introduced"></a>Versión introducida

3.0

#### <a name="old-behavior"></a>Comportamiento anterior

El paquete `Microsoft.AspNetCore.Mvc.Razor.ViewCompilation` se usaba para compilar previamente las vistas de Razor de MVC.

#### <a name="new-behavior"></a>Comportamiento nuevo

El SDK de Razor es compatible de forma nativa con esta funcionalidad. El paquete `Microsoft.AspNetCore.Mvc.Razor.ViewCompilation` ya no está actualizado.

#### <a name="reason-for-change"></a>Motivo del cambio

El SDK de Razor proporciona más funcionalidad y comprueba la exactitud de los archivos *.cshtml* en tiempo de compilación. El SDK también mejora el tiempo de inicio de la aplicación.

#### <a name="recommended-action"></a>Acción recomendada

Para los usuarios de ASP.NET Core 2.1 o versiones posteriores, actualice para usar la compatibilidad nativa con la precompilación en el [SDK de Razor](/aspnet/core/razor-pages/sdk?view=aspnetcore-3.0). Si los errores o las características que faltan impiden la migración al SDK de Razor, abra una incidencia en [aspnet/AspNetCore](https://github.com/aspnet/AspNetCore/issues).

#### <a name="category"></a>Categoría

ASP.NET Core

#### <a name="affected-apis"></a>API afectadas

None

<!-- 

### Affected APIs

Not detectable via API analysis

-->