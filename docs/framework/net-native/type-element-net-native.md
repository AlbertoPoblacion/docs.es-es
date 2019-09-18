---
title: <Type>Elemento (.NET Native)
ms.date: 03/30/2017
ms.assetid: 1e88d368-a886-4f1e-8eb6-6127979a9fce
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 7ffe37540fe089bfd1e0eca1958498e725eb9b5b
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/17/2019
ms.locfileid: "71049151"
---
# <a name="type-element-net-native"></a>\<Elemento > de tipo (.NET Native)

Aplica la directiva de tiempo de ejecución a un tipo determinado, como una clase o estructura.

## <a name="syntax"></a>Sintaxis

```xml
<Type Name="type_name"
      Activate="policy_type"
      Browse="policy_type"
      Dynamic="policy_type"
      Serialize="policy_type"
      DataContractSerializer="policy_setting"
      DataContractJsonSerializer="policy_setting"
      XmlSerializer="policy_setting"
      MarshalObject="policy_setting"
      MarshalDelegate="policy_setting"
      MarshalStructure="policy_setting" />
```

## <a name="attributes-and-elements"></a>Atributos y elementos

En las siguientes secciones se describen los atributos, los elementos secundarios y los elementos primarios.

### <a name="attributes"></a>Atributos

|Atributo|Tipo de atributo|DESCRIPCIÓN|
|---------------|--------------------|-----------------|
|`Name`|General|Atributo necesario. Especifica el nombre del tipo.|
|`Activate`|Reflexión|Atributo opcional. Controla el acceso en tiempo de ejecución a los constructores para permitir la activación de instancias.|
|`Browse`|Reflexión|Atributo opcional. Controla la consulta para obtener información sobre los elementos de programa, pero no permite el acceso en tiempo de ejecución.|
|`Dynamic`|Reflexión|Atributo opcional. Controla el acceso en tiempo de ejecución a todos los miembros de tipo (incluidos constructores, métodos, campos, propiedades y eventos) para permitir la programación dinámica.|
|`Serialize`|Serialización|Atributo opcional. Controla el acceso en tiempo de ejecución a constructores, campos y propiedades para permitir que bibliotecas como el serializador JSON Newtonsoft puedan serializar y deserializar instancias de tipo.|
|`DataContractSerializer`|Serialización|Atributo opcional. Controla la directiva de serialización que usa la clase <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=nameWithType>.|
|`DataContractJsonSerializer`|Serialización|Atributo opcional. Controla la directiva de serialización JSON que usa la clase <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer?displayProperty=nameWithType>.|
|`XmlSerializer`|Serialización|Atributo opcional. Controla la directiva de serialización XML que usa la clase <xref:System.Xml.Serialization.XmlSerializer?displayProperty=nameWithType>.|
|`MarshalObject`|Interop|Atributo opcional. Controla la directiva de serialización de tipos de referencia a Windows Runtime y COM.|
|`MarshalDelegate`|Interop|Atributo opcional. Controla la directiva de serialización de tipos de delegado como punteros de función a código nativo.|
|`MarshalStructure`|Interop|Atributo opcional. Controla la directiva de cálculo de referencias de tipos de valor a código nativo.|

## <a name="name-attribute"></a>Name (atributo)

|Valor|DESCRIPCIÓN|
|-----------|-----------------|
|*type_name*|Nombre del tipo. Si este elemento `<Type>` es el elemento secundario de un elemento [\<Namespace>](namespace-element-net-native.md) o de otro elemento `<Type>`, *type_name* puede incluir el nombre del tipo sin su espacio de nombres. De lo contrario, *type_name* debe incluir el nombre de tipo completo.|

## <a name="all-other-attributes"></a>Resto de atributos

|Value|DESCRIPCIÓN|
|-----------|-----------------|
|*policy_setting*|Configuración que se va a aplicar a este tipo de directiva. Los valores posibles son `All`, `Auto`, `Excluded`, `Public`, `PublicAndInternal`, `Required Public`, `Required PublicAndInternal` y `Required All`. Para obtener más información, vea [Runtime Directive Policy Settings](runtime-directive-policy-settings.md) (Configuración de directiva de la directiva en tiempo de ejecución).|

### <a name="child-elements"></a>Elementos secundarios

|Elemento|DESCRIPCIÓN|
|-------------|-----------------|
|[\<AttributeImplies>](attributeimplies-element-net-native.md)|Si el tipo contenedor es un atributo, define la directiva de tiempo de ejecución para elementos de código a los que se aplica el atributo.|
|[\<Event>](event-element-net-native.md)|Aplica la directiva de reflexión a un evento perteneciente a este tipo.|
|[\<Field>](field-element-net-native.md)|Aplica la directiva de reflexión a un campo de este tipo.|
|[\<GenericParameter>](genericparameter-element-net-native.md)|Aplica la directiva al tipo del parámetro de tipo genérico.|
|[\<ImpliesType>](impliestype-element-net-native.md)|Aplica la directiva a un tipo, en caso de que dicha directiva se haya aplicado al tipo representado por el elemento `<Type>` que lo contiene.|
|[\<Method>](method-element-net-native.md)|Aplica la directiva de reflexión a un método perteneciente a este tipo.|
|[\<MethodInstantiation>](methodinstantiation-element-net-native.md)|Aplica la directiva de reflexión a un método genérico construido perteneciente a este tipo.|
|[\<Property>](property-element-net-native.md)|Aplica la directiva de reflexión a una propiedad de este tipo.|
|[\<Subtypes>](subtypes-element-net-native.md)|Aplica la directiva en tiempo de ejecución a todas las clases heredadas del tipo contenedor.|
|`<Type>`|Aplica la directiva de reflexión a un tipo anidado.|
|[\<TypeInstantiation>](typeinstantiation-element-net-native.md)|Aplica la directiva de reflexión a un tipo genérico construido.|

### <a name="parent-elements"></a>Elementos primarios

|Elemento|DESCRIPCIÓN|
|-------------|-----------------|
|[\<Application>](application-element-net-native.md)|Sirve de contenedor de los tipos y miembros de tipo de la aplicación cuyos metadatos están disponibles para la reflexión en tiempo de ejecución.|
|[\<Assembly>](assembly-element-net-native.md)|Aplica la directiva de reflexión a todos los tipos en un ensamblado especificado.|
|[\<Library>](library-element-net-native.md)|Define el ensamblado que contiene los tipos y miembros de tipo cuyos metadatos están disponibles para la reflexión en tiempo de ejecución.|
|[\<Namespace>](namespace-element-net-native.md)|Aplica la directiva de reflexión a todos los tipos en un espacio de nombres.|
|`<Type>`|Aplica la directiva de reflexión a un tipo y a todos sus miembros.|
|[\<TypeInstantiation>](typeinstantiation-element-net-native.md)|Aplica la directiva de reflexión a un tipo genérico construido y a todos sus miembros.|

## <a name="remarks"></a>Comentarios

La reflexión, la serialización y los atributos de interoperabilidad son opcionales. Si ninguno de ellos está presente, el elemento `<Type>` actúa como un contenedor cuyos tipos secundarios definen directivas para los miembros individuales.

Si un elemento `<Type>` es el elemento secundario de un elemento [\<Assembly>](assembly-element-net-native.md), [\<Namespace>](namespace-element-net-native.md), `<Type>` o [\<TypeInstantiation>](typeinstantiation-element-net-native.md), invalida la configuración de directiva definida por el elemento primario.

Un elemento `<Type>` de un tipo genérico aplica su directiva a todas las instancias que no tienen su propia directiva. La directiva de los tipos genéricos construidos se define mediante el elemento [\<TypeInstantiation>](typeinstantiation-element-net-native.md).

Si el tipo es un tipo genérico, su nombre se decora con un símbolo de acento grave (\`) seguido por el número de parámetros genéricos. Por ejemplo, el atributo `Name` de un elemento `<Type>` de la clase <xref:System.Collections.Generic.List%601?displayProperty=nameWithType> aparece como ``Name="System.Collections.Generic.List`1"``.

## <a name="example"></a>Ejemplo

En el ejemplo siguiente se utiliza la reflexión para mostrar información sobre los campos, las propiedades y los métodos de la clase <xref:System.Collections.Generic.List%601?displayProperty=nameWithType>. La variable `b` del ejemplo es un <xref:Windows.UI.Xaml.Controls.TextBlock> control. Dado que el ejemplo simplemente recupera información de tipos, la disponibilidad de los metadatos se controla mediante la configuración de directiva `Browse`.

 [!code-csharp[ProjectN_Reflection#3](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn_reflection/cs/browsegenerictype1.cs#3)]

 Dado que la cadena <xref:System.Collections.Generic.List%601> de herramientas de .net Native no incluye de forma automática los metadatos de la clase, en el ejemplo no se muestra la información de miembro solicitada en tiempo de ejecución. Para proporcionar los metadatos necesarios, agregue el elemento `<Type>` siguiente al archivo de directivas en tiempo de ejecución. Tenga en cuenta que, dado que se ha proporcionado un elemento primario [<Namespace\>](namespace-element-net-native.md), no es necesario proporcionar un nombre de tipo completo en el elemento `<Type>`.

```xml
<Directives xmlns="http://schemas.microsoft.com/netfx/2013/01/metadata">
   <Application>
      <Assembly Name="*Application*" Dynamic="Required All" />
      <Namespace Name ="System.Collections.Generic" >
        <Type Name="List`1" Browse="Required All" />
     </Namespace>
   </Application>
</Directives>
```

## <a name="example"></a>Ejemplo
 En el ejemplo siguiente se utiliza la reflexión para recuperar un objeto <xref:System.Reflection.PropertyInfo> que representa a la propiedad <xref:System.String.Chars%2A?displayProperty=nameWithType>. A continuación, se utiliza el método <xref:System.Reflection.PropertyInfo.GetValue%28System.Object%2CSystem.Object%5B%5D%29?displayProperty=nameWithType> para recuperar el valor del séptimo carácter de una cadena y para mostrar todos los caracteres de la cadena. La variable `b` del ejemplo es un <xref:Windows.UI.Xaml.Controls.TextBlock> control.

 [!code-csharp[ProjectN_Reflection#1](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn_reflection/cs/propertyinfo1.cs#1)]

 Dado <xref:System.String> quelosmetadatos<xref:System.NullReferenceException> del objeto no están disponibles, la llamada al métodoproduceunaexcepciónentiempodeejecucióncuandosecompilaconlacadenadeherramientasde.netNative.<xref:System.Reflection.PropertyInfo.GetValue%28System.Object%2CSystem.Object%5B%5D%29?displayProperty=nameWithType> Para eliminar la excepción y proporcionar los metadatos necesarios, agregue el siguiente elemento `<Type>` al archivo de directivas en tiempo de ejecución:

```xml
<Directives xmlns="http://schemas.microsoft.com/netfx/2013/01/metadata">
  <Application>
    <Assembly Name="*Application*" Dynamic="Required All" />
    <Type Name="System.String" Dynamic="Required Public"/> -->
  </Application>
</Directives>
```

## <a name="see-also"></a>Vea también

- [Runtime Directives (rd.xml) Configuration File Reference (Referencia del archivo de configuración de directivas en tiempo de ejecución (rd.xml))](runtime-directives-rd-xml-configuration-file-reference.md)
- [Runtime Directive Elements (Elementos de directivas en tiempo de ejecución)](runtime-directive-elements.md)
- [Runtime Directive Policy Settings](runtime-directive-policy-settings.md) (Configuración de directiva de la directiva en tiempo de ejecución)
