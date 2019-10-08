---
title: -bugreport
ms.date: 03/08/2018
helpviewer_keywords:
- -bugreport compiler option [Visual Basic]
- bugreport compiler option [Visual Basic]
- /bugreport compiler option [Visual Basic]
ms.assetid: e4325406-8dbd-4b48-b311-9ee0799e48bb
ms.openlocfilehash: 46d726332806f7d1f6e80dd7df31867051276b45
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/07/2019
ms.locfileid: "72002352"
---
# <a name="-bugreport"></a>-bugreport
Crea un archivo que se puede usar al archivar un informe de errores.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-bugreport:file  
```  
  
## <a name="arguments"></a>Argumentos  
  
|Término|Definición|  
|---|---|  
|`file`|Obligatorio. Nombre del archivo que contendrá el informe de errores. Escriba el nombre de archivo entre comillas ("") si el nombre contiene un espacio.|  
  
## <a name="remarks"></a>Comentarios  
 La siguiente información se agrega a `file`:  
  
- Una copia de todos los archivos de código fuente en la compilación.  
  
- Una lista de las opciones del compilador utilizadas en la compilación.  
  
- Información de versión sobre el compilador, el Common Language Runtime y el sistema operativo.  
  
- Resultados del compilador, si los hay.  
  
- Una descripción del problema, para el que se le solicita.  
  
- Una descripción de cómo cree que el problema debe corregirse, para lo que se le solicita.  
  
 Dado que una copia de todos los archivos de código fuente se incluye en `file`, puede que desee reproducir el defecto de código (sospechoso) en el programa más corto posible.  
  
> [!IMPORTANT]
> La opción `-bugreport` genera un archivo que contiene información potencialmente confidencial. Esto incluye la hora actual, la versión del compilador, la versión .NET Framework, la versión del sistema operativo, el nombre de usuario, los argumentos de línea de comandos con los que se ejecutó el compilador, todo el código fuente y el formato binario de cualquier ensamblado al que se hace referencia. Se puede tener acceso a esta opción si se especifican las opciones de línea de comandos en el archivo Web. config para una compilación del lado servidor de una aplicación ASP.NET. Para evitarlo, modifique el archivo Machine. config para que no permita a los usuarios compilar en el servidor.  
  
 Si esta opción se usa con `-errorreport:prompt`, `-errorreport:queue` o `-errorreport:send` y la aplicación encuentra un error interno del compilador, la información de `file` se envía a Microsoft Corporation. Esa información ayudará a los ingenieros de Microsoft a identificar la causa del error y puede ayudar a mejorar la próxima versión de Visual Basic. De forma predeterminada, no se envía información a Microsoft. Sin embargo, al compilar una aplicación mediante `-errorreport:queue`, que está habilitada de forma predeterminada, la aplicación recopila sus informes de errores. A continuación, cuando el administrador del equipo inicia sesión, el sistema de informes de errores muestra una ventana emergente que permite al administrador reenviar a Microsoft los informes de errores que se produjeron desde el inicio de sesión.  
  
> [!NOTE]
> La opción `/bugreport` no está disponible en el entorno de desarrollo de Visual Studio; solo está disponible cuando se compila desde la línea de comandos.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se compila `T2.vb` y se coloca toda la información de informes de errores en el archivo `Problem.txt`.  
  
```console  
vbc -bugreport:problem.txt t2.vb  
```  
  
## <a name="see-also"></a>Vea también

- [Compilador de línea de comandos de Visual Basic](../../../visual-basic/reference/command-line-compiler/index.md)
- [-debug (Visual Basic)](../../../visual-basic/reference/command-line-compiler/debug.md)
- [-errorreport](../../../visual-basic/reference/command-line-compiler/errorreport.md)
- [Líneas de comandos de compilación de ejemplo](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
- [trustLevel (elemento) para securityPolicy (esquema de configuración de ASP.NET)](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/as399f0x(v=vs.100))
