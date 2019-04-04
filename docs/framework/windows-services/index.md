---
title: Desarrollar aplicaciones de servicios de Windows
ms.date: 03/30/2017
helpviewer_keywords:
- ServiceInstaller class, Windows Service applications
- Service class, Windows Service applications
- Windows Service applications
- Windows NT services
- ServiceProcessInstaller class, Windows Service applications
- services
- .NET applications, Windows applications
ms.assetid: ba72d648-9553-4849-b829-069ad5ea014b
author: ghogen
ms.openlocfilehash: 32aa2c1c4cd31e4591c9fa30c05ebe61058f94c5
ms.sourcegitcommit: acd8ed14fe94e9d4e3a7fb685fe83d05e941073c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/20/2019
ms.locfileid: "56442638"
---
# <a name="develop-windows-service-apps"></a>Desarrollar aplicaciones de servicios de Windows

Con Visual Studio o el SDK de .NET Framework, puede crear fácilmente servicios mediante la creación de una aplicación que se instale como un servicio. Este tipo de aplicación se denomina servicio Windows. Con las características de la plataforma, puede crear servicios, instalarlos e iniciar, detener y controlar su comportamiento.

> [!NOTE]
> En Visual Studio puede crear un servicio en código administrado en Visual C# o Visual Basic, que pueda interoperar con código C++ existente si es necesario. O bien, puede crear un servicio de Windows en C++ nativo mediante el [Asistente para proyectos ATL](/cpp/atl/reference/atl-project-wizard).

## <a name="in-this-section"></a>En esta sección

[Introducción a las aplicaciones de servicios de Windows](../../../docs/framework/windows-services/introduction-to-windows-service-applications.md)

Proporciona información general de las aplicaciones de servicio de Windows, la duración de un servicio y las diferencias entre las aplicaciones de servicio y otros tipos de proyectos comunes.

[Tutorial: Creación de una aplicación de servicios de Windows en el Diseñador de componentes](../../../docs/framework/windows-services/walkthrough-creating-a-windows-service-application-in-the-component-designer.md)

Proporciona un ejemplo de cómo crear un servicio en Visual Basic y Visual C#.

[Arquitectura de programación de aplicaciones de servicio](../../../docs/framework/windows-services/service-application-programming-architecture.md)

Explica los elementos del lenguaje utilizados en la programación de servicios.

[Cómo: Creación de servicios de Windows](../../../docs/framework/windows-services/how-to-create-windows-services.md)

Describe el proceso de creación y configuración de servicios de Windows mediante la plantilla de proyecto de servicio de Windows.

## <a name="related-sections"></a>Secciones relacionadas

<xref:System.ServiceProcess.ServiceBase>: describe las características principales de la clase <xref:System.ServiceProcess.ServiceBase>, que se utiliza para crear servicios.

<xref:System.ServiceProcess.ServiceProcessInstaller>: describe las características de la clase <xref:System.ServiceProcess.ServiceProcessInstaller>, que se utiliza junto con la clase <xref:System.ServiceProcess.ServiceInstaller> para instalar y desinstalar sus servicios.

<xref:System.ServiceProcess.ServiceInstaller>: describe las características de la clase <xref:System.ServiceProcess.ServiceInstaller>, que se utiliza junto con la clase <xref:System.ServiceProcess.ServiceProcessInstaller> para instalar y desinstalar su servicio.

[Crear proyectos a partir de plantillas](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/0fyc0azh(v=vs.120)): describe los tipos de proyectos utilizados en este capítulo y cómo elegir entre ellos.
