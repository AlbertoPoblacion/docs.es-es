---
title: System.String (Métodos)
ms.date: 03/30/2017
ms.assetid: ce307f14-87e6-4816-8694-8a4147f6b784
ms.openlocfilehash: 3a7b45f27441d889524f5055eb5c6a3b06937bd3
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61876660"
---
# <a name="systemstring-methods"></a>System.String (Métodos)
[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] no admite los métodos <xref:System.String> siguientes.  
  
## <a name="unsupported-systemstring-methods-in-general"></a>Métodos System.String no admitidos en general  
 Métodos <xref:System.String> no admitidos en general:  
  
- Sobrecargas que reconocen la referencia cultural (métodos que toman un `CultureInfo`  /  `StringComparison`  /  `IFormatProvider`).  
  
- Métodos que utilizan o generan una matriz `char`.  
  
## <a name="unsupported-systemstring-static-methods"></a>Métodos System.String estáticos no admitidos  
  
|Métodos System.String estáticos no admitidos|  
|----------------------------------------------|  
|<xref:System.String.Copy%28System.String%29?displayProperty=nameWithType>|  
|<xref:System.String.Compare%28System.String%2CSystem.String%2CSystem.Boolean%29?displayProperty=nameWithType>|  
|<xref:System.String.Compare%28System.String%2CSystem.String%2CSystem.Boolean%2CSystem.Globalization.CultureInfo%29?displayProperty=nameWithType>|  
|<xref:System.String.Compare%28System.String%2CSystem.Int32%2CSystem.String%2CSystem.Int32%2CSystem.Int32%29?displayProperty=nameWithType>|  
|<xref:System.String.Compare%28System.String%2CSystem.Int32%2CSystem.String%2CSystem.Int32%2CSystem.Int32%2CSystem.Boolean%29?displayProperty=nameWithType>|  
|<xref:System.String.Compare%28System.String%2CSystem.Int32%2CSystem.String%2CSystem.Int32%2CSystem.Int32%2CSystem.Boolean%2CSystem.Globalization.CultureInfo%29?displayProperty=nameWithType>|  
|<xref:System.String.CompareOrdinal%28System.String%2CSystem.String%29?displayProperty=nameWithType>|  
|<xref:System.String.CompareOrdinal%28System.String%2CSystem.Int32%2CSystem.String%2CSystem.Int32%2CSystem.Int32%29?displayProperty=nameWithType>|  
|<xref:System.String.Format%2A?displayProperty=nameWithType>|  
|<xref:System.String.Join%2A?displayProperty=nameWithType>|  
  
## <a name="unsupported-systemstring-non-static-methods"></a>Métodos System.String no estáticos no admitidos  
  
|Métodos System.String no estáticos no admitidos|  
|---------------------------------------------------|  
|<xref:System.String.IndexOfAny%28System.Char%5B%5D%29?displayProperty=nameWithType>|  
|<xref:System.String.Split%2A?displayProperty=nameWithType>|  
|<xref:System.String.ToCharArray?displayProperty=nameWithType>|  
|<xref:System.String.ToUpper%28System.Globalization.CultureInfo%29?displayProperty=nameWithType>|  
|<xref:System.String.TrimEnd%28System.Char%5B%5D%29?displayProperty=nameWithType>|  
|<xref:System.String.TrimStart%28System.Char%5B%5D%29?displayProperty=nameWithType>|  
  
## <a name="differences-from-net"></a>Diferencias respecto a .NET  
  
- Las consultas no tienen en cuenta las intercalaciones de SQL Server que podrían aplicarse en el servidor y, por lo tanto, proporcionan de forma predeterminada comparaciones dependientes de la referencia cultural, sin distinción entre mayúsculas y minúsculas. Este comportamiento difiere del predeterminado, la semántica con distinción entre mayúsculas y minúsculas de .NET Framework.  
  
- Cuando `LastIndexOf` devuelve 0, la cadena es `NULL` o la posición encontrada es 0.  
  
- Pueden obtenerse resultados inesperados en operaciones de concatenación u otras operaciones con cadenas de longitud fija (`CHAR`, `NCHAR`), porque a estos tipos se les aplica relleno automáticamente en la base de datos.  
  
- Dado que muchos métodos, como `Replace`, `ToLower`, `ToUpper`, y el indizador de carácter, no tienen ningún equivalente válido para las columnas `TEXT` o `NTEXT` y XML, se producirán `SqlExceptions` si se convierten de la forma habitual. Este comportamiento se considera que es aceptable para estos tipos. Sin embargo, todas las operaciones de cadena deben coincidir con la semántica de Common Language Runtime (CLR) para `VARCHAR`, `NVARCHAR`, `VARCHAR(max)` y `NVARCHAR(max)`.  
  
## <a name="see-also"></a>Vea también

- [Tipos de datos y funciones](../../../../../../docs/framework/data/adonet/sql/linq/data-types-and-functions.md)
