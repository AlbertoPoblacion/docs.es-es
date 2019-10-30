---
title: Portabilidad de .NET Framework a .NET Core
description: Comprenda el proceso de portabilidad y descubra herramientas que le pueden resultar útiles al realizar la portabilidad de un proyecto de .NET Framework a .NET Core.
author: cartermp
ms.date: 10/22/2019
ms.custom: seodec18
ms.openlocfilehash: 89f00e5c6ce7f3cea7a3135c9b2856c54a70da40
ms.sourcegitcommit: ad800f019ac976cb669e635fb0ea49db740e6890
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/29/2019
ms.locfileid: "73038530"
---
# <a name="overview-of-the-porting-process-from-net-framework-to-net-core"></a>Información general sobre el proceso de portabilidad de .NET Framework a .NET Core

Es posible que tenga código que se ejecuta actualmente en .NET Framework que le interesa portar a .NET Core. Este artículo ofrece:

* Una introducción al proceso de portabilidad.
* Una lista de las herramientas que puede encontrar de utilidad al portar el código a .NET Core.

## <a name="overview-of-the-porting-process"></a>Introducción al proceso de portabilidad

Le recomendamos que utilice el siguiente proceso al portar un proyecto a .NET Core:

1. Redirija todos los proyectos que desee portar a .NET Framework 4.7.2 o superior.

   Este paso garantiza que puede usar alternativas de API para destinos específicos de .NET Framework en los casos donde .NET Core no admite una API determinada.

2. Use el [Analizador de portabilidad de .NET](../../standard/analyzers/portability-analyzer.md) para analizar los ensamblados y ver si se pueden portar a .NET Core.

   La herramienta Analizador de portabilidad de API analiza los ensamblados compilados y genera un informe. Este informe muestra un resumen de portabilidad de alto nivel y un desglose de cada API que está usando y que no está disponible en NET Core.

3. Instale el [analizador de API de .NET](../../standard/analyzers/api-analyzer.md) en los proyectos para identificar las API que inician <xref:System.PlatformNotSupportedException> en algunas plataformas y otros posibles problemas de compatibilidad.

   Esta herramienta es similar al analizador de portabilidad, pero en lugar de analizar si las cosas se pueden basar en .NET Core, analizará si se usa una API de una forma que iniciará <xref:System.PlatformNotSupportedException> en tiempo de ejecución. Aunque esto no es habitual si va a realizar la portabilidad desde .NET Framework 4.7.2 o superior, es conveniente comprobarlo.

4. Convierta todas las dependencias de `packages.config` en el formato de [PackageReference](/nuget/consume-packages/package-references-in-project-files) con la [herramienta de conversión en Visual Studio](/nuget/consume-packages/migrate-packages-config-to-package-reference).

   Este paso implica convertir las dependencias del formato `packages.config` heredado. `packages.config` no funciona en .NET Core, por lo que esta conversión es necesaria si tiene dependencias de paquete.

5. Cree nuevos proyectos para .NET Core y copie en los archivos de código fuente, o intente convertir el archivo de proyecto existente con una herramienta.

   .NET Core usa un [formato de archivo de proyecto](../tools/csproj.md) simplificado y diferente al de .NET Framework. Deberá convertir los archivos de proyecto en este formato para continuar.

6. Porte el código de prueba.

   Dado que portar a .NET Core es un cambio tan considerable para el código base, se recomienda encarecidamente portar las pruebas de forma que pueda ejecutarlas mientras porta el código. MSTest, xUnit y NUnit funcionan en .NET Core.

Además, puede intentar portar soluciones más pequeñas o proyectos individuales en el formato de archivo de proyecto de .NET Core con la herramienta [dotnet try-convert](https://github.com/dotnet/try-convert) en una operación. No hay ninguna garantía de que `dotnet try-convert` funcione con todos los proyectos y puede provocar cambios sutiles de comportamiento de los que puede depender. Debe usarse como _punto inicial_ que automatiza los elementos básicos que se pueden automatizar. No es una solución garantizada para migrar un proyecto.

>[!div class="step-by-step"]
>[Siguiente](net-framework-tech-unavailable.md)
