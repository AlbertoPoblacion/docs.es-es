---
title: Elemento &lt;Property&gt; (.NET Native)
ms.date: 03/30/2017
ms.assetid: ad4ba56d-3bcb-4c10-ba90-1cc66e2175a1
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 74fd4fa1387836e12d186a604f6996254eabf956
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/23/2019
ms.locfileid: "54549423"
---
# <a name="ltpropertygt-element-net-native"></a>Elemento &lt;Property&gt; (.NET Native)
Aplica la directiva de reflexión en tiempo de ejecución a una propiedad.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
<Property Name="property_name"  
          Browse="policy_type"  
          Dynamic="policy_type"  
          Serialize="policy_type" />  
```  
  
## <a name="attributes-and-elements"></a>Atributos y elementos  
 En las siguientes secciones se describen los atributos, los elementos secundarios y los elementos primarios.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Tipo de atributo|Descripción|  
|---------------|--------------------|-----------------|  
|`Name`|General|Atributo necesario. Especifica el nombre de la propiedad.|  
|`Browse`|Reflexión|Atributo opcional. Controla la consulta para obtener información acerca de la propiedad o la enumeración de la propiedad, pero no permite el acceso dinámico en tiempo de ejecución.|  
|`Dynamic`|Reflexión|Atributo opcional. Controla el acceso en tiempo de ejecución a la propiedad para permitir la programación dinámica. Esta directiva garantiza que una propiedad se puede establecer o recuperar dinámicamente en tiempo de ejecución.|  
|`Serialize`|Serialización|Atributo opcional. Controla el acceso en tiempo de ejecución a una propiedad para permitir que bibliotecas como el serializador JSON Newtonsoft puedan serializar instancias de tipo o que estas puedan usarse para enlazar datos.|  
  
## <a name="name-attribute"></a>Name (atributo)  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*method_name*|Nombre de la propiedad. El tipo de la propiedad se define mediante el elemento primario [\<Type>](../../../docs/framework/net-native/type-element-net-native.md) o [\<TypeInstantiation>](../../../docs/framework/net-native/typeinstantiation-element-net-native.md).|  
  
## <a name="all-other-attributes"></a>Todos los demás atributos  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*policy_setting*|Configuración que se aplica a este tipo de directiva para la propiedad. Los valores posibles son `Auto`, `Excluded`, `Included` y `Required`. Para obtener más información, vea [Runtime Directive Policy Settings](../../../docs/framework/net-native/runtime-directive-policy-settings.md) (Configuración de directiva de la directiva en tiempo de ejecución).|  
  
### <a name="child-elements"></a>Elementos secundarios  
 Ninguno.  
  
### <a name="parent-elements"></a>Elementos primarios  
  
|Elemento|Descripción|  
|-------------|-----------------|  
|[\<Type>](../../../docs/framework/net-native/type-element-net-native.md)|Aplica la directiva de reflexión a un tipo y a todos sus miembros.|  
|[\<TypeInstantiation>](../../../docs/framework/net-native/typeinstantiation-element-net-native.md)|Aplica la directiva de reflexión a un tipo genérico construido y a todos sus miembros.|  
  
## <a name="remarks"></a>Comentarios  
 Si la directiva de una propiedad no está definida explícitamente, hereda la directiva en tiempo de ejecución de su elemento primario.  
  
## <a name="example"></a>Ejemplo  
 En el siguiente ejemplo se usa la reflexión para crear instancias de un objeto `Book` y mostrar sus valores de propiedad. El archivo default.rd.xml original del proyecto se muestra así:  
  
```xml  
<Directives xmlns="http://schemas.microsoft.com/netfx/2013/01/metadata">  
   <Application>  
      <Namespace Name="LibraryApplications"  Browse="Required Public" >  
         <Type Name="Book"   Activate="All" />  
      </Namespace>  
   </Application>  
</Directives>  
```  
  
 El archivo se aplica el valor `All` a la directiva `Activate` de la clase `Book`, lo que permite el acceso a los constructores de clase mediante reflexión. La directiva `Browse` para la `Book` clase se hereda de su espacio de nombres primario. Esto se establece en `Required Public`, que hace que los metadatos estén disponibles en tiempo de ejecución.  
  
 A continuación se muestra el código fuente del ejemplo. El `outputBlock` variable representa un <xref:Windows.UI.Xaml.Controls.TextBlock> control.  
  
 [!code-csharp[ProjectN_Reflection#6](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn_reflection/cs/property1.cs#6)]  
  
 Sin embargo, compilar y ejecutar este ejemplo genera una excepción [MissingRuntimeArtifactException](../../../docs/framework/net-native/missingruntimeartifactexception-class-net-native.md). Aunque hemos puesto a disposición los metadatos correspondientes a `Book`, no hemos podido llevar a cabo las implementaciones de los captadores de propiedades disponibles dinámicamente. Podemos corregir este error mediante una de estas dos maneras:  
  
-   Definiendo la directiva `Dynamic` para el tipo `Book` en su elemento [\<Type>](../../../docs/framework/net-native/type-element-net-native.md).  
  
-   Agregando un elemento [\<Property>](../../../docs/framework/net-native/property-element-net-native.md) anidado por cada propiedad cuyo captador se quiere invocar, como sucede en el siguiente archivo default.rd.xml.  
  
    ```xml  
    <Directives xmlns="http://schemas.microsoft.com/netfx/2013/01/metadata">  
       <Application>  
          <Namespace Name="LibraryApplications"  Browse="Required Public" >  
             <Type Name="Book"   Activate="All" >  
                <Property Name="Title" Dynamic="Required" />  
                <Property Name="Author" Dynamic="Required" />  
                  <Property Name="ISBN" Dynamic="Required" />  
             </Type>  
          </Namespace>  
       </Application>  
    </Directives>  
    ```  
  
## <a name="see-also"></a>Vea también
- [Runtime Directives (rd.xml) Configuration File Reference (Referencia del archivo de configuración de directivas en tiempo de ejecución (rd.xml))](../../../docs/framework/net-native/runtime-directives-rd-xml-configuration-file-reference.md)
- [Runtime Directive Elements (Elementos de directivas en tiempo de ejecución)](../../../docs/framework/net-native/runtime-directive-elements.md)
- [Runtime Directive Policy Settings](../../../docs/framework/net-native/runtime-directive-policy-settings.md) (Configuración de directiva de la directiva en tiempo de ejecución)
