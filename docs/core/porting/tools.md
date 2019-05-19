---
title: Herramientas para la portabilidad a .NET Core
description: Más información sobre algunas de las herramientas que puede usar para realizar la portabilidad a .NET Core
author: cartermp
ms.author: mairaw
ms.date: 12/07/2018
ms.openlocfilehash: d0b74b5708f31922b72fa0e236c8bbe69ae06217
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/15/2019
ms.locfileid: "65632246"
---
# <a name="tools-to-help-with-porting-to-net-core"></a>Herramientas útiles para la portabilidad a .NET Core

Las herramientas enumeradas en este artículo pueden ser útiles cuando realice la portabilidad:

* [Analizador de portabilidad de .NET](../../standard/analyzers/portability-analyzer.md), una cadena de herramientas que puede generar un informe de portabilidad del código entre .NET Framework y .NET Core:  como [herramienta de línea de comandos](https://github.com/Microsoft/dotnet-apiport/releases) como [extensión de Visual Studio](https://visualstudiogallery.msdn.microsoft.com/1177943e-cfb7-4822-a8a6-e56c7905292b)
* [Analizador de API en .NET](../../standard/analyzers/api-analyzer.md): un analizador de Roslyn que detecta posibles riesgos de compatibilidad de las API de C# en distintas plataformas y detecta llamadas a API en desuso.

Además, puede intentar portar soluciones más pequeñas o proyectos individuales en el formato de archivo de proyecto de .NET Core con la herramienta [CsprojToVs2017](https://github.com/hvanbakel/CsprojToVs2017).

> [!WARNING] 
> CsprojToVs2017 es una herramienta de terceros. No hay ninguna garantía de que funcione con todos los proyectos, y podría provocar cambios sutiles de comportamiento de los que dependa. CsprojToVs2017 debe usarse como _punto de partida_ que automatiza los elementos básicos que se pueden automatizar. No es una solución que se garantice para migrar formatos de archivo de proyecto.
