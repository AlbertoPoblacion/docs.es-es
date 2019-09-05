---
title: Funciones canónicas de cadena
ms.date: 03/30/2017
ms.assetid: 5e2cbebd-5df3-47c7-b0e2-49a17ab22bfb
ms.openlocfilehash: 9013b8bd8505442666dd0688eaf2586959a61b70
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2019
ms.locfileid: "70249088"
---
# <a name="string-canonical-functions"></a>Funciones canónicas de cadena
[!INCLUDE[esql](../../../../../../includes/esql-md.md)] incluye funciones canónicas de cadena.  
  
## <a name="remarks"></a>Comentarios  
 En la tabla siguiente se muestran las funciones canónicas de cadena de [!INCLUDE[esql](../../../../../../includes/esql-md.md)].  
  
|Función|DESCRIPCIÓN|  
|--------------|-----------------|  
|`Concat(string1, string2)`|Devuelve una cadena que contiene una `string2` anexada a `string1`.<br /><br /> **Argumentos**<br /><br /> `string1`: Cadena a la que `string2` se anexa.<br /><br /> `string2`: Cadena que se anexa a `string1`.<br /><br /> **Valor devuelto**<br /><br /> Objeto `String`. Se producirá un error si la longitud de la cadena del valor devuelto es mayor que la longitud máxima permitida.<br /><br /> **Ejemplo**<br /><br /> `-- The following example returns abcxyz.`<br /><br /> `Concat('abc', 'xyz')`|  
|`Contains(string, target)`|Devuelve `true` si `target` está incluida en `string`.<br /><br /> **Argumentos**<br /><br /> `string`: Cadena en la que se busca.<br /><br /> `target`: Cadena de destino que se busca.<br /><br /> **Valor devuelto**<br /><br /> Es `true` si `target` está incluida en `string`; de lo contrario, es `false`.<br /><br /> **Ejemplo**<br /><br /> `-- The following example returns true.`<br /><br /> `Contains('abc', 'bc')`|  
|`EndsWith(string, target)`|Devuelve `true` si la cadena `target` está situada al final de la cadena `string`.<br /><br /> **Argumentos**<br /><br /> `string`: Cadena en la que se busca.<br /><br /> `target`: La cadena de destino que se busca al final de `string`.<br /><br /> **Valor devuelto**<br /><br /> `True` si `string` termina por `target`; de lo contrario `false`.<br /><br /> **Ejemplo**<br /><br /> `-- The following example returns true.`<br /><br /> `EndsWith('abc', 'bc')` **Nota:**  Si usa el proveedor de datos SQL Server, esta función devuelve `false` si la cadena está almacenada en una columna de cadena de longitud fija y `target` es una constante. En este caso, se buscará en toda la cadena, incluyendo los espacios finales de relleno que pueda haber. Una posible solución alternativa es recortar los datos de la cadena de longitud fija, como en el ejemplo siguiente: `EndsWith(TRIM(string), target)`|  
|`IndexOf(target, string)`|Devuelve la posición de `target` dentro de `string`, o 0 si no se encuentra. Devuelve 1 para indicar el principio de `string`. La numeración del índice empieza a partir de 1.<br /><br /> **Argumentos**<br /><br /> `target`: Cadena que se busca.<br /><br /> `string`: Cadena en la que se busca.<br /><br /> **Valor devuelto**<br /><br /> Una clase `Int32`.<br /><br /> **Ejemplo**<br /><br /> `-- The following example returns 4.`<br /><br /> `IndexOf('xyz', 'abcxyz')`|  
|`Left(string, length)`|Devuelve los primeros `length` caracteres del lado izquierdo de `string`. Si la longitud de `string` es menor que `length`, se devuelve la cadena entera.<br /><br /> **Argumentos**<br /><br /> `string`: OBJETO `String`.<br /><br /> `length`: `Int16`, ,`Int32` O`Byte`. `Int64` El parámetro `length` no puede ser menor que cero.<br /><br /> **Valor devuelto**<br /><br /> Objeto `String`.<br /><br /> **Ejemplo**<br /><br /> `-- The following example returns abc.`<br /><br /> `Left('abcxyz', 3)`|  
|`Length(string)`|Devuelve la longitud (`Int32`) de la cadena en caracteres.<br /><br /> **Argumentos**<br /><br /> `string`: OBJETO `String`.<br /><br /> **Valor devuelto**<br /><br /> Una clase `Int32`.<br /><br /> **Ejemplo**<br /><br /> `-- The following example returns 6.`<br /><br /> `Legth('abcxyz')`|  
|`LTrim(string)`|Devuelve `string` sin el espacio en blanco inicial.<br /><br /> **Argumentos**<br /><br /> Objeto `String`.<br /><br /> **Valor devuelto**<br /><br /> Objeto `String`.<br /><br /> **Ejemplo**<br /><br /> `-- The following example returns abc.`<br /><br /> `LTrim('   abc')`|  
|`Replace(string1, string2, string3)`|Devuelve `string1`, con todas las apariciones de `string2` reemplazadas por `string3`.<br /><br /> **Argumentos**<br /><br /> Objeto `String`.<br /><br /> **Valor devuelto**<br /><br /> Objeto `String`.<br /><br /> **Ejemplo**<br /><br /> `-- The following example returns abcxyz.`<br /><br /> `Concat('abc', 'xyz')`|  
|`Reverse(string)`|Devuelve `string` con el orden de los caracteres invertidos.<br /><br /> **Argumentos**<br /><br /> Objeto `String`.<br /><br /> **Valor devuelto**<br /><br /> Objeto `String`.<br /><br /> **Ejemplo**<br /><br /> `-- The following example returns dcba.`<br /><br /> `Reverse('abcd')`|  
|`Right(string, length)`|Devuelve los últimos `length` caracteres `string`de. Si la longitud de `string` es menor que `length`, se devuelve la cadena entera.<br /><br /> **Argumentos**<br /><br /> `string`: OBJETO `String`.<br /><br /> `length`: `Int16`, ,`Int32` O`Byte`. `Int64` El parámetro `length` no puede ser menor que cero.<br /><br /> **Valor devuelto**<br /><br /> Objeto `String`.<br /><br /> **Ejemplo**<br /><br /> `-- The following example returns xyz.`<br /><br /> `Right('abcxyz', 3)`|  
|`RTrim(string)`|Devuelve `string` sin el espacio en blanco al final.<br /><br /> **Argumentos**<br /><br /> Objeto `String`.<br /><br /> **Valor devuelto**<br /><br /> Objeto `String`.|  
|`Substring(string, start, length)`|Devuelve la subcadena de la cadena a partir de la posición `start`, con una longitud de `length` caracteres. Si se inicia a partir de 1, indica el primer carácter de la cadena. La numeración del índice empieza a partir de 1.<br /><br /> **Argumentos**<br /><br /> `string`: OBJETO `String`.<br /><br /> `start`: `Int16` ,`Int32`Y .`Byte` `Int64` El parámetro `start` no puede ser menor que uno.<br /><br /> `length`: `Int16` ,`Int32`Y .`Byte` `Int64` El parámetro `length` no puede ser menor que cero.<br /><br /> **Valor devuelto**<br /><br /> Objeto `String`.<br /><br /> **Ejemplo**<br /><br /> `-- The following example returns xyz.`<br /><br /> `Substring('abcxyz', 4, 3)`|  
|`StartsWith(string, target)`|Devuelve `true` si el objeto `string` comienza por `target`.<br /><br /> **Argumentos**<br /><br /> `string`: Cadena en la que se busca.<br /><br /> `target`: La cadena de destino que se busca al principio de `string`.<br /><br /> **Valor devuelto**<br /><br /> `True` si el objeto `string` comienza por `target`; de lo contrario, `false`.<br /><br /> **Ejemplo**<br /><br /> `-- The following example returns true.`<br /><br /> `StartsWith('abc', 'ab')`|  
|`ToLower(string)`|Devuelve una `string` con los caracteres en mayúscula pasados a minúscula.<br /><br /> **Argumentos**<br /><br /> Objeto `String`.<br /><br /> **Valor devuelto**<br /><br /> Objeto `String`.<br /><br /> **Ejemplo**<br /><br /> `-- The following example returns abc.`<br /><br /> `ToLower('ABC')`|  
|`ToUpper(string)`|Devuelve una `string` con los caracteres en minúscula pasados a mayúscula.<br /><br /> **Argumentos**<br /><br /> Objeto `String`.<br /><br /> **Valor devuelto**<br /><br /> Objeto `String`.<br /><br /> **Ejemplo**<br /><br /> `-- The following example returns ABC.`<br /><br /> `ToUpper('abc')`|  
|`Trim(string)`|Devuelve `string` sin espacios en blanco iniciales y finales.<br /><br /> **Argumentos**<br /><br /> Objeto `String`.<br /><br /> **Valor devuelto**<br /><br /> Objeto `String`.<br /><br /> **Ejemplo**<br /><br /> `-- The following example returns abc.`<br /><br /> `Trim('      abc   ')`|  
  
 Estas funciones devolverán `null` si se proporciona la entrada `null`.  
  
 La funcionalidad equivalente está disponible en el proveedor administrado de Microsoft SQL Client. Para obtener más información, vea [SqlClient para funciones de Entity Framework](../sqlclient-for-ef-functions.md).  
  
## <a name="see-also"></a>Vea también

- [Funciones canónicas](canonical-functions.md)
