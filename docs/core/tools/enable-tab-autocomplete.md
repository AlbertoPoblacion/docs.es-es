---
title: Habilitación de la finalización con tabulación
description: En este artículo se describe cómo habilitar la finalización con tabulación para la CLI de .NET Core para PowerShell, Bash y zsh.
author: thraka
ms.author: adegeo
ms.date: 12/17/2018
ms.openlocfilehash: 0f29ba2ef1d419339a0e2dc44f67c93b326eb40d
ms.sourcegitcommit: 55f438d4d00a34b9aca9eedaac3f85590bb11565
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/23/2019
ms.locfileid: "71182464"
---
# <a name="how-to-enable-tab-completion-for-net-core-cli"></a>Cómo habilitar la finalización con tabulación para la CLI de .NET Core

A partir del SDK de .NET Core 2.0, la CLI de .NET Core admite la finalización con tabulación. En este artículo se describe cómo configurar la finalización con tabulación para tres shells: PowerShell, Bash y zsh. Otros shells pueden tener compatibilidad con la finalización automática. Consulte su documentación sobre cómo configurar la finalización automática, los pasos deben ser similares a los que se describen en este artículo.

[!INCLUDE [topic-appliesto-net-core-2plus](~/includes/topic-appliesto-net-core-2plus.md)]

Una vez configurada, para desencadenar la finalización con tabulación para la CLI de .NET Core, escriba un comando `dotnet` en el shell y, después, presione el tabulador. La línea de comandos que se envía al comando `dotnet complete` y los resultados se procesan mediante el shell. Puede probar los resultados sin habilitar la finalización con tabulación si envía algo directamente al comando `dotnet complete`. Por ejemplo:

```console
> dotnet complete "dotnet a"
add
clean
--diagnostics
migrate
pack
```

Si ese comando no funciona, asegúrese de que está instalado el SDK de .NET Core 2.0 o una versión superior. Si está instalado, pero el comando sigue sin funcionar, asegúrese de que `dotnet` se resuelva como mínimo en la versión 2.0 del SDK de .NET Core. Use el comando `dotnet --version` para ver en qué versión de `dotnet` se resuelve la ruta de acceso actual. Para obtener más información, vea [Selección de la versión de .NET Core que se va a usar](../versions/selection.md).

### <a name="examples"></a>Ejemplos

Estos son algunos ejemplos de lo que proporciona la finalización con tabulación:

Entrada                                | se convierte en                                                                     | porque
:------------------------------------|:----------------------------------------------------------------------------|:--------------------------------
`dotnet a⇥`                          | `dotnet add`                                                                 | `add` es el primer subcomando, por orden alfabético.
`dotnet add p⇥`                      | `dotnet add --help`                                                          | La finalización con tabulación hace coincidir las subcadenas y `--help` aparece primero alfabéticamente.
`dotnet add p⇥⇥`                    | `dotnet add package`                                                          | Al presionar la tecla Tab una segunda vez aparece la siguiente sugerencia.      
`dotnet add package Microsoft⇥`      | `dotnet add package Microsoft.ApplicationInsights.Web`                      | Los resultados se devuelven por orden alfabético.
`dotnet remove reference ⇥`          | `dotnet remove reference ..\..\src\OmniSharp.DotNet\OmniSharp.DotNet.csproj` | La finalización con tabulación es compatible con archivos de proyecto.

## <a name="powershell"></a>PowerShell

Para agregar finalización con tabulación a **PowerShell** para la CLI de .NET Core, cree o edite el perfil almacenado en la variable `$PROFILE`. Para obtener más información, vea [Cómo crear el perfil](/powershell/module/microsoft.powershell.core/about/about_profiles#how-to-create-a-profile) y [Los perfiles y la directiva de ejecución](/powershell/module/microsoft.powershell.core/about/about_profiles#profiles-and-execution-policy). 

Agregue el código siguiente al perfil:

```powershell
# PowerShell parameter completion shim for the dotnet CLI 
Register-ArgumentCompleter -Native -CommandName dotnet -ScriptBlock {
     param($commandName, $wordToComplete, $cursorPosition)
         dotnet complete --position $cursorPosition "$wordToComplete" | ForEach-Object {
            [System.Management.Automation.CompletionResult]::new($_, $_, 'ParameterValue', $_)
         }
 }
```

## <a name="bash"></a>Bash

Para agregar finalización con tabulación al shell de **bash** para la CLI de .NET Core, agregue el código siguiente al archivo `.bashrc`:

```bash
# bash parameter completion for the dotnet CLI

_dotnet_bash_complete()
{
  local word=${COMP_WORDS[COMP_CWORD]}

  local completions
  completions="$(dotnet complete --position "${COMP_POINT}" "${COMP_LINE}")"

  COMPREPLY=( $(compgen -W "$completions" -- "$word") )
}

complete -f -F _dotnet_bash_complete dotnet
```

## <a name="zsh"></a>Zsh

Para agregar finalización con tabulación al shell de **zsh** para la CLI de .NET Core, agregue el código siguiente al archivo `.zshrc`:

```zsh
# zsh parameter completion for the dotnet CLI

_dotnet_zsh_complete() 
{
  local completions=("$(dotnet complete "$words")")

  reply=( "${(ps:\n:)completions}" )
}

compctl -K _dotnet_zsh_complete dotnet
```
