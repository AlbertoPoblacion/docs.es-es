---
title: <section> elemento
ms.date: 05/01/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/configSections/section
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/configSections/sectionGroup/section
helpviewer_keywords:
- section Element
- <section> Element
ms.assetid: ec7d4110-2403-47ac-8218-499bfe9d5ddb
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 8c1675540df6844f98572c11cfb140bff23b31a8
ms.sourcegitcommit: 7f8eeef060ddeb2cabfa52843776faf652c5a1f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/14/2019
ms.locfileid: "74089018"
---
# <a name="section-element"></a>\<sección > elemento

Contiene una declaración de sección de configuración.

[ **\<configuration>** ](configuration-element.md)\
&nbsp;&nbsp;[ **\<configSections >** ](configsections-element-for-configuration.md)\
&nbsp;&nbsp;&nbsp;&nbsp; **\<sección** >

[ **\<configuration>** ](configuration-element.md)\
&nbsp;&nbsp;[ **\<configSections >** ](configsections-element-for-configuration.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<sectionGroup**](sectiongroup-element-for-configsections.md) >\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\<**sección** >

## <a name="syntax"></a>Sintaxis

```xml
<section name="section name"
         type="configuration section handler class, assembly"
         allowDefinition="Everywhere|MachineOnly|MachineToApplication" 
         allowLocation="true|false" />
```

## <a name="required-attributes"></a>Atributos requeridos

|           | Descripción |
| --------- | ----------- |
| **name**  | Especifica el nombre de la sección de configuración. |
| **type**  | Especifica el nombre de la clase de controlador de la sección de configuración que lee la sección del archivo de configuración. El valor de tipo tiene la sintaxis "Full-Qualified-Section-Handler-Class-Name, simple-Assembly-name". El nombre de ensamblado simple es el nombre de archivo raíz sin la extensión de archivo *. dll* . |

## <a name="optional-attributes"></a>Atributos opcionales

Los atributos siguientes solo son aplicables a las aplicaciones ASP.NET. El sistema de configuración omite estos atributos para otros tipos de aplicaciones.

|                     | Descripción |
| ------------------- | ----------- |
| **allowDefinition** | Especifica el archivo de configuración en el que se puede usar la sección. Utilice uno de los siguientes valores:<br><br>**Todas**<br>Permite que la sección se use en cualquier archivo de configuración. Este es el valor predeterminado.<br>**MachineOnly**<br>Permite que la sección se use solo en el archivo de configuración del equipo (*Machine. config*).<br>**MachineToApplication**<br>Permite usar la sección en el archivo de configuración del equipo o en el archivo de configuración de la aplicación. |
| **allowLocation**   | Determina si la sección se puede usar dentro del elemento de **> de ubicación\<** . Utilice uno de los siguientes valores:<br><br>**true**<br>Permite que la sección se use dentro del elemento **\<location >** . Este es el valor predeterminado.<br>**false**<br>No permite el uso de la sección dentro del elemento **\<location >** . |

## <a name="parent-elements"></a>Elementos primarios

|     | Descripción |
| --- | ----------- |
| [ **\<configSections >** Element](configsections-element-for-configuration.md) | Contiene la sección de configuración y las declaraciones de espacio de nombres. |
| [ **\<sectionGroup >** Element](sectiongroup-element-for-configsections.md) | Define un espacio de nombres para las secciones de configuración. |

> [!NOTE]
> Una **\<sección >** elemento es un elemento secundario de **\<configSections >** o **\<sectionGroup** >, pero no ambos.

## <a name="child-elements"></a>Elementos secundarios

Ninguno

## <a name="remarks"></a>Comentarios

Al declarar una sección de configuración, básicamente se define un nuevo elemento para el archivo de configuración. El nuevo elemento contiene valores que lee un controlador de sección de configuración (es decir, una clase que implementa la interfaz <xref:System.Configuration.IConfigurationSectionHandler>). Los atributos y elementos secundarios de una sección que se define dependen del controlador de la sección que se usa para leer la configuración.

Declarar un controlador de sección de configuración en el archivo *Machine. config* permite usar la sección de configuración en cualquier archivo de configuración de la aplicación de ese equipo, a menos que el atributo **allowDefinition** especifique lo contrario.

## <a name="example"></a>Ejemplo

En el ejemplo siguiente se muestra cómo definir una sección de configuración y definir la configuración de esa sección:

```xml
<configuration>
  <configSections>
    <section name="sampleSection"
             type="System.Configuration.SingleTagSectionHandler" 
             allowLocation="false" />
  </configSections>
  <sampleSection setting1="Value1" 
                 setting2="value two" 
                 setting3="third value" />
</configuration>
```

## <a name="configuration-file"></a>Archivo de configuración

Este elemento puede usarse en el archivo de configuración de la aplicación, el archivo de configuración del equipo (*Machine. config*) y los archivos *Web. config* que no están en el nivel de directorio de la aplicación.

## <a name="see-also"></a>Vea también

- [Esquema del archivo de configuración para el .NET Framework](index.md)
