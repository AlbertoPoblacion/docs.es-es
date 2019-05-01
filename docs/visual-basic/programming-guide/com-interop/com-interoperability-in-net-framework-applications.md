---
title: Interoperabilidad COM en aplicaciones .NET Framework (Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- interoperability, COM and .NET framework objects
- COM interop [Visual Basic]
- shared components
ms.assetid: f5a72143-c268-4dff-a019-974ad940e17d
ms.openlocfilehash: 6e8b4eba40cc1872cb289ca120679bb951f2652a
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62022389"
---
# <a name="com-interoperability-in-net-framework-applications-visual-basic"></a>Interoperabilidad COM en aplicaciones .NET Framework (Visual Basic)

Cuando desea utilizar objetos COM y objetos de .NET Framework en la misma aplicación, deberá abordar las diferencias en cómo los objetos existen en la memoria. Un objeto de .NET Framework se encuentra en la memoria administrada, la memoria controlada por common language runtime y puede moverse por el tiempo de ejecución según sea necesario. Un objeto COM se encuentra en la memoria no administrada y no se espera que mover a otra ubicación de memoria. Visual Studio y el [!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)] proporcionan herramientas para controlar la interacción de estos administrados y los componentes. Para obtener más información sobre el código administrado, consulte [Common Language Runtime](../../../standard/clr.md).

Además de usar objetos COM en aplicaciones. NET, también puede usar Visual Basic para desarrollar objetos accesibles desde código no administrado a través de COM.

Los vínculos de esta página proporcionan detalles sobre las interacciones entre los objetos COM y .NET Framework.

## <a name="related-sections"></a>Secciones relacionadas

| | |
|---------|---------|
| [Interoperabilidad COM](../../../visual-basic/programming-guide/com-interop/index.md) | Proporciona vínculos a temas que tratan sobre la interoperabilidad COM en Visual Basic, incluidos objetos de COM, controles de ActiveX, los archivos DLL Win32, los objetos administrados y herencia de objetos COM. |
| [Interoperating with Unmanaged Code](../../../framework/interop/index.md) (Interoperar con código no administrado) | Algunos de los problemas de interacción entre código administrado y describe brevemente y proporciona vínculos para más información al respecto. |
| [Contenedores COM](../../../framework/interop/com-wrappers.md) | Describe contenedores RCW, que permiten al código administrado llamar a métodos COM, y contenedores COM invocables, que permiten a los clientes COM llamar a métodos del objeto. NET. |
| [Interoperabilidad COM avanzada](../../../framework/interop/index.md) | Proporciona vínculos a temas que tratan sobre la interoperabilidad COM con respecto a los contenedores, excepciones, herencia, subprocesos, eventos, conversiones y cálculo de referencias. |
| [TlbImp.exe (Importador de la biblioteca de tipos)](../../../framework/tools/tlbimp-exe-type-library-importer.md) | Describe la herramienta que puede usar para convertir las definiciones de tipo que se encuentran en una biblioteca de tipos COM en las definiciones equivalentes en un ensamblado de common language runtime. |