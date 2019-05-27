---
title: Elementos de directivas en tiempo de ejecución
ms.date: 03/30/2017
ms.assetid: 3fe5848c-ecd7-4136-970b-8e48d250bde6
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: fb3ad0d39d47297b7d26a5c28cfbbc269ce99e44
ms.sourcegitcommit: 7e129d879ddb42a8b4334eee35727afe3d437952
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66052413"
---
# <a name="runtime-directive-elements"></a>Elementos de directivas en tiempo de ejecución
El formato del archivo de directivas de tiempo de ejecución (rd.xml) es compatible con los siguientes elementos de directiva de tiempo de ejecución. Vea [Runtime Directives (rd.xml) Configuration File Reference](../../../docs/framework/net-native/runtime-directives-rd-xml-configuration-file-reference.md) (Referencia del archivo de configuración de directivas en tiempo de ejecución (rd.xml)) para obtener una representación jerárquica.  
  
 [\<Application>](../../../docs/framework/net-native/application-element-net-native.md)  
 Aplica la directiva de reflexión en tiempo de ejecución a todos los tipos utilizados por la aplicación y sirve como contenedor para los miembros de tipos y los tipos de toda la aplicación cuyos metadatos están disponibles para la reflexión en tiempo de ejecución. Se trata de un elemento secundario del elemento [\<Directives>](../../../docs/framework/net-native/directives-element-net-native.md).  
  
 [\<Assembly>](../../../docs/framework/net-native/assembly-element-net-native.md)  
 Aplica la directiva de tiempo de ejecución a todos los tipos de un ensamblado. Se trata de un elemento secundario de los elementos [\<Application>](../../../docs/framework/net-native/application-element-net-native.md) y [\<Library>](../../../docs/framework/net-native/library-element-net-native.md).  
  
 [\<AttributeImplies>](../../../docs/framework/net-native/attributeimplies-element-net-native.md)  
 Si la directiva [\<Type>](../../../docs/framework/net-native/type-element-net-native.md) que contiene es un atributo, aplica la directiva en tiempo de ejecución a los elementos de código a los que se les aplica dicho atributo.  
  
 [\<Directives>](../../../docs/framework/net-native/directives-element-net-native.md)  
 El elemento raíz en cada archivo de directivas en tiempo de ejecución de .NET Native. Sus elementos secundarios son [\<Application>](../../../docs/framework/net-native/application-element-net-native.md) y [\<Library>](../../../docs/framework/net-native/library-element-net-native.md).  
  
 [\<Event>](../../../docs/framework/net-native/event-element-net-native.md)  
 Aplica la directiva de tiempo de ejecución a un evento. Se trata de un elemento secundario de los elementos [\<Type>](../../../docs/framework/net-native/type-element-net-native.md) y [\<TypeInstantiation>](../../../docs/framework/net-native/typeinstantiation-element-net-native.md).  
  
 [\<Field>](../../../docs/framework/net-native/field-element-net-native.md)  
 Aplica la directiva de tiempo de ejecución a un campo. Se trata de un elemento secundario de los elementos [\<Type>](../../../docs/framework/net-native/type-element-net-native.md) y [\<TypeInstantiation>](../../../docs/framework/net-native/typeinstantiation-element-net-native.md).  
  
 [\<GenericParameter>](../../../docs/framework/net-native/genericparameter-element-net-native.md)  
 Aplica la directiva de tiempo de ejecución al tipo de parámetro de un método o tipo genérico.  
  
 [\<ImpliesType>](../../../docs/framework/net-native/impliestype-element-net-native.md)  
 Aplica la directiva de tiempo de ejecución a un tipo, si dicha directiva se ha aplicado al tipo contenedor o al método.  
  
 [\<Library>](../../../docs/framework/net-native/library-element-net-native.md)  
 Aplica la directiva de tiempo de ejecución a todos los tipos de un ensamblado. Se trata de un elemento secundario de los elementos [\<Application>](../../../docs/framework/net-native/application-element-net-native.md) y [\<Library>](../../../docs/framework/net-native/library-element-net-native.md).  
  
 [\<Method>](../../../docs/framework/net-native/method-element-net-native.md)  
 Aplica la directiva de tiempo de ejecución a un método. Se trata de un elemento secundario de los elementos [\<Type>](../../../docs/framework/net-native/type-element-net-native.md) y [\<TypeInstantiation>](../../../docs/framework/net-native/typeinstantiation-element-net-native.md).  
  
 [\<MethodInstantiation>](../../../docs/framework/net-native/methodinstantiation-element-net-native.md)  
 Aplica la directiva de tiempo de ejecución a un método genérico construido. Se trata de un elemento secundario de los elementos [\<Type>](../../../docs/framework/net-native/type-element-net-native.md) y [\<TypeInstantiation>](../../../docs/framework/net-native/typeinstantiation-element-net-native.md).  
  
 [\<Namespace>](../../../docs/framework/net-native/namespace-element-net-native.md)  
 Aplica la directiva de tiempo de ejecución a todos los tipos de un espacio de nombres.  
  
 [\<Parameter>](../../../docs/framework/net-native/parameter-element-net-native.md)  
 Aplica la directiva de tiempo de ejecución al tipo del argumento que se pasa a un método.  
  
 [\<Property>](../../../docs/framework/net-native/property-element-net-native.md)  
 Aplica la directiva de tiempo de ejecución a una propiedad. Se trata de un elemento secundario de los elementos [\<Type>](../../../docs/framework/net-native/type-element-net-native.md) y [\<TypeInstantiation>](../../../docs/framework/net-native/typeinstantiation-element-net-native.md).  
  
 [\<Subtypes>](../../../docs/framework/net-native/subtypes-element-net-native.md)  
 Aplica la directiva en tiempo de ejecución a todas las clases heredadas del tipo contenedor.  
  
 [\<Type>](../../../docs/framework/net-native/type-element-net-native.md)  
 Aplica la directiva de tiempo de ejecución a un tipo.  
  
 [\<TypeInstantiation>](../../../docs/framework/net-native/typeinstantiation-element-net-native.md)  
 Aplica la directiva de tiempo de ejecución a un tipo genérico construido.  
  
 [\<TypeParameter>](../../../docs/framework/net-native/typeparameter-element-net-native.md)  
 Aplica la directiva de tiempo de ejecución al tipo representado por un argumento <xref:System.Type> que se pasa a un método.  
  
## <a name="see-also"></a>Vea también

- [Referencia del archivo de configuración rd.xml](../../../docs/framework/net-native/runtime-directives-rd-xml-configuration-file-reference.md)
