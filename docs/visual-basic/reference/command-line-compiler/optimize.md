---
title: -optimize
ms.date: 07/20/2015
helpviewer_keywords:
- optimize compiler option [Visual Basic]
- /optimize compiler option [Visual Basic]
- optimization [Visual Basic], enabling
- -optimize compiler option [Visual Basic]
ms.assetid: fcba4a97-3622-4b87-a891-0f77deab4998
ms.openlocfilehash: eb84e0a7038e7ff8cb399ac7222b6ac1661b5bc1
ms.sourcegitcommit: bce0586f0cccaae6d6cbd625d5a7b824d1d3de4b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/02/2019
ms.locfileid: "58842166"
---
# <a name="-optimize"></a>-optimize
Habilita o deshabilita las optimizaciones del compilador.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-optimize[ + | - ]  
```  
  
## <a name="arguments"></a>Argumentos  
  
|Término|de esquema JSON|  
|---|---|  
|`+` &#124; `-`|Opcional. El `-optimize-` opción deshabilita las optimizaciones del compilador. El `-optimize+` opción habilita las optimizaciones. De forma predeterminada, las optimizaciones están deshabilitadas.|  
  
## <a name="remarks"></a>Comentarios  
 Gracias a las optimizaciones del compilador, el archivo de salida será más pequeño, más rápido y más eficaz. Sin embargo, dado que las optimizaciones causan la reestructuración del código en el archivo de salida `-optimize+` puede dificultar la depuración.  
  
 Todos los módulos que se genera con `-target:module` para un ensamblado debe usar la misma `-optimize` configuración que el ensamblado. Para obtener más información, consulte [-destino (Visual Basic)](../../../visual-basic/reference/command-line-compiler/target.md).  
  
 Puede combinar el `-optimize` y `-debug` opciones.  
  
|Para establecer - optimizar en el entorno de desarrollo integrado de Visual Studio|  
|---|  
|1.  Seleccione un proyecto en el **Explorador de soluciones**. En el menú **Proyecto**, haga clic en **Propiedades**.<br />     <br />2.  Haga clic en la pestaña **Compilar**.<br />3.  Haga clic en el botón **Avanzada** .<br />4.  Modificar el **habilitar optimizaciones** casilla de verificación.|  
  
## <a name="example"></a>Ejemplo  
 El siguiente código compila `T2.vb` y habilita las optimizaciones del compilador.  
  
```console
vbc t2.vb -optimize  
```  
  
## <a name="see-also"></a>Vea también

- [Compilador de línea de comandos de Visual Basic](../../../visual-basic/reference/command-line-compiler/index.md)
- [-debug (Visual Basic)](../../../visual-basic/reference/command-line-compiler/debug.md)
- [Líneas de comandos de compilación de ejemplo](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
- [-target (Visual Basic)](../../../visual-basic/reference/command-line-compiler/target.md)
