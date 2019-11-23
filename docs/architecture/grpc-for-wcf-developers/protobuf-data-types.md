---
title: Tipos de datos escalares de protobuf-gRPC para desarrolladores de WCF
description: Obtenga información sobre los tipos de datos básicos y conocidos que admiten protobuf y gRPC en .NET Core.
ms.date: 09/09/2019
ms.openlocfilehash: ae7f5f48099000dff0eefb36e23cb9b9f2ac517c
ms.sourcegitcommit: f348c84443380a1959294cdf12babcb804cfa987
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/12/2019
ms.locfileid: "73971547"
---
# <a name="protobuf-scalar-data-types"></a>Tipos de datos escalares de Protobuf

Protobuf admite un intervalo de tipos de valores escalares nativos. En la tabla siguiente se enumeran todos con C# su tipo equivalente:

| Tipo protobuf | Tipo de C#      | Notas |
| ------------- | ------------ | ----- |
| `double`      | `double`     |       |
| `float`       | `float`      |       |
| `int32`       | `int`        | 1     |
| `int64`       | `long`       | 1     |
| `uint32`      | `uint`       |       |
| `uint64`      | `ulong`      |       |
| `sint32`      | `int`        | 1     |
| `sint64`      | `long`       | 1     |
| `fixed32`     | `uint`       | 2     |
| `fixed64`     | `ulong`      | 2     |
| `sfixed32`    | `int`        | 2     |
| `sfixed64`    | `long`       | 2     |
| `bool`        | `bool`       |       |
| `string`      | `string`     | 3     |
| `bytes`       | `ByteString` | 4     |

## <a name="notes"></a>Notas

1. La codificación estándar para `int32` y `int64` es ineficaz cuando se trabaja con valores con signo. Si es probable que el campo contenga números negativos, use `sint32` o `sint64` en su lugar. Ambos tipos se asignan C# a los tipos `int` y `long`, respectivamente.
2. Los campos de `fixed` siempre utilizan el mismo número de bytes, independientemente del valor que sea. Este comportamiento hace que la serialización y la deserialización sean más rápidas para los valores más grandes.
3. Las cadenas protobuf son codificadas con UTF-8 (o ASCII de 7 bits) y la longitud codificada no puede ser mayor que 2<sup>32</sup>.
4. El tiempo de ejecución de protobuf proporciona un tipo de `ByteString` que se C# asigna fácilmente a `byte[]` matrices y desde ellas.

## <a name="other-net-primitive-types"></a>Otros tipos primitivos de .NET

### <a name="dates-and-times"></a>Fechas y horas

Los tipos escalares nativos no proporcionan valores de fecha y hora, equivalentes a C#<xref:System.DateTimeOffset>, <xref:System.DateTime>y <xref:System.TimeSpan>. Estos tipos se pueden especificar usando algunas de las extensiones de "tipos conocidos" de Google, que proporcionan compatibilidad de generación de código y en tiempo de ejecución para tipos de campo más complejos en las plataformas admitidas. En la tabla siguiente se muestran los tipos de fecha y hora:

| Tipo de C# | Protobuf Well-Known Type |
| ------- | ------------------------ |
| `DateTimeOffset` | `google.protobuf.Timestamp` |
| `DateTime` | `google.protobuf.Timestamp` |
| `TimeSpan` | `google.protobuf.Duration` |

```protobuf  
syntax = "proto3"

import "google/protobuf/duration.proto";  
import "google/protobuf/timestamp.proto";

message Meeting {

    string subject = 1;
    google.protobuf.Timestamp time = 2;
    google.protobuf.Duration duration = 3;

}  
```

Las propiedades generadas en C# la clase no son los tipos de fecha y hora de .net. Las propiedades usan las clases `Timestamp` y `Duration` en el espacio de nombres `Google.Protobuf.WellKnownTypes`, que proporcionan métodos para realizar conversiones entre `DateTimeOffset`, `DateTime`y `TimeSpan`.

```csharp
// Create Timestamp and Duration from .NET DateTimeOffset and TimeSpan
var meeting = new Meeting
{
    Time = Timestamp.FromDateTimeOffset(meetingTime), // also FromDateTime()
    Duration = Duration.FromTimeSpan(meetingLength)
};

// Convert Timestamp and Duration to .NET DateTimeOffset and TimeSpan
DateTimeOffset time = meeting.Time.ToDateTimeOffset();
TimeSpan? duration = meeting.Duration?.ToTimeSpan();
```

> [!NOTE]
> El tipo de `Timestamp` funciona con las horas UTC; los valores de `DateTimeOffset` siempre tienen un desplazamiento de cero y la propiedad `DateTime.Kind` siempre se `DateTimeKind.Utc`.

### <a name="systemguid"></a>System.Guid

El tipo de <xref:System.Guid>, conocido como `UUID` en otras plataformas, no es compatible directamente con protobuf y no hay ningún tipo conocido para él. El mejor enfoque consiste en controlar `Guid` valores como `string` campo, con el formato hexadecimal de `8-4-4-4-12` estándar (por ejemplo, `45a9fda3-bd01-47a9-8460-c1cd7484b0b3`), que puede analizarse en todos los lenguajes y plataformas. No use un campo de `bytes` para `Guid` valores, ya que los problemas con modos endian pueden producir un comportamiento errático al interactuar con otras plataformas, como Java.

### <a name="nullable-types"></a>Tipos que aceptan valores NULL

La generación de código protobuf C# para usa los tipos nativos, como `int` para `int32`. Esto significa que los valores siempre se incluyen y no pueden ser null. En el caso de los valores que requieren valores NULL explícitos, C# como el uso de `int?` en el código, los "tipos conocidos" de protobuf incluyen contenedores C# que se compilan en tipos que aceptan valores NULL. Para usarlos, importe `wrappers.proto` en el archivo `.proto`, de la siguiente manera:

```protobuf  
syntax = "proto3"

import "google/protobuf/wrappers.proto"

message Person {

    ...
    google.protobuf.Int32Value age = 5;

}
```

Protobuf usará el `T?` simple (por ejemplo, `int?`) para la propiedad de mensaje generada.

En la tabla siguiente se muestra la lista completa de tipos de contenedor C# con su tipo equivalente:

| Tipo de C#   | Contenedor de tipo conocido       |
| --------- | ----------------------------- |
| `double?` | `google.protobuf.DoubleValue` |
| `float?`  | `google.protobuf.FloatValue`  |
| `int?`    | `google.protobuf.Int32Value`  |
| `long?`   | `google.protobuf.Int64Value`  |
| `uint?`   | `google.protobuf.UInt32Value` |
| `ulong?`  | `google.protobuf.UInt64Value` |

Los tipos conocidos `Timestamp` y `Duration` se representan en .NET como clases, por lo que no hay necesidad de una versión que acepte valores NULL, pero es importante comprobar si hay valores NULL en las propiedades de esos tipos al convertirlos a `DateTimeOffset` o `TimeSpan`.

## <a name="decimals"></a>Decimals

Protobuf no admite de forma nativa el tipo de `decimal` .NET, simplemente `double` y `float`. Hay una explicación en curso en el proyecto protobuf sobre la posibilidad de agregar un tipo de `Decimal` estándar a los tipos conocidos, con compatibilidad de plataforma para los lenguajes y marcos que lo admiten, pero aún no se ha implementado nada.

Es posible crear una definición de mensaje para representar el tipo de `decimal` que funcionaría para la serialización segura entre clientes y servidores de .NET, pero los desarrolladores de otras plataformas tendrían que comprender el formato que se usa e implementar su propio control.

### <a name="creating-a-custom-decimal-type-for-protobuf"></a>Crear un tipo decimal personalizado para protobuf

Una implementación muy sencilla podría ser similar al tipo de `Money` no estándar usado por algunas API de Google, sin el campo `currency`.

```protobuf
package CustomTypes;

// Example: 12345.6789 -> { units = 12345, nanos = 678900000 }
message Decimal {

    // Whole units part of the amount
    int64 units = 1;

    // Nano units of the amount (10^-9)
    // Must be same sign as units
    sfixed32 nanos = 2;
}
```

El campo `nanos` representa los valores de `0.999_999_999` a `-0.999_999_999`. Por ejemplo, el valor de `decimal` `1.5m` se representaría como `{ units = 1, nanos = 500_000_000 }` (este es el motivo por el que el campo `nanos` de este ejemplo usa el tipo de `sfixed32`, que codifica de forma más eficaz que `int32` para valores mayores). Si el campo `units` es negativo, el campo de `nanos` también debe ser negativo.

> [!NOTE]
> Existen varios algoritmos para codificar los valores `decimal` como cadenas de bytes, pero este mensaje es mucho más fácil de entender que cualquiera de ellos, y los valores no se ven afectados por *[modos endian](https://en.wikipedia.org/wiki/Endianness)* en distintas plataformas.

La conversión entre este tipo y el tipo de `decimal` BCL podría implementarse de C# la siguiente manera.

```csharp
namespace CustomTypes
{
    public partial class GrpcDecimal
    {
        private const decimal NanoFactor = 1_000_000_000;
        public GrpcDecimal(long units, int nanos)
        {
            Units = units;
            Nanos = nanos;
        }

        public long Units { get; }
        public int Nanos { get; }

        public static implicit operator decimal(CustomTypes.Decimal grpcDecimal)
        {
            return grpcDecimal.Units + grpcDecimal.Nanos / NanoFactor;
        }

        public static implicit operator CustomTypes.Decimal(decimal value)
        {
            var units = decimal.ToInt64(value);
            var nanos = decimal.ToInt32((value - units) * NanoFactor);
            return new CustomTypes.Decimal(units, nanos);
        }
    }
}
```

> [!IMPORTANT]
> Siempre que use tipos de mensaje de utilidad personalizados como este, **debe** documentarlos con comentarios en el `.proto` para que otros desarrolladores puedan implementar la conversión a y desde el tipo equivalente en su propio lenguaje o marco.

>[!div class="step-by-step"]
>[Anterior](protobuf-messages.md)
>[Siguiente](protobuf-nested-types.md)
