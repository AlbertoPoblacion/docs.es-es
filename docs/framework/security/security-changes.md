---
title: Cambios de seguridad en .NET Framework
ms.date: 03/30/2017
helpviewer_keywords:
- Allow Partially Trusted Callers attribute
- .NET Framework 4, security changes
- .NET Framework security
- security-transparent code
- security-critical code
- code access security, changes
ms.assetid: 5e87881c-9c13-4b52-8ad1-e34bb46e8aaa
author: mairaw
ms.author: mairaw
ms.openlocfilehash: af2869e5ca3b41778c094b7a78a9493e74868811
ms.sourcegitcommit: 81ad1f09b93f3b3e6706a7f2e4ddf50ef229ea3d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2019
ms.locfileid: "74204503"
---
# <a name="security-changes-in-the-net-framework"></a>Cambios de seguridad en .NET Framework

El cambio más importante en la seguridad de la .NET Framework 4,5 es con un nombre seguro. Consulte [Enhanced Strong Naming](../../standard/assembly/enhanced-strong-naming.md) para obtener una descripción de estos cambios.  
  
.NET Framework proporciona un modelo de seguridad de dos niveles para las aplicaciones administradas. Las aplicaciones de la tienda Windows 8. x se ejecutan en un contenedor de seguridad de Windows que limita el acceso a los recursos. Dentro de ese contenedor, la ejecución de las aplicaciones administradas es de plena confianza. Desde la perspectiva de la seguridad de acceso del código (CAS), no hay nada que un desarrollador pueda hacer para elevar los privilegios. Para obtener información sobre los privilegios concedidos por Windows, consulte [Declaraciones de funcionalidades de las aplicaciones (aplicaciones de la Tienda Windows)](https://go.microsoft.com/fwlink/?LinkId=230436) en el Centro de desarrollo de Windows. Para obtener información sobre cómo crear una aplicación de la tienda Windows 8. x, consulte [crear la primera C# aplicación de la tienda windows con o Visual Basic](https://go.microsoft.com/fwlink/?LinkId=230461).
