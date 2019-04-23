---
title: Exponer componentes COM en .NET Framework
ms.date: 03/30/2017
helpviewer_keywords:
- exposing COM components to .NET Framework
- interoperation with unmanaged code, exposing COM components
- COM interop, exposing COM components
ms.assetid: e78b14f1-e487-43cd-9c6d-1a07483f1730
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 2b7aa028afeaf4230ee079f0d4071a5cd6a21c65
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59320917"
---
# <a name="exposing-com-components-to-the-net-framework"></a>Exponer componentes COM en .NET Framework
En esta sección se resume el proceso necesario para exponer un componente COM existente a código administrado. Para obtener más detalles sobre cómo escribir servidores COM que se integren estrechamente con .NET Framework, vea [Consideraciones de diseño para interoperaciones](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/61aax4kh(v=vs.100)).
  
 Los componentes COM existentes son recursos valiosos en código administrado como aplicaciones empresariales de nivel medio o funcionalidad aislada. Un componente ideal tiene un ensamblado de interoperabilidad primario y se ajusta totalmente a los estándares de programación impuestos por COM.  
  
#### <a name="to-expose-com-components-to-the-net-framework"></a>Para exponer componentes COM en .NET Framework  
  
1. [Importe una biblioteca de tipos como un ensamblado](importing-a-type-library-as-an-assembly.md).  
  
     Common Language Runtime requiere metadatos para todos los tipos, incluidos los tipos COM. Hay varias maneras de obtener un ensamblado que contiene tipos COM importados como metadatos.  
  
2. [Use tipos COM en código administrado](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/3y76b69k(v=vs.100)).  
  
     Puede inspeccionar los tipos COM, activar instancias e invocar métodos en el objeto COM de la misma manera que lo hace para cualquier tipo administrado.  
  
3. [Compile un proyecto de interoperabilidad](compiling-an-interop-project.md).  
  
     El [!INCLUDE[winsdklong](../../../includes/winsdklong-md.md)] proporciona compiladores para varios lenguajes compatibles con Common Language Specification (CLS), incluidos [!INCLUDE[vbprvblong](../../../includes/vbprvblong-md.md)], C# y C++.  
  
4. [Implemente una aplicación de interoperabilidad](deploying-an-interop-application.md).  
  
     Las aplicaciones de interoperabilidad se implementan mejor como ensamblados firmados [con nombre seguro](../app-domains/strong-named-assemblies.md) en la caché global de ensamblados.  
  
## <a name="see-also"></a>Vea también

- [Interoperating with Unmanaged Code](index.md) (Interoperar con código no administrado)
- [Consideraciones de diseño para interoperaciones](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/61aax4kh(v=vs.100))
- [Ejemplo de interoperabilidad COM: cliente .NET y servidor COM](com-interop-sample-net-client-and-com-server.md)
- [Independencia del lenguaje y componentes independientes del lenguaje](../../standard/language-independence-and-language-independent-components.md)
- [Gacutil.exe (Herramienta Caché global de ensamblados)](../tools/gacutil-exe-gac-tool.md)
