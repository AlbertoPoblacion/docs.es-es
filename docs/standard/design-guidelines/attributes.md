---
title: Atributos
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- attributes [.NET Framework], about
- class library design guidelines [.NET Framework], attributes
ms.assetid: ee0038ef-b247-4747-a650-3c5c5cd58d8b
author: KrzysztofCwalina
ms.openlocfilehash: 6d4cc6615b7f7346e9c8fc2a7264025f318c8a3d
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61785572"
---
# <a name="attributes"></a>Atributos
<xref:System.Attribute?displayProperty=nameWithType> se utiliza una clase base para definir atributos personalizados.  
  
 Los atributos son anotaciones que pueden agregarse a elementos de programación como ensamblados, tipos, miembros y parámetros. Que se almacenan en los metadatos del ensamblado y se pueden tener acceso en tiempo de ejecución mediante las API de reflexión. Por ejemplo, el marco de trabajo define el <xref:System.ObsoleteAttribute>, que pueden aplicarse a un tipo o miembro para indicar que el tipo o miembro en desuso.  
  
 Los atributos pueden tener una o varias propiedades que transportan datos adicionales relacionados con el atributo. Por ejemplo, `ObsoleteAttribute` podría incluir información adicional sobre la versión en que un tipo o miembro se obtuvo en desuso y la descripción de las nuevas API reemplazando la API obsoleta.  
  
 Algunas propiedades de un atributo se deben especificar cuando se aplica el atributo. Estos se conocen como las propiedades necesarias o los argumentos necesarios, ya que se representan como parámetros de constructor posicional. Por ejemplo, el <xref:System.Diagnostics.ConditionalAttribute.ConditionString%2A> propiedad de la <xref:System.Diagnostics.ConditionalAttribute> es una propiedad necesaria.  
  
 Las propiedades que no necesariamente deben especificarse cuando se aplica el atributo se denominan propiedades opcionales (o argumentos opcionales). Se representan mediante las propiedades configurables. Los compiladores proporcionan una sintaxis especial para establecer estas propiedades cuando se aplica un atributo. Por ejemplo, el <xref:System.AttributeUsageAttribute.Inherited%2A?displayProperty=nameWithType> propiedad representa un argumento opcional.  
  
 **✓ DO** nombres de las clases de atributo personalizado con el sufijo "Atributos".  
  
 **✓ DO** aplicar el <xref:System.AttributeUsageAttribute> a atributos personalizados.  
  
 **✓ DO** proporcionar propiedades configurables para los argumentos opcionales.  
  
 **✓ DO** proporcionan propiedades get-only de argumentos necesarios.  
  
 **✓ DO** proporcionan parámetros de constructor para inicializar las propiedades que corresponden a los argumentos necesarios. Cada parámetro debe tener el mismo nombre (aunque con distinguen mayúsculas de minúsculas) como la propiedad correspondiente.  
  
 **X AVOID** proporcionar parámetros del constructor para inicializar las propiedades que corresponden a los argumentos opcionales.  
  
 En otras palabras, no tiene propiedades que se pueden establecer con un constructor y un establecedor. Esta instrucción hace que sea muy explícito que los argumentos son opcionales y que son necesarias y evita tener dos formas de hacer lo mismo.  
  
 **X AVOID** sobrecarga de constructores de atributo personalizado.  
  
 Tener solo un constructor claramente comunica al usuario qué argumentos son obligatorios y cuáles son opcionales.  
  
 **✓ DO** sellar clases de atributos personalizados, si es posible. Esto hace que la búsqueda para el atributo con mayor rapidez.  
  
 *Portions © 2005, 2009 Microsoft Corporation. Reservados todos los derechos.*  
  
 *Reimpreso con permiso de Pearson Education, Inc. de [instrucciones de diseño de Framework: Convenciones, expresiones y patrones para bibliotecas reutilizables. NET, 2ª edición](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina y Brad Abrams, publicada el 22 de octubre de 2008 por Addison-Wesley Professional como parte de la serie de desarrollo de Microsoft Windows.*  
  
## <a name="see-also"></a>Vea también

- [Instrucciones de diseño de .NET Framework](../../../docs/standard/design-guidelines/index.md)
- [Instrucciones de uso](../../../docs/standard/design-guidelines/usage-guidelines.md)
