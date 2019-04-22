---
title: -highentropyva (Visual Basic)
ms.date: 03/10/2018
helpviewer_keywords:
- highentropyva compiler option (Visual Basic)
- /highentropyva compiler option (Visual Basic)
ms.assetid: ff25f20a-6ca2-467b-9e52-5cf439f5028e
ms.openlocfilehash: 16bfea37a5742ac5aaaabfacdcf03a2b5bedb6db
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "58819286"
---
# <a name="-highentropyva-visual-basic"></a>-highentropyva (Visual Basic)
Indica si un archivo ejecutable de 64 bits o un archivo ejecutable que se ha marcado por el [/Platform: anycpu](../../../visual-basic/reference/command-line-compiler/platform.md) admite la opción del compilador dirección Space Layout Randomization (ASLR) de alta entropía.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-highentropyva[+ | -]  
```  
  
## <a name="arguments"></a>Argumentos  
 `+` &#124; `-`  
 Opcional. La opción está desactivada de forma predeterminada o si especifica `-highentropyva-`. La opción está activada si especifica `-highentropyva` o `-highentropyva+`.  
  
## <a name="remarks"></a>Comentarios  
 Si especifica esta opción, las versiones compatibles del kernel de Windows pueden usar niveles superiores de entropía cuando el kernel Aleatoriza el diseño del espacio de direcciones de un proceso como parte de ASLR. Si el kernel usa niveles superiores de entropía, se puede asignar un número mayor de direcciones a las regiones de memoria como pilas y montones. Como resultado, la ubicación de un área de memoria específica es más difícil de adivinar.  
  
 Cuando la opción está activada, el archivo ejecutable de destino y los módulos en que dependa debe ser capaz de controlar los valores de puntero que son superiores a 4 gigabytes (GB) cuando dichos módulos se ejecutan como procesos de 64 bits.  
  
## <a name="see-also"></a>Vea también

- [Compilador de línea de comandos de Visual Basic](../../../visual-basic/reference/command-line-compiler/index.md)
- [Líneas de comandos de compilación de ejemplo](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
