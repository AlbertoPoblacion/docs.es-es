---
ms.openlocfilehash: d35de48dd22003c851cf5dba9e8517ec48b9217b
ms.sourcegitcommit: 5a28f8eb071fcc09b045b0c4ae4b96898673192e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/31/2019
ms.locfileid: "73198563"
---
### <a name="c-locale-maps-to-the-invariant-locale"></a>La configuración regional de “C” se asigna a la configuración regional invariable

.NET Core 2.2 y las versiones anteriores dependen del comportamiento predeterminado de ICU, el cual asigna la configuración regional de “C” a la configuración regional en_US_POSIX. La configuración regional en_US_POSIX tiene un comportamiento de intercalación no deseado, porque no admite comparaciones de cadenas que no distinguen mayúsculas de minúsculas. Algunas distribuciones de Linux establecían la configuración regional de “C” como la configuración regional predeterminada, por lo que los usuarios experimentaban un comportamiento inesperado.

#### <a name="change-description"></a>Descripción del cambio

A partir de .NET Core 3.0, la asignación de la configuración regional de “C” ha cambiado para usar la configuración regional invariable en lugar de en_US_POSIX. La configuración regional de “C” con la asignación invariable también se aplica a Windows para mantener la coherencia.

La asignación de “C” a la referencia cultural en_US_POSIX causaba confusión entre los clientes porque en_US_POSIX no admite operaciones de ordenación y búsqueda de cadenas que no distinguen mayúsculas de minúsculas. Dado que la configuración regional de “C” se usa como configuración regional predeterminada en algunas de las distribuciones de Linux, los clientes experimentaron este comportamiento no deseado en estos sistemas operativos.

#### <a name="version-introduced"></a>Versión introducida

3.0

### <a name="recommended-action"></a>Acción recomendada

Nada más aparte de conocer este cambio. Este cambio solo afecta a las aplicaciones que usan la asignación de configuración regional de “C”.

### <a name="category"></a>Categoría

Globalización

### <a name="affected-apis"></a>API afectadas

Este cambio afecta a todas las API de intercalación y de referencia cultural.

<!--

-->
