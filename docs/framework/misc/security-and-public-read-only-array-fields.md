---
title: Seguridad y campos de matriz públicos de sólo lectura
ms.date: 03/30/2017
helpviewer_keywords:
- security [.NET Framework], public read-only array fields
ms.assetid: 3df28dee-2a9f-40ff-9852-bfdbe59c27f3
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 3d36009fa4fc7b9299708768fe34a75f1fde6797
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/22/2019
ms.locfileid: "69910736"
---
# <a name="security-and-public-read-only-array-fields"></a>Seguridad y campos de matriz públicos de sólo lectura
Nunca use campos de matriz pública de solo lectura de las bibliotecas administradas para definir el comportamiento del límite o la seguridad de las aplicaciones, ya que se pueden modificar los campos de matriz pública de solo lectura.  
  
## <a name="remarks"></a>Comentarios  
 Algunas clases de .NET Framework incluyen campos públicos de solo lectura que contienen parámetros de límite específicos de la plataforma.  Por ejemplo, el <xref:System.IO.Path.InvalidPathChars> campo es una matriz que describe los caracteres que no están permitidos en una cadena de ruta de acceso de archivo.  Muchos campos similares están presentes en el .NET Framework.  
  
 Los valores de los campos públicos de solo lectura <xref:System.IO.Path.InvalidPathChars> como pueden ser modificados por el código o el código que comparte el dominio de aplicación del código.  No debe utilizar campos de matriz pública de solo lectura como este para definir el comportamiento de los límites de las aplicaciones.  Si lo hace, el código malintencionado puede modificar las definiciones de límite y usar el código de maneras inesperadas.  
  
 En la versión 2,0 y posteriores de la .NET Framework, debe utilizar métodos que devuelvan una nueva matriz en lugar de usar campos de matriz públicos.  Por ejemplo, en lugar de utilizar el <xref:System.IO.Path.InvalidPathChars> campo, debe utilizar el <xref:System.IO.Path.GetInvalidPathChars%2A> método.  
  
 Tenga en cuenta que los tipos de .NET Framework no utilizan los campos públicos para definir tipos de límites internamente.  En su lugar, el .NET Framework utiliza campos privados independientes.  El cambio de los valores de estos campos públicos no altera el comportamiento de los tipos de .NET Framework.  
  
## <a name="see-also"></a>Vea también

- [Instrucciones de codificación segura](../../standard/security/secure-coding-guidelines.md)
