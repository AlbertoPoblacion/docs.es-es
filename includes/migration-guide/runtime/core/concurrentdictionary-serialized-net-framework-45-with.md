---
ms.openlocfilehash: f9d7b8d22818245b96cafffe3732bdfe82ff69d8
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59805113"
---
### <a name="a-concurrentdictionary-serialized-in-net-framework-45-with-netdatacontractserializer-cannot-be-deserialized-by-net-framework-451-or-452"></a>Un elemento ConcurrentDictionary serializado en .NET Framework 4.5 con NetDataContractSerializer no se puede deserializar en .NET Framework 4.5.1 ni 4.5.2

|   |   |
|---|---|
|Detalles|Debido a los cambios internos en el tipo, los objetos <xref:System.Collections.Concurrent.ConcurrentDictionary%602> que se serializaron con .NET Framework 4.5 mediante <xref:System.Runtime.Serialization.NetDataContractSerializer?displayProperty=name> no se pueden deserializar en .NET Framework 4.5.1 o 4.5.2. Tenga en cuenta que a la inversa sí funciona (la serialización con .NET Framework 4.5.x y la deserialización con .NET Framework 4.5). Del mismo modo, la serialización entre todas las versiones 4.x funciona con .NET Framework 4.6. La serialización y deserialización con una única versión de .NET Framework no se ve afectada.|
|Sugerencia|Si es necesario serializar y deserializar <xref:System.Collections.Concurrent.ConcurrentDictionary%602?displayProperty=name> entre .NET Framework 4.5 y 4.5.1/4.5.2, se debe usar un serializador alternativo como <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=name> o <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter?displayProperty=name> en lugar de <xref:System.Runtime.Serialization.NetDataContractSerializer?displayProperty=name>. Como alternativa, dado que este problema se corrige en .NET Framework 4.6, se podría resolver mediante la actualización a esa versión de .NET Framework.|
|Ámbito|Secundaria|
|Versión|4.5.1|
|Tipo|Tiempo de ejecución|
