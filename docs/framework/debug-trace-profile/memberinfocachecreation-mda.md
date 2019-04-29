---
title: MDA de memberInfoCacheCreation
ms.date: 03/30/2017
helpviewer_keywords:
- member info cache creation
- MemberInfoCacheCreation MDA
- reflection, run-time errors
- MDAs (managed debugging assistants), cache
- cache [.NET Framework], reflection
- managed debugging assistants (MDAs), cache
- MemberInfo cache
ms.assetid: 5abdad23-1335-4744-8acb-934002c0b6fe
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 90f59f4d593a8aa077a6710cc0f5c1747ac1a3ad
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61754006"
---
# <a name="memberinfocachecreation-mda"></a>MDA de memberInfoCacheCreation
El asistente para la depuración administrada (MDA) `memberInfoCacheCreation` se activa cuando se crea una caché de <xref:System.Reflection.MemberInfo>. Esto es una indicación clara de un programa que está usando características de reflexión que consumen muchos recursos.  
  
## <a name="symptoms"></a>Síntomas  
 El espacio de trabajo de un programa aumenta porque el programa está usando reflexión que consume muchos recursos.  
  
## <a name="cause"></a>Motivo  
 Las operaciones de reflexión que implican dos objetos <xref:System.Reflection.MemberInfo> se consideran que consumen muchos recursos porque deben leer metadatos que se almacenan en páginas frías y en general indican que el programa usa algún tipo de escenario enlazado en tiempo de ejecución.  
  
## <a name="resolution"></a>Resolución  
 Puede determinar dónde se usa la reflexión en su programa si habilita este MDA y, después, ejecuta el código en un depurador o lo adjunta con un depurador cuando se activa el MDA. Bajo un depurador obtendrá un seguimiento de pila en el que se muestra dónde se creó la caché de <xref:System.Reflection.MemberInfo> y desde allí puede determinar dónde usa la reflexión el programa.  
  
 La resolución depende de los objetivos del código. Este MDA le avisa de que el programa tiene un escenario enlazado en tiempo de ejecución. Es posible que quiera determinar si puede sustituir un escenario enlazado en tiempo de compilación o considerar el rendimiento del escenario enlazado en tiempo de ejecución.  
  
## <a name="effect-on-the-runtime"></a>Efecto en el Runtime  
 Este MDA se activa para cada caché de <xref:System.Reflection.MemberInfo> que se crea. El rendimiento se ve afectado de forma insignificante.  
  
## <a name="output"></a>Salida  
 El MDA genera un mensaje que indica que se creó la caché de <xref:System.Reflection.MemberInfo>. Use un depurador para realizar un seguimiento de pila en el que se muestre dónde usa la reflexión el programa.  
  
## <a name="configuration"></a>Configuración  
  
```xml  
<mdaConfig>  
  <assistants>  
    <memberInfoCacheCreation/>  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="example"></a>Ejemplo  
 Este código de ejemplo activará el MDA `memberInfoCacheCreation`.  
  
```csharp
using System;  
  
public class Exe  
{  
    public static void Main()  
    {  
        typeof(object).GetMethods();  
    }  
}  
```  
  
## <a name="see-also"></a>Vea también

- <xref:System.Reflection.MemberInfo>
- [Diagnosing Errors with Managed Debugging Assistants (Diagnóstico de errores con asistentes para la depuración administrada)](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)
