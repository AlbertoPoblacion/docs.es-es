---
title: Protobuf any y de Fields for Variant Types-gRPC for WCF Developers
description: Aprenda a usar el tipo any y la palabra clave de para representar los tipos de objeto Variant en los mensajes.
ms.date: 09/09/2019
ms.openlocfilehash: af3ba22c238aa80a8c6119f62d5d8914770cad68
ms.sourcegitcommit: f348c84443380a1959294cdf12babcb804cfa987
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/12/2019
ms.locfileid: "73971613"
---
# <a name="protobuf-any-and-oneof-fields-for-variant-types"></a>Protobuf todos los campos y de para los tipos Variant

El control de los tipos de propiedades dinámicas (es decir, las propiedades de tipo `object`) en WCF es complicado. Se deben especificar los serializadores, se deben proporcionar los atributos [KnownType](xref:System.Runtime.Serialization.KnownTypeAttribute) , etc.

Protobuf proporciona dos opciones más sencillas para tratar con valores que pueden ser de más de un tipo. El tipo de `Any` puede representar cualquier tipo de mensaje conocido de protobuf, mientras que la palabra clave `oneof` permite especificar que solo se puede establecer un intervalo de campos en un mensaje determinado.

## <a name="any"></a>Cualquiera

`Any` es uno de los "tipos conocidos" de protobuf: una colección de tipos de mensajes útiles y reutilizables con implementaciones en todos los idiomas admitidos. Para usar el tipo de `Any`, debe importar la definición de `google/protobuf/any.proto`.

```protobuf
syntax "proto3"

import "google/protobuf/any.proto"

message Stock {
    // Stock-specific data
}

message Currency {
    // Currency-specific data
}

message ChangeNotification {
    int32 id = 1;
    google.protobuf.Any instrument = 2;
}
```

En el C# código, la clase `Any` proporciona métodos para establecer el campo, extraer el mensaje y comprobar el tipo.

```csharp
public void FormatChangeNotification(ChangeNotification change)
{
    if (change.Instrument.Is(Stock.Descriptor))
    {
        FormatStock(change.Instrument.Unpack<Stock>());
    }
    else if (change.Instrument.Is(Currency.Descriptor))
    {
        FormatCurrency(change.Instrument.Unpack<Currency>());
    }
    else
    {
        throw new ArgumentException("Unknown instrument type");
    }
}
```

El código de reflexión interno de protobuf usa el campo estático `Descriptor` en cada tipo generado para resolver `Any` tipos de campo. También hay un método `TryUnpack<T>`, pero que crea una instancia no inicializada de `T` incluso cuando se produce un error, por lo que es mejor usar el método `Is` tal y como se mostró anteriormente.

## <a name="oneof"></a>De

Los campos de de son una característica de lenguaje: el compilador controla la palabra clave `oneof` cuando genera la clase de mensaje. El uso de `oneof` para especificar el mensaje de `ChangeNotification` podría ser similar al siguiente:

```protobuf
message Stock {
    // Stock-specific data
}

message Currency {
    // Currency-specific data
}

message ChangeNotification {
  int32 id = 1;
  oneof instrument {
    Stock stock = 2;
    Currency currency = 3;
  }
}
```

Los campos del conjunto de `oneof` deben tener números de campo únicos dentro de la declaración de mensaje global.

Cuando se usa `oneof`, el código C# generado incluye una enumeración que especifica cuál de los campos se ha establecido. Puede probar la enumeración para buscar el campo que se establece. Los campos que no se establecen devuelven `null` o el valor predeterminado, en lugar de producir una excepción.

```csharp
public void FormatChangeNotification(ChangeNotification change)
{
    switch (change.InstrumentCase)
    {
        case ChangeNotification.InstrumentOneofCase.None:
            return;
        case ChangeNotification.InstrumentOneofCase.Stock:
            FormatStock(change.Stock);
            break;
        case ChangeNotification.InstrumentOneofCase.Currency:
            FormatCurrency(change.Currency);
            break;
        default:
            throw new ArgumentException("Unknown instrument type");
    }
}
```

Al establecer cualquier campo que forme parte de un conjunto de `oneof` se borrarán automáticamente los demás campos del conjunto. No se puede usar `repeated` con `oneof`. En su lugar, puede crear un mensaje anidado con el campo repetido o el `oneof` establecido para evitar esta limitación.

>[!div class="step-by-step"]
>[Anterior](protobuf-reserved.md)
>[Siguiente](protobuf-enums.md)
