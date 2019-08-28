---
title: Categorías de cambios importantes - .NET Core
description: Obtenga información sobre la forma de clasificar los cambios importantes en .NET Core.
author: rpetrusha
ms.author: ronpet
ms.date: 06/10/2019
ms.openlocfilehash: 68cd3580e80305e54b41610f05d939a6aff8b54d
ms.sourcegitcommit: a970268118ea61ce14207e0916e17243546a491f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/21/2019
ms.locfileid: "69577157"
---
# <a name="breaking-change-categories"></a>Categorías de cambios importantes

*Compatibilidad* hace referencia a la capacidad de compilar o ejecutar código en una versión de una implementación .NET distinta a la que se utilizó originalmente para desarrollar el código. Un cambio determinado puede repercutir en la compatibilidad de seis formas distintas. Los [tipos de cambios individuales que se tienen en cuenta al evaluar la compatibilidad](index.md) se incluyen en las cinco primeras categorías. 

## <a name="behavioral-change"></a>Cambio de comportamiento

Un cambio de comportamiento representa un cambio en el comportamiento de un miembro. El cambio puede ser visible externamente (por ejemplo, un método puede producir una excepción diferente) o puede representar una implementación modificada (por ejemplo, un cambio en la forma en que se calcula un valor devuelto, la adición o eliminación de llamadas a métodos internos o incluso una mejora significativa del rendimiento).

Cuando los cambios de comportamiento son visibles externamente y modifican el contrato público de un tipo, se pueden evaluar fácilmente, ya que repercuten en la compatibilidad binaria. Los cambios de implementación son mucho más difíciles de evaluar. En función de la naturaleza del cambio y de la frecuencia y los patrones de uso de la API, el impacto de un cambio puede ir de grave a inocuo.  

## <a name="binary-compatibility"></a>Compatibilidad binaria

La compatibilidad binaria hace referencia a la capacidad de un consumidor de una API de usar la API en una versión más reciente sin volver a compilar. Los cambios como agregar métodos o agregar la implementación de una nueva interfaz a un tipo no repercuten en la compatibilidad binaria. Pero eliminar o modificar las firmas públicas de un ensamblado para que los consumidores dejen de tener acceso a la misma interfaz expuesta por el ensamblado sí que repercute en la compatibilidad binaria. Los cambios de este tipo se denominan *cambios binarios no compatibles*.

## <a name="source-compatibility"></a>Compatibilidad de origen

 La compatibilidad de origen hace referencia a la capacidad de los consumidores existentes de que una API vuelva a compilar con una versión más reciente sin ningún cambio de origen. Un *cambio de origen incompatible* se produce cuando un consumidor necesita modificar el código fuente para que se compile correctamente en una versión más reciente de una API.

## <a name="design-time-compatibility"></a>Compatibilidad en tiempo de diseño

La compatibilidad en tiempo de diseño hace referencia a la conservación de la experiencia de tiempo de diseño en diferentes versiones de Visual Studio y otros entornos de tiempo de diseño. Aunque esto puede afectar al comportamiento o a la interfaz de usuario de los diseñadores, el aspecto más importante de la compatibilidad en tiempo de diseño repercute en la compatibilidad del proyecto. Un proyecto o solución debe poder abrirse y usarse en una versión más reciente del entorno de tiempo de diseño.

## <a name="backwards-compatibility"></a>Compatibilidad con versiones anteriores

La compatibilidad con versiones anteriores hace referencia a la capacidad de un consumidor de una API existente de ejecutarse en una versión nueva con el mismo comportamiento. Tanto los cambios de comportamiento como los cambios en la compatibilidad binaria repercuten en la compatibilidad con versiones anteriores. Si un consumidor no puede ejecutarse o se comporta de forma diferente cuando se ejecuta en la versión más reciente de la API, la API *no es compatible con versiones anteriores*.

Los cambios que repercuten en la compatibilidad con versiones anteriores no se recomiendan, ya que los desarrolladores, de forma predeterminada, esperan una compatibilidad con versiones anteriores en las versiones más recientes de una API.

## <a name="forward-compatibility"></a>Compatibilidad con versiones posteriores

La compatibilidad con versiones posteriores hace referencia a la capacidad de un consumidor de una API existente de ejecutarse en una versión anterior con el mismo comportamiento. Si un consumidor no puede ejecutarse o se comporta de forma diferente cuando se ejecuta en una versión anterior de la API, la API *no es compatible con versiones posteriores*. 

Mantener la compatibilidad con versiones posteriores excluye prácticamente cualquier cambio o adición de una versión a otra, ya que esos cambios impiden que un consumidor que tiene como destino una versión posterior se ejecute en una versión anterior. Los desarrolladores esperan que un consumidor que depende de una API más reciente podría no funcionar correctamente con la API anterior. 

Mantener la compatibilidad con versiones posteriores no es un objetivo de .NET Core.

## <a name="see-also"></a>Vea también

[Evaluación de los cambios importantes en .NET Core](index.md)
