---
title: 'Metadatos: gRPC para desarrolladores de WCF'
description: Cómo se usan los metadatos en gRPC para pasar contexto adicional entre clientes y servidores
ms.date: 09/02/2019
ms.openlocfilehash: 723d877bfbf0c2b0785949ff15939aedbac4d4e9
ms.sourcegitcommit: f348c84443380a1959294cdf12babcb804cfa987
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/12/2019
ms.locfileid: "73971973"
---
# <a name="metadata"></a>Metadatos

"Metadatos" hace referencia a datos adicionales que pueden ser útiles mientras se procesan las solicitudes y las respuestas, pero no forman parte de los datos reales de la aplicación. Los metadatos pueden incluir tokens de autenticación, identificadores de solicitud y etiquetas para fines de supervisión, o información sobre los datos, como el número de registros de un conjunto de datos.

Es posible agregar encabezados de clave y valor genéricos a los mensajes WCF mediante una <xref:System.ServiceModel.OperationContextScope> y la propiedad <xref:System.ServiceModel.OperationContext.OutgoingMessageHeaders?displayProperty=nameWithType>, y controlarlos mediante <xref:System.ServiceModel.Channels.MessageProperties>.

las llamadas y respuestas gRPC también pueden incluir metadatos similares a los encabezados HTTP. Son principalmente invisibles para gRPC y se pasan para ser procesados por su código de aplicación o middleware. Los metadatos se representan como pares clave-valor, donde la clave es una cadena y el valor es una cadena o datos binarios. No es necesario especificar metadatos en el archivo de `.proto`.

Los metadatos se controlan mediante la clase `Metadata` del paquete de NuGet [GRPC. Core. API](https://www.nuget.org/packages/Grpc.Core.Api/) . Esta clase se puede utilizar con la sintaxis del inicializador de colección.

En el ejemplo siguiente se muestra cómo agregar metadatos a una llamada C# de un cliente:

```csharp
var metadata = new Metadata
{
    { "Requester", _clientName }
};

var request = new GetPortfolioRequest
{
    Id = portfolioId
};

var response = await client.GetPortfolioAsync(request, metadata);
```

los servicios de gRPC pueden tener acceso a los metadatos de la propiedad `RequestHeaders` del argumento `ServerCallContext`:

```csharp
public async Task<GetPortfolioResponse> GetPortfolio(GetPortfolioRequest request, ServerCallContext context)
{
    var requesterHeader = context.RequestHeaders.FirstOrDefault(e => e.Key == "Requester");
    if (requesterHeader != null)
    {
        _logger.LogInformation($"Request from {requesterHeader.Value}");
    }
    // ...
}
```

Los servicios pueden enviar metadatos a los clientes mediante la propiedad `ResponseTrailers` de `ServerCallContext`:

```csharp
public async Task<GetPortfolioResponse> GetPortfolio(GetPortfolioRequest request, ServerCallContext context)
{
    // ...
    context.ResponseTrailers.Add("Responder", _serverName);
    // ...
}
```

>[!div class="step-by-step"]
>[Anterior](rpc-types.md)
>[Siguiente](error-handling.md)
