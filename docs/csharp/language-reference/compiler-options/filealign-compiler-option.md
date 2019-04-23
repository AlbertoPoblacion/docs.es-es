---
title: -filealign (Opciones del compilador de C#)
ms.date: 07/20/2015
f1_keywords:
- /filealign
helpviewer_keywords:
- /alignment compiler option [C#]
- filealign compiler option [C#]
- -filealign compiler option [C#]
- /sections compiler option [C#]
- alignment compiler option [C#]
- sections compiler option [C#]
- -sections compiler option [C#]
- /filealign compiler option [C#]
- file sharing [C#]
- -alignment compiler option [C#]
- section alignment [C#]
ms.assetid: 15cf1c98-3798-4ced-9f08-60619308a073
ms.openlocfilehash: f3ce1bb864c4cb0b1c330de7d96649f9870231e8
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59328704"
---
# <a name="-filealign-c-compiler-options"></a>-filealign (Opciones del compilador de C#)
La opción **-filealign** permite especificar el tamaño de las secciones en el archivo de salida.  
  
## <a name="syntax"></a>Sintaxis  
  
```console  
-filealign:number  
```  
  
## <a name="arguments"></a>Argumentos  
 `number`  
 Un valor que especifica el tamaño de las secciones del archivo de salida. Los valores válidos son 512, 1024, 2048, 4096 y 8192. Estos valores están en bytes.  
  
## <a name="remarks"></a>Comentarios  
 Cada sección se alineará en un límite que es un múltiplo del valor **-filealign**. No hay ningún valor predeterminado fijo. Si no se especifica **-filealign**, Common Language Runtime elige un valor predeterminado en tiempo de compilación.  
  
 Al especificar el tamaño de la sección, el tamaño del archivo de salida se ve afectado. Modificar el tamaño de la sección puede ser útil para los programas que se ejecutan en dispositivos más pequeños.  
  
 Use [DUMPBIN](/cpp/build/reference/dumpbin-options) para ver información sobre las secciones en el archivo de salida.  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Para establecer esta opción del compilador en el entorno de desarrollo de Visual Studio  
  
1. Abra la página **Propiedades** del proyecto.  
  
2. Haga clic en la página de propiedades de **Compilar**.  
  
3. Haga clic en el botón **Avanzada** .  
  
4. Modifique la propiedad **Alineación de archivo**.  
  
 Para obtener información sobre cómo establecer esta opción del compilador mediante programación, vea <xref:VSLangProj80.CSharpProjectConfigurationProperties3.FileAlignment%2A>.  
  
## <a name="see-also"></a>Vea también

- [Opciones del compilador de C#](../../../csharp/language-reference/compiler-options/index.md)
- [Administrar propiedades de soluciones y proyectos](/visualstudio/ide/managing-project-and-solution-properties)
