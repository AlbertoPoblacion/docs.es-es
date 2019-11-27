---
title: Eventos ETW de CLR
ms.date: 03/30/2017
helpviewer_keywords:
- CLR ETW events
- ETW, common language runtime
- ETW, CLR events
ms.assetid: ef2b31c3-7426-43e7-9924-92339b96556d
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 951941af2568e72fe093860801bd2595b3037e41
ms.sourcegitcommit: 9a39f2a06f110c9c7ca54ba216900d038aa14ef3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/23/2019
ms.locfileid: "74428168"
---
# <a name="clr-etw-events"></a>Eventos ETW de CLR
Los temas de esta sección describen los eventos de seguimiento de eventos para Windows (ETW). Cada evento tiene una palabra clave y un nivel asociados que se describen en el tema [Palabras clave y niveles ETW de CLR](clr-etw-keywords-and-levels.md). CLR tiene dos proveedores para los eventos:  
  
- El proveedor en tiempo de ejecución genera eventos en función de las palabras clave (categorías de eventos) que están habilitadas. El GUID del proveedor en tiempo de ejecución de CLR es e13c0d23-ccbc-4e12-931b-d9cc2eee27e4.  
  
- El proveedor de informe detallado, que es para fines especiales. El GUID del proveedor de informe detallado de CLR es a669021c-c450-4609-a035-5af59af4df18.  
  
 Para más información, vea [Proveedores ETW de CLR](clr-etw-providers.md).  
  
## <a name="in-this-section"></a>Esta sección  
 [Eventos de información en tiempo de ejecución](runtime-information-etw-events.md)  
 Capturan información sobre el tiempo de ejecución, lo que incluye la SKU, el número de versión, la manera en que se ha activado el tiempo de ejecución, los parámetros de línea de comandos con los que se ha iniciado, el GUID (si está disponible) y otra información relevante.  
  
 [Evento de excepción Thrown_V1](exception-thrown-v1-etw-event.md)  
 Captura información de excepciones.  
  
 [Eventos de contención](contention-etw-events.md)  
 Capturan información sobre la contención para bloqueos de monitor o nativos que use el tiempo de ejecución.  
  
 [Eventos de grupos de subprocesos](thread-pool-etw-events.md)  
 Capturan información sobre grupos de subprocesos de trabajo y de E/S.  
  
 [Eventos de cargador](loader-etw-events.md)  
 Capturan información sobre la carga y descarga de dominios, ensamblados y módulos de aplicación.  
  
 [Eventos de método](method-etw-events.md)  
 Capturan información sobre métodos CLR para resolución de símbolo.  
  
 [Eventos de recolección de elementos no utilizados](garbage-collection-etw-events.md)  
 Capturan información relativa a la recolección de elementos no utilizados, para facilitar la depuración y el diagnóstico.  
  
 [Eventos de traza JIT](jit-tracing-etw-events.md)  
 Capturan información sobre inclusión en línea JIT y llamadas de cola.  
  
 [Eventos de interoperabilidad](interop-etw-events.md)  
 Capturan información sobre generación de código auxiliar y almacenamiento en memoria caché del lenguaje intermedio de Microsoft (MSIL).  
  
 [Eventos ARM](application-domain-resource-monitoring-arm-etw-events.md)  
 Capturan información de diagnóstico detallada sobre el estado de un dominio de aplicación.  
  
 [Eventos de seguridad](security-etw-events.md)  
 Capturan información sobre verificación de nombres seguros y Authenticode.  
  
 [Evento de pila](stack-etw-event.md)  
 Captura información usada con otros eventos para generar seguimientos de pilas después de que se haya generado un evento.  
  
## <a name="see-also"></a>Vea también

- [Mejorar la depuración y el ajuste del rendimiento con ETW](https://docs.microsoft.com/archive/msdn-magazine/2007/april/event-tracing-improve-debugging-and-performance-tuning-with-etw)
- [Blog de rendimiento de Windows](https://blogs.msdn.microsoft.com/pigscanfly/tag/xperf/)
- [Controlar el registro de .NET Framework](controlling-logging.md)
- [Proveedores ETW de CLR](clr-etw-providers.md)
- [Palabras clave y niveles ETW de CLR](clr-etw-keywords-and-levels.md)
- [Eventos ETW en Common Language Runtime](etw-events-in-the-common-language-runtime.md)
