---
title: -bugreport
ms.date: 03/08/2018
helpviewer_keywords:
- -bugreport compiler option [Visual Basic]
- bugreport compiler option [Visual Basic]
- /bugreport compiler option [Visual Basic]
ms.assetid: e4325406-8dbd-4b48-b311-9ee0799e48bb
ms.openlocfilehash: 440e583b55765d680ee72f8574f929e335e10cdb
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/14/2019
ms.locfileid: "65590633"
---
# <a name="-bugreport"></a>-bugreport
Crea un archivo que puede usar cuando se archiva un informe de errores.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-bugreport:file  
```  
  
## <a name="arguments"></a>Argumentos  
  
|Término|Definición|  
|---|---|  
|`file`|Obligatorio. El nombre del archivo que contendrá el informe de errores. Ponga el nombre de archivo entre comillas ("") si el nombre contiene un espacio.|  
  
## <a name="remarks"></a>Comentarios  
 La siguiente información se agrega a `file`:  
  
- Una copia de todos los archivos de código fuente de la compilación.  
  
- Una lista de las opciones del compilador utilizadas en la compilación.  
  
- Información de versión sobre su compilador, el common language runtime y el sistema operativo.  
  
- Resultados del compilador, si los hay.  
  
- Una descripción del problema, para el que se le pedirá.  
  
- Una descripción de cómo cree que el problema debe corregirse para que se le pedirá.  
  
 Dado que una copia de todos los archivos de código fuente se incluye en `file`, que es posible que desee reproducir el defecto de código (sospechado) en el programa más corto posible.  
  
> [!IMPORTANT]
>  El `-bugreport` opción genera un archivo que contiene información potencialmente confidencial. Esto incluye la hora actual, la versión de compilador, versión de .NET Framework, versión del sistema operativo, nombre de usuario, los argumentos de línea de comandos con la que se ejecutó el compilador, todo el código fuente y el formato binario de cualquier ensamblado que se hace referencia. Esta opción puede obtenerse mediante la especificación de opciones de línea de comandos en el archivo Web.config para una compilación de servidor de una aplicación ASP.NET. Para evitar esto, modifique el archivo Machine.config para impedir que los usuarios realizar la compilación en el servidor.  
  
 Si esta opción se utiliza con `-errorreport:prompt`, `-errorreport:queue`, o `-errorreport:send`, y la aplicación detecta un error interno del compilador, la información de `file` se envía a Microsoft Corporation. Esta información le ayudará a los ingenieros de Microsoft a identificar la causa del error y puede ayudar a mejorar la próxima versión de Visual Basic. De forma predeterminada, no se envía ninguna información a Microsoft. Sin embargo, cuando se compila una aplicación mediante el uso de `-errorreport:queue`, que está habilitado de forma predeterminada, la aplicación recopila los informes de errores. A continuación, cuando el administrador del equipo inicia sesión, el sistema de informes de errores muestra una ventana emergente que permite al administrador enviar a Microsoft los informes de errores producidos desde el inicio de sesión.  
  
> [!NOTE]
>  El `/bugreport` opción no está disponible en el entorno de desarrollo de Visual Studio; está disponible solo cuando se compila desde la línea de comandos.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente se compila `T2.vb` y coloca toda la información de informes de errores en el archivo `Problem.txt`.  
  
```  
vbc -bugreport:problem.txt t2.vb  
```  
  
## <a name="see-also"></a>Vea también

- [Compilador de línea de comandos de Visual Basic](../../../visual-basic/reference/command-line-compiler/index.md)
- [-debug (Visual Basic)](../../../visual-basic/reference/command-line-compiler/debug.md)
- [-errorreport](../../../visual-basic/reference/command-line-compiler/errorreport.md)
- [Líneas de comandos de compilación de ejemplo](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
- [Elemento trustLevel para securityPolicy (esquema de configuración de ASP.NET)](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/as399f0x(v=vs.100))
