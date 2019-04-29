---
title: Campo ServicePoint.m_ConnectionGroupList
ms.date: 05/01/2017
topic_type:
- apiref
api_name:
- System.Net.ServicePoint.m_ConnectionGroupList
api_location:
- System.dll
api_type:
- Assembly
ms.assetid: df8afb59-f0f6-4ddc-b3c1-839b9fc601d8
author: guardrex
ms.author: mairaw
ms.openlocfilehash: a764c74dc0927094675b0f5e0916a4ad29f04250
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61705953"
---
# <a name="servicepointmconnectiongrouplist-field"></a>ServicePoint.m\_ConnectionGroupList campo

`ServicePoint.m_ConnectionGroupList` es un <xref:System.Collections.Hashtable> de grupos de conexión, cada uno mantiene una conexión para el <xref:System.Net.ServicePoint>del URI.

## <a name="syntax"></a>Sintaxis
  
```csharp  
private Hashtable m_ConnectionGroupList
```

> [!WARNING]
> El `ServicePoint.m_ConnectionGroupList` campo es privado y no está pensado para usarse directamente en el código.
> 
> Microsoft no admite el uso de este campo en una aplicación de producción bajo ninguna circunstancia.

## <a name="requirements"></a>Requisitos

**Espacio de nombres:** <xref:System.Net>

**Ensamblado:** Sistema (en System.dll)

**Versiones de .NET framework:** Disponible desde la versión 2.0.
