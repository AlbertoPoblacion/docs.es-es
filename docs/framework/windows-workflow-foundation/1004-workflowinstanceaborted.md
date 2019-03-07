---
title: 1004 - WorkflowInstanceAborted
ms.date: 03/30/2017
ms.assetid: edb9ab8c-0b9a-488d-aa96-9c8c7984b53c
ms.openlocfilehash: d34f6f1ab6af8e06a0f28fb043faf9fe16a8b211
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/06/2019
ms.locfileid: "57485192"
---
# <a name="1004---workflowinstanceaborted"></a>1004 - WorkflowInstanceAborted

## <a name="properties"></a>Propiedades

|||
|-|-|
|Id.|1004|
|Palabras clave|WFRuntime|
|Nivel|Información|
|Canal|Microsoft-Windows-Application Server-Applications/Debug|

## <a name="description"></a>Descripción

Indica que una instancia de flujo de trabajo se ha anulado con una excepción.

## <a name="message"></a>Mensaje

WorkflowInstance Id: '%1' se anuló con una excepción.

## <a name="details"></a>Detalles

|Nombre del elemento de datos|Tipo del elemento de datos|Descripción|
|--------------------|--------------------|-----------------|
|WorkflowInstanceId|`xs:string`|El id. de instancia del flujo de trabajo.|
|Excepción|`xs:string`|Detalles de la excepción para la excepción|
|AppDomain|`xs:string`|La cadena devuelta por AppDomain.CurrentDomain.FriendlyName.|
