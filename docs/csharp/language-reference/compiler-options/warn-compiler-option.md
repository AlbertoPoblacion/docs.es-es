---
title: -warn (Opciones del compilador de C#)
ms.date: 07/20/2015
f1_keywords:
- /warn
helpviewer_keywords:
- warning level [C#]
- /w compiler option [C#]
- -w compiler option [C#]
- -warn compiler option [C#]
- /warn compiler option [C#]
- w compiler option [C#]
- warn compiler option [C#]
ms.assetid: 5f80ff59-4991-4382-9f9a-77da18446e71
ms.openlocfilehash: 17dd992edbec5ce444b53ed42b2b486282618672
ms.sourcegitcommit: 558d78d2a68acd4c95ef23231c8b4e4c7bac3902
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/09/2019
ms.locfileid: "59315808"
---
# <a name="-warn-c-compiler-options"></a>-warn (Opciones del compilador de C#)
La opción **-warn** especifica el nivel de advertencia que debe mostrar el compilador.  
  
## <a name="syntax"></a>Sintaxis  
  
```console  
-warn:option  
```  
  
## <a name="arguments"></a>Argumentos  
 `option`  
 El nivel de advertencia que se quiere mostrar para la compilación: los números más bajos solo muestran advertencias de gravedad alta; los más altos muestran más advertencias. Los valores válidos son 0 a 4:  
  
|Nivel de advertencia|Significado|  
|-------------------|-------------|  
|0|Desactiva la emisión de todos los mensajes de advertencia.|  
|1|Muestra mensajes de advertencia graves.|  
|2|Muestra advertencias de nivel 1 además de determinadas advertencias menos graves, como advertencias sobre ocultar miembros de clase.|  
|3|Muestra advertencias de nivel 2 además de determinadas advertencias menos graves, como advertencias sobre expresiones que siempre se evalúan como `true` o `false`.|  
|4 (el valor predeterminado)|Muestra todas las advertencias de nivel 3 además de advertencias informativas.|  
  
## <a name="remarks"></a>Comentarios  
 Para obtener información sobre un error o advertencia, puede buscar el código de error en el Índice de la Ayuda. Para conocer otras maneras de obtener información sobre un error o advertencia, vea [Errores del compilador de C#](../../../csharp/language-reference/compiler-messages/index.md).  
  
 Use [-warnaserror](../../../csharp/language-reference/compiler-options/warnaserror-compiler-option.md) para tratar todas las advertencias como errores. Use [-nowarn](../../../csharp/language-reference/compiler-options/nowarn-compiler-option.md) para deshabilitar determinadas advertencias.  
  
 **-w** es la forma abreviada de **-warn**.  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Para establecer esta opción del compilador en el entorno de desarrollo de Visual Studio  
  
1. Abra la página **Propiedades** del proyecto.  
  
2. Haga clic en la página de propiedades de **Compilar**.  
  
3. Modifique la propiedad de **Nivel de advertencia**.  
  
 Para obtener información sobre cómo establecer esta opción del compilador mediante programación, vea <xref:VSLangProj80.CSharpProjectConfigurationProperties3.WarningLevel%2A>.  
  
## <a name="example"></a>Ejemplo  
 Compile `in.cs` y haga que el compilador solo muestre advertencias de nivel 1:  
  
```console  
csc -warn:1 in.cs  
```  
  
## <a name="see-also"></a>Vea también

- [Opciones del compilador de C#](../../../csharp/language-reference/compiler-options/index.md)
- [Administrar propiedades de soluciones y proyectos](/visualstudio/ide/managing-project-and-solution-properties)
