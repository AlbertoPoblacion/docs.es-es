---
title: Ensamblados con nombre seguro
ms.date: 03/30/2017
helpviewer_keywords:
- strong-named assemblies, about strong-named assemblies
- assemblies [.NET Framework], strong-named
ms.assetid: d4a80263-f3e0-4d81-9b61-f0cbeae3797b
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 3f87fb330fbea1344cc8532519d358fe8580a9fd
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2019
ms.locfileid: "64592703"
---
# <a name="strong-named-assemblies"></a>Ensamblados con nombre seguro
Al asignar un nombre seguro a un ensamblado, se crea una identidad única para este, lo que puede evitar conflictos de ensamblado.  
  
## <a name="what-makes-a-strong-named-assembly"></a>¿Cómo se obtiene un ensamblado con nombre seguro?  
 Para generar un ensamblado con nombre seguro es necesario usar la clave privada que se corresponda con la clave pública distribuida con el ensamblado, además del ensamblado en sí. En el ensamblado se incluye el manifiesto del ensamblado, que contiene los nombres y los hash de todos los archivos que componen el ensamblado. Los ensamblados que tengan el mismo nombre seguro deben ser idénticos.  
  
 Para asignar nombres seguros a ensamblados puede usar Visual Studio o una herramienta de línea de comandos. Para obtener más información, vea [Cómo: Firmar un ensamblado con un nombre seguro](../../../docs/framework/app-domains/how-to-sign-an-assembly-with-a-strong-name.md) o [Sn.exe (Herramienta de nombre seguro)](../../../docs/framework/tools/sn-exe-strong-name-tool.md).  
  
 Al crear un ensamblado con nombre seguro, este contiene el nombre de texto simple del ensamblado, el número de versión, información opcional de referencia cultural, una firma digital y la clave pública que se corresponda con la clave privada usada para la firma.  
  
> [!WARNING]
>  Para garantizar la seguridad, no confíe únicamente en el uso de nombres seguros. Estos solo proporcionan una identidad única.  
  
## <a name="why-strong-name-your-assemblies"></a>¿Por qué asignar nombres seguros a los ensamblados?  
 Cuando se hace referencia a un ensamblado con nombre seguro, se espera obtener ciertas ventajas, como el control de versiones y la protección de nombres. Los ensamblados con nombre seguro se pueden instalar en la caché global de ensamblados, que es necesaria para permitir algunos escenarios.  
  
 Los ensamblados con nombre seguro son útiles en los escenarios siguientes:  
  
- Cuando quiere habilitar los ensamblados para hacer referencia a ensamblados con nombre seguro, o quiere dar acceso `friend` a sus ensamblados desde otros ensamblados con nombre seguro.  
  
- Cuando una aplicación necesita acceder a versiones diferentes del mismo ensamblado. Esto quiere decir que necesita cargar en paralelo diferentes versiones de un ensamblado en el mismo dominio de la aplicación sin que surjan conflictos. Por ejemplo, si existen diferentes extensiones de una API en ensamblados que tienen el mismo nombre simple, los nombres seguros proporcionan una identidad única para cada versión del ensamblado.  
  
- Cuando no quiere que el rendimiento de las aplicaciones que usan el ensamblado se vea afectado, por lo que el ensamblado debe ser de dominio neutro. Esto requiere nombres seguros, ya que se debe instalar un ensamblado de dominio neutro en la caché global de ensamblados.  
  
- Cuando quiere centralizar el servicio la aplicación mediante una directiva de edición, lo que significa que el ensamblado se debe instalar en la caché global de ensamblados.  
  
 Si es un desarrollador de código abierto y quiere obtener las ventajas de identidad de un ensamblado con nombre seguro, proteja la clave privada asociada con un ensamblado en el sistema de control de código fuente.  
  
## <a name="see-also"></a>Vea también

- [Caché global de ensamblados](../../../docs/framework/app-domains/gac.md)
- [Cómo: Firma de un ensamblado con un nombre seguro](../../../docs/framework/app-domains/how-to-sign-an-assembly-with-a-strong-name.md)
- [Sn.exe (Herramienta de nombre seguro)](../../../docs/framework/tools/sn-exe-strong-name-tool.md)
- [Crear y utilizar ensamblados con nombre seguro](../../../docs/framework/app-domains/create-and-use-strong-named-assemblies.md)
