---
title: Eventos ETW de contención - .NET
ms.date: 03/30/2017
helpviewer_keywords:
- contention events [.NET Framework]
- ETW, contention events (CLR)
ms.assetid: 6933e753-2f2a-425b-ae84-42138c957d76
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 95f56a6c8b51c58ed36d5d0de428bf57b728009c
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61723945"
---
# <a name="contention-etw-events"></a>Eventos ETW de contención

Los eventos de contención se generan cuando el tiempo de ejecución usa contención de bloqueos <xref:System.Threading.Monitor?displayProperty=nameWithType> o nativos. La contención se produce cuando un subproceso espera un bloqueo mientras otro posee el bloqueo.

En la tabla siguiente se muestra la palabra clave bajo la que se generan los eventos de contención y el nivel de los eventos. Para obtener más información, consulte [CLR ETW Keywords and Levels](clr-etw-keywords-and-levels.md).

|Palabra clave para generar el evento|Nivel|
|-----------------------------------|-----------|
|`ContentionKeyword` (0x4000)|Informativo (4)|

En la tabla siguiente se muestra la información de evento:

|evento|Id. de evento|Se genera cuando|
|-----------|--------------|-----------------|
|`ContentionStart_V1`|81|Se inicia la contención. Este evento no incluye la cantidad de tiempo de giro antes de que un subproceso comience a esperar para adquirir un bloqueo; solo se genera cuando el subproceso espera para adquirir un bloqueo.|
|`ContentionStop`|91|Finaliza la contención.|

La siguiente tabla muestra los datos del evento:

|Nombre de campo|Tipo de datos|Descripción|
|----------------|---------------|-----------------|
|Marcas|win:UInt8|0 para administrado; 1 para nativo.|
|ClrInstanceID|win:UInt16|Identificador único para la instancia de CLR.|

## <a name="see-also"></a>Vea también

- [CLR ETW Events (Eventos ETW de CLR)](clr-etw-events.md)
