---
title: <add> elemento para NameValueSectionHandler y DictionarySectionHandler
ms.date: 05/01/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/sectionName/add
helpviewer_keywords:
- add Element
- <add> Element
ms.assetid: 0d4ddb53-eb2b-49c0-9c33-a8dec5c39b46
author: guardrex
ms.author: mairaw
ms.openlocfilehash: 9b421b4bab32c1aae7a6ba7d69b9f4aea2ab99a5
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61705498"
---
# <a name="add-element-for-namevaluesectionhandler-and-dictionarysectionhandler"></a>\<Agregar > elemento para NameValueSectionHandler y DictionarySectionHandler

Agrega la configuración de aplicación personalizada. Cada  **\<Agregar >** etiqueta contiene un par clave/valor.

[**\<configuration>**](~/docs/framework/configure-apps/file-schema/configuration-element.md)   
&nbsp;&nbsp;[**\<sectionName>**](~/docs/framework/configure-apps/file-schema/custom-element-2.md)   
&nbsp;&nbsp;&nbsp;&nbsp;**\<add>**

## <a name="syntax"></a>Sintaxis

```xml
<add key="key" value="value" />
```

## <a name="attributes"></a>Atributos

| Atributo | Descripción |
| --------- | ----------- |
| **key**   | Atributo necesario.<br><br>Especifica el nombre de la configuración. |
| **value** | Atributo necesario.<br><br>Especifica el valor de la configuración. |

## <a name="parent-element"></a>Elemento primario

| Elemento | Descripción |
| ------- | ------------|
| [**\<sectionName >** elemento](~/docs/framework/configure-apps/file-schema/custom-element-2.md) | Define los valores de las secciones de configuración personalizada que utilicen el <xref:System.Configuration.NameValueSectionHandler> y <xref:System.Configuration.DictionarySectionHandler> clases. |

## <a name="child-elements"></a>Elementos secundarios

Ninguna

## <a name="example"></a>Ejemplo

El ejemplo siguiente muestra cómo definir una sección de configuración personalizado y usar el  **\<Agregar >** elemento para que la configuración en la sección:

```xml
<configuration>
  <configSections>
    <section name="dictionarySample" type="System.Configuration.DictionarySectionHandler,System" />
  </configSections>
  <dictionarySample>
    <add key="myKey" value="myValue" />
  </dictionarySample>
</configuration>
```

## <a name="configuration-file"></a>Archivo de configuración

Este elemento se puede usar en el archivo de configuración de aplicación, archivo de configuración del equipo (*Machine.config*), y *Web.config* archivos que no están en el nivel de directorio de aplicación.

## <a name="see-also"></a>Vea también

- [Esquema de archivo de configuración de .NET Framework](~/docs/framework/configure-apps/file-schema/index.md)
