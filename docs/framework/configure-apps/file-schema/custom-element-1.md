---
title: Elemento personalizado para SingleTagSectionHandler
ms.date: 05/01/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/sectionName
helpviewer_keywords:
- custom element
ms.assetid: e62056c6-b351-40eb-afc0-cc13fc44e45e
author: rpetrusha
ms.author: mairaw
ms.openlocfilehash: ad98617cd4e88d1650f67136536b7dd5994233a4
ms.sourcegitcommit: 621a5f6df00152006160987395b93b5b55f7ffcd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/29/2019
ms.locfileid: "66301151"
---
# <a name="custom-element-for-singletagsectionhandler"></a>Elemento personalizado para SingleTagSectionHandler

Define la configuración en una sección de configuración personalizada que se define mediante un \<sección > elemento y se usa el <xref:System.Configuration.SingleTagSectionHandler> clase.

[ **\<configuration>** ](~/docs/framework/configure-apps/file-schema/configuration-element.md)   
&nbsp;&nbsp; *\<sectionName>*

## <a name="syntax"></a>Sintaxis

```xml
<sectionName key="value" key2="value2" ... />
```

## <a name="attributes"></a>Atributos

Atributos y valores de atributo son definidos por el usuario.

## <a name="parent-element"></a>Elemento primario

|     | Descripción |
| --- | ----------- |
| [ **\<configuration>** ](~/docs/framework/configure-apps/file-schema/configuration-element.md) | Elemento raíz de cada archivo de configuración usado por las aplicaciones de Common Language Runtime y .NET Framework. |

## <a name="child-elements"></a>Elementos secundarios

Ninguna

## <a name="remarks"></a>Comentarios

El  **\<sectionName >** trata de un elemento personalizado definido por una [  **\<sección >** ](~/docs/framework/configure-apps/file-schema/section-element.md) etiquetar en el [  **\<configSections >** ](~/docs/framework/configure-apps/file-schema/configsections-element-for-configuration.md) elemento. Devuelve el sistema de configuración un <xref:System.Collections.IDictionary> objeto cuando se llama a <xref:System.Configuration.Configuration.GetSection(System.String)?displayProperty=nameWithType>.

## <a name="example"></a>Ejemplo

En el ejemplo siguiente se declara un elemento personalizado llamado  **\<sampleSection >** que contiene los valores leídos por la <xref:System.Configuration.SingleTagSectionHandler> clase:

```xml
<configuration>
  <configSections>
    <section name="sampleSection" 
             type="System.Configuration.SingleTagSectionHandler" />
  </configSections>
  <sampleSection setting1="Value1" 
                 setting2="value two" 
                 setting3="third value" />
</configuration>
```

## <a name="configuration-file"></a>Archivo de configuración

Este elemento se puede usar en el archivo de configuración de aplicación, archivo de configuración del equipo (*Machine.config*), y *Web.config* archivos que no están en el nivel de directorio de aplicación.

## <a name="see-also"></a>Vea también

- [Esquema de archivo de configuración de .NET Framework](~/docs/framework/configure-apps/file-schema/index.md)
