---
title: Interfaces genéricas
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- generic interfaces [.NET Framework]
- equality comparisons [.NET Framework]
- generics [.NET Framework], interfaces
- ordering comparisons [.NET Framework]
ms.assetid: 88bf5b04-d371-4edb-ba38-01ec7cabaacf
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 9570578e8ae4397f060805b891f86d7d4f273cd4
ms.sourcegitcommit: 155012a8a826ee8ab6aa49b1b3a3b532e7b7d9bd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2019
ms.locfileid: "66487046"
---
# <a name="generic-interfaces"></a>Interfaces genéricas
Este tema ofrece una introducción a las interfaces genéricas que proporcionan funcionalidad común a distintas familias de tipos genéricos.  
  
## <a name="generic-interfaces"></a>Interfaces genéricas  
 Las interfaces genéricas proporcionan homólogas con seguridad de tipos a las interfaces no genéricas para realizar comparaciones de ordenación y de igualdad, y para obtener funcionalidad compartida por los tipos de colección genéricos.  
  
> [!NOTE]
>  A partir de .NET Framework 4, los parámetros de tipo de varias interfaces genéricas están marcados como covariantes o contravariantes, y ofrecen una mayor flexibilidad para asignar y usar tipos que implementan estas interfaces. Vea [Covarianza y contravarianza](../../../docs/standard/generics/covariance-and-contravariance.md).  
  
### <a name="equality-and-ordering-comparisons"></a>Comparaciones de igualdad y ordenación  
 En el espacio de nombres <xref:System>, las interfaces genéricas <xref:System.IComparable%601?displayProperty=nameWithType> y <xref:System.IEquatable%601?displayProperty=nameWithType>, igual que sus homólogas no genéricas, definen métodos para realizar comparaciones de ordenación y comparaciones de igualdad, respectivamente. Los tipos implementan estas interfaces para proporcionar la capacidad de desempeñar dichas comparaciones.  
  
 En el espacio de nombres <xref:System.Collections.Generic>, las interfaces genéricas <xref:System.Collections.Generic.IComparer%601> y <xref:System.Collections.Generic.IEqualityComparer%601> ofrecen una manera de definir una comparación de ordenación o de igualdad para los tipos que no implementan las interfaces genéricas <xref:System.IComparable%601?displayProperty=nameWithType> o <xref:System.IEquatable%601?displayProperty=nameWithType> y proporcionan una manera de redefinir esas relaciones para los tipos que sí lo hacen. Estas interfaces son usadas por métodos y constructores de muchas de las clases de colección genéricas. Por ejemplo, puede pasar un objeto genérico <xref:System.Collections.Generic.IComparer%601> al constructor de la clase <xref:System.Collections.Generic.SortedDictionary%602> para especificar un criterio de ordenación para un tipo que no implementa una interfaz <xref:System.IComparable%601?displayProperty=nameWithType> genérica. Hay sobrecargas del método estático genérico <xref:System.Array.Sort%2A?displayProperty=nameWithType> y el método de instancia <xref:System.Collections.Generic.List%601.Sort%2A?displayProperty=nameWithType> para ordenar matrices y listas usando implementaciones genéricas <xref:System.Collections.Generic.IComparer%601>.  
  
 Las clases genéricas <xref:System.Collections.Generic.Comparer%601> y <xref:System.Collections.Generic.EqualityComparer%601> proporcionan clases base para las implementaciones de las interfaces genéricas <xref:System.Collections.Generic.IComparer%601> y <xref:System.Collections.Generic.IEqualityComparer%601>, y también proporcionan comparaciones de ordenación y de igualdad predeterminadas mediante sus respectivas propiedades <xref:System.Collections.Generic.Comparer%601.Default%2A?displayProperty=nameWithType> y <xref:System.Collections.Generic.EqualityComparer%601.Default%2A?displayProperty=nameWithType>.  
  
### <a name="collection-functionality"></a>Funcionalidad de colección  
 La interfaz genérica <xref:System.Collections.Generic.ICollection%601> es la interfaz básica para los tipos de colección genéricos. Proporciona la funcionalidad básica para agregar, quitar, copiar y enumerar elementos. <xref:System.Collections.Generic.ICollection%601> hereda tanto de la interfaz genérica <xref:System.Collections.Generic.IEnumerable%601> como de la interfaz no genérica <xref:System.Collections.IEnumerable>.  
  
 La interfaz genérica <xref:System.Collections.Generic.IList%601> extiende la interfaz genérica <xref:System.Collections.Generic.ICollection%601> con métodos para la recuperación indizada.  
  
 La interfaz genérica <xref:System.Collections.Generic.IDictionary%602> extiende la interfaz genérica <xref:System.Collections.Generic.ICollection%601> con métodos para la recuperación con clave. Los tipos de diccionario genéricos de la biblioteca de clases base de .NET Framework también implementan la interfaz no genérica <xref:System.Collections.IDictionary>.  
  
 La interfaz genérica <xref:System.Collections.Generic.IEnumerable%601> proporciona una estructura de enumerador genérica. La interfaz genérica <xref:System.Collections.Generic.IEnumerator%601> implementada por enumeradores genéricos hereda la interfaz no genérica <xref:System.Collections.IEnumerator>; los miembros <xref:System.Collections.IEnumerator.MoveNext%2A> y <xref:System.Collections.IEnumerator.Reset%2A>, que no dependen del parámetro de tipo `T`, solo aparecen en la interfaz no genérica. Esto significa que cualquier consumidor de la interfaz no genérica también puede usar la interfaz genérica.  
  
## <a name="see-also"></a>Vea también

- <xref:System.Collections.Generic?displayProperty=nameWithType>
- <xref:System.Collections.ObjectModel?displayProperty=nameWithType>
- [Genéricos](../../../docs/standard/generics/index.md)
- [Colecciones genéricas en .NET Framework](../../../docs/standard/generics/collections.md)
- [Delegados genéricos para manipular matrices y listas](../../../docs/standard/generics/delegates-for-manipulating-arrays-and-lists.md)
- [Covarianza y contravarianza](../../../docs/standard/generics/covariance-and-contravariance.md)
