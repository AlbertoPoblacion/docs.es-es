---
title: -unsafe (Opciones del compilador de C#)
ms.date: 04/25/2018
f1_keywords:
- /unsafe
helpviewer_keywords:
- -unsafe compiler option [C#]
- unsafe compiler option [C#]
- /unsafe compiler option [C#]
ms.openlocfilehash: 4cfd7c82bc2cbf816164b235642c0647eeb7e5b6
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59337336"
---
# <a name="-unsafe-c-compiler-options"></a>-unsafe (Opciones del compilador de C#)
La opción del compilador **-unsafe** permite la compilación de código en el que se usa la palabra clave [unsafe](../../../csharp/language-reference/keywords/unsafe.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```console  
-unsafe  
```  
  
## <a name="remarks"></a>Comentarios  
 Para obtener más información sobre el código no seguro, vea [Código no seguro y punteros](../../../csharp/programming-guide/unsafe-code-pointers/index.md).  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Para establecer esta opción del compilador en el entorno de desarrollo de Visual Studio  
  
1. Abra la página **Propiedades** del proyecto.  
  
2. Haga clic en la página de propiedades de **Compilar**.  
  
3. Active la casilla **Permitir código no seguro**.  
  
### <a name="to-add-this-option-in-a-csproj-file"></a>Para agregar esta opción en un archivo csproj

Abra el archivo .csproj de un proyecto y agregue los siguientes elementos:

```xml
  <PropertyGroup>
    <AllowUnsafeBlocks>true</AllowUnsafeBlocks>
  </PropertyGroup>
```

 Para obtener información sobre cómo establecer esta opción del compilador mediante programación, vea <xref:VSLangProj80.CSharpProjectConfigurationProperties3.AllowUnsafeBlocks%2A>.  
  
## <a name="example"></a>Ejemplo  
 Compile `in.cs` para el modo no seguro:  
  
```console  
csc -unsafe in.cs  
```  
  
## <a name="see-also"></a>Vea también

- [Opciones del compilador de C#](../../../csharp/language-reference/compiler-options/index.md)
- [Administrar propiedades de soluciones y proyectos](/visualstudio/ide/managing-project-and-solution-properties)
