---
title: Publicación de un paquete NuGet
description: Procedimientos recomendados para publicar bibliotecas de .NET en NuGet.
author: jamesnk
ms.author: mairaw
ms.date: 10/02/2018
ms.openlocfilehash: 9c8442b52ed2c54d2fb3368a2e886c5fc2b19148
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/15/2019
ms.locfileid: "65640770"
---
# <a name="publishing-a-nuget-package"></a>Publicación de un paquete NuGet

Los paquetes NuGet se publican y consumen desde repositorios de paquetes. Aunque NuGet.org es el repositorio más conocido y utilizado, hay muchos lugares para publicar paquetes NuGet:

* **[NuGet.org](https://www.nuget.org/)** es el repositorio en línea principal para paquetes NuGet. Todos los paquetes de NuGet.org están públicamente disponibles para todo el mundo. De forma predeterminada, Visual Studio tiene NuGet.org como origen del paquete y, para muchos desarrolladores, NuGet.org es el único repositorio de paquetes con el que interactuarán. NuGet.org es el mejor lugar para publicar paquetes estables y paquetes de versión preliminar en los que desea incluir comentarios de la comunidad.

* **[MyGet](https://myget.org/)** es un servicio de repositorio que admite fuentes de paquete personalizadas para proyectos de código abierto. Una fuente personalizada pública de MyGet es un lugar ideal para publicar paquetes de versión preliminar creados por su servicio de integración continua. MyGet también proporciona fuentes privadas de forma comercial.

* Una **[fuente local](/nuget/hosting-packages/local-feeds)** le permite tratar una carpeta como un repositorio de paquetes y hace que se pueda obtener acceso a los archivos `*.nupkg` de la carpeta mediante NuGet. Una fuente local es útil para probar un paquete NuGet antes de publicarlo en NuGet.org.

> [!NOTE]
> NuGet.org [no permite que se elimine un paquete](/nuget/policies/deleting-packages) una vez cargado este. Se puede quitar de la lista un paquete para que no esté visible en la interfaz de usuario, pero aún puede descargarse `*.nupkg` en la restauración. Además, nuget.org no permite versiones de paquetes duplicadas. Para corregir un paquete NuGet con un error, debe quitar de la lista el paquete incorrecto, aumentar el número de versión y publicar una nueva versión del paquete.

**✔️ HACER** [publique en NuGet.org paquetes estables y paquetes de versión preliminar](/nuget/create-packages/publish-a-package) en los que desee incluir comentarios de la comunidad.

**✔️ CONSIDERAR** publicación de paquetes de versión preliminar en una fuente de MyGet desde una compilación de integración continua.

**✔️ CONSIDERAR** prueba de paquetes en su entorno de desarrollo con una fuente local o MyGet. Compruebe que funciona el paquete y, a continuación, publíquelo en NuGet.org.

## <a name="nugetorg-security"></a>Seguridad de NuGet.org

Es importante que los actores malos no puedan tener acceso a su cuenta NuGet ni cargar una versión malintencionada de su biblioteca. NuGet.org ofrece autenticación en dos fases y notificaciones por correo electrónico al publicarse un paquete. Habilite estas características después de iniciar sesión en NuGet.org en la página **Configuración de cuenta**.

![alt text](./media/publish-nuget-package/nuget-2fa.png "Seguridad de la cuenta NuGet")

**✔️ HACER** use una cuenta Microsoft para iniciar sesión en NuGet.

**✔️ HACER** habilite la autenticación en dos fases para tener acceso a NuGet.

**✔️ HACER** habilite la notificación por correo electrónico al publicarse un paquete.

>[!div class="step-by-step"]
>[Anterior](sourcelink.md)
>[Siguiente](versioning.md)
