---
title: Necesaria una referencia al ensamblado &#39; &lt;assemblyname&gt; &#39; que contiene la clase base &#39; &lt;classname&gt;&#39;
ms.date: 07/20/2015
f1_keywords:
- bc30007
- vbc30007
helpviewer_keywords:
- BC30007
ms.assetid: 5f34cf47-6c6e-4954-bd8e-d6b020b75fb7
ms.openlocfilehash: f2aa8f1f05ce15bd25992b7f1851854952108813
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/23/2019
ms.locfileid: "54506285"
---
# <a name="reference-required-to-assembly-39ltassemblynamegt39-containing-the-base-class-39ltclassnamegt39"></a>Necesaria una referencia al ensamblado &#39; &lt;assemblyname&gt; &#39; que contiene la clase base &#39; &lt;classname&gt;&#39;
Necesaria una referencia al ensamblado '\<assemblyname >' que contiene la clase base\<classname >'. Agregue una al proyecto.  
  
 La clase está definida en una biblioteca de vínculos dinámicos (DLL) o un ensamblado al que no se hace referencia directamente en el proyecto. El compilador de Visual Basic requiere una referencia para evitar la ambigüedad en caso de la clase está definida en más de una DLL o ensamblado.  
  
 **Identificador de error:** BC30007  
  
## <a name="to-correct-this-error"></a>Para corregir este error  
  
-   Incluya el nombre de la DLL o el ensamblado no referenciados en las referencias del proyecto.  
  
## <a name="see-also"></a>Vea también

- [Administrar referencias en un proyecto](/visualstudio/ide/managing-references-in-a-project)
- [Solucionar problemas de referencias rotas](/visualstudio/ide/troubleshooting-broken-references)
