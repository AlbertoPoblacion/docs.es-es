---
title: Funciones canónicas de cadena
ms.date: 03/30/2017
ms.assetid: 5e2cbebd-5df3-47c7-b0e2-49a17ab22bfb
ms.openlocfilehash: bfd18f0302b897dabd7c75118e3892df6153ea63
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61797714"
---
# <a name="string-canonical-functions"></a>Funciones canónicas de cadena
[!INCLUDE[esql](../../../../../../includes/esql-md.md)] incluye funciones canónicas de cadena.  
  
## <a name="remarks"></a>Comentarios  
 En la tabla siguiente se muestran las funciones canónicas de cadena de [!INCLUDE[esql](../../../../../../includes/esql-md.md)].  
  
|Función|Descripción|  
|--------------|-----------------|  
|`Concat(string1, string2)`|Devuelve una cadena que contiene una `string2` anexada a `string1`.<br /><br /> **Argumentos**<br /><br /> `string1`: La cadena a la que `string2` se anexa.<br /><br /> `string2`: La cadena que se anexa a `string1`.<br /><br /> **Valor devuelto**<br /><br /> Objeto `String`. Se producirá un error si la longitud de la cadena del valor devuelto es mayor que la longitud máxima permitida.<br /><br /> **Ejemplo**<br /><br /> `-- The following example returns abcxyz.`<br /><br /> `Concat('abc', 'xyz')`|  
|`Contains(string, target)`|Devuelve `true` si `target` está incluida en `string`.<br /><br /> **Argumentos**<br /><br /> `string`: Cadena que se va a buscar.<br /><br /> `target`: La cadena de destino que se va a buscar.<br /><br /> **Valor devuelto**<br /><br /> Es `true` si `target` está incluida en `string`; de lo contrario, es `false`.<br /><br /> **Ejemplo**<br /><br /> `-- The following example returns true.`<br /><br /> `Contains('abc', 'bc')`|  
|`EndsWith(string, target)`|Devuelve `true` si la cadena `target` está situada al final de la cadena `string`.<br /><br /> **Argumentos**<br /><br /> `string`: Cadena que se va a buscar.<br /><br /> `target`: La cadena de destino que se busca al final de `string`.<br /><br /> **Valor devuelto**<br /><br /> `True` si `string` termina por `target`; de lo contrario `false`.<br /><br /> **Ejemplo**<br /><br /> `-- The following example returns true.`<br /><br /> `EndsWith('abc', 'bc')` **Nota:**  Si está utilizando el proveedor de datos de SQL Server, esta función devuelve `false` si la cadena se almacena en una columna de cadena de longitud fija y `target` es una constante. En este caso, se buscará en toda la cadena, incluyendo los espacios finales de relleno que pueda haber. Una posible solución alternativa es recortar los datos de la cadena de longitud fija, como en el ejemplo siguiente: `EndsWith(TRIM(string), target)`|  
|`IndexOf(target, string)`|Devuelve la posición de `target` dentro de `string`, o 0 si no se encuentra. Devuelve 1 para indicar el principio de `string`. La numeración del índice empieza a partir de 1.<br /><br /> **Argumentos**<br /><br /> `target`: Cadena que se va a buscar.<br /><br /> `string`: Cadena que se va a buscar.<br /><br /> **Valor devuelto**<br /><br /> Una clase `Int32`.<br /><br /> **Ejemplo**<br /><br /> `-- The following example returns 4.`<br /><br /> `IndexOf('xyz', 'abcxyz')`|  
|`Left(string, length)`|Devuelve los primeros `length` caracteres del lado izquierdo de `string`. Si la longitud de `string` es menor que `length`, se devuelve la cadena entera.<br /><br /> **Argumentos**<br /><br /> `string`: OBJETO `String`.<br /><br /> `length`: Un `Int16`, `Int32`, `Int64`, o `Byte`. El parámetro `length` no puede ser menor que cero.<br /><br /> **Valor devuelto**<br /><br /> Objeto `String`.<br /><br /> **Ejemplo**<br /><br /> `-- The following example returns abc.`<br /><br /> `Left('abcxyz', 3)`|  
|`Length(string)`|Devuelve la longitud (`Int32`) de la cadena en caracteres.<br /><br /> **Argumentos**<br /><br /> `string`: OBJETO `String`.<br /><br /> **Valor devuelto**<br /><br /> Una clase `Int32`.<br /><br /> **Ejemplo**<br /><br /> `-- The following example returns 6.`<br /><br /> `Legth('abcxyz')`|  
|`LTrim(string)`|Devuelve `string` sin espacio en blanco inicial.<br /><br /> **Argumentos**<br /><br /> Objeto `String`.<br /><br /> **Valor devuelto**<br /><br /> Objeto `String`.<br /><br /> **Ejemplo**<br /><br /> `-- The following example returns abc.`<br /><br /> `LTrim('   abc')`|  
|`Replace(string1, string2, string3)`|Devuelve `string1`, con todas las apariciones de `string2` reemplazadas por `string3`.<br /><br /> **Argumentos**<br /><br /> Objeto `String`.<br /><br /> **Valor devuelto**<br /><br /> Objeto `String`.<br /><br /> **Ejemplo**<br /><br /> `-- The following example returns abcxyz.`<br /><br /> `Concat('abc', 'xyz')`|  
|`Reverse(string)`|Devuelve `string` con el orden de los caracteres invertidos.<br /><br /> **Argumentos**<br /><br /> Objeto `String`.<br /><br /> **Valor devuelto**<br /><br /> Objeto `String`.<br /><br /> **Ejemplo**<br /><br /> `-- The following example returns dcba.`<br /><br /> `Reverse('abcd')`|  
|`Right(string, length)`|Devuelve el último `length` caracteres desde el `string`. Si la longitud de `string` es menor que `length`, se devuelve la cadena entera.<br /><br /> **Argumentos**<br /><br /> `string`: OBJETO `String`.<br /><br /> `length`: Un `Int16`, `Int32`, `Int64`, o `Byte`. El parámetro `length` no puede ser menor que cero.<br /><br /> **Valor devuelto**<br /><br /> Objeto `String`.<br /><br /> **Ejemplo**<br /><br /> `-- The following example returns xyz.`<br /><br /> `Right('abcxyz', 3)`|  
|`RTrim(string)`|Devuelve `string` sin espacios en blanco finales.<br /><br /> **Argumentos**<br /><br /> Objeto `String`.<br /><br /> **Valor devuelto**<br /><br /> Objeto `String`.|  
|`Substring(string, start, length)`|Devuelve la subcadena de la cadena a partir de la posición `start`, con una longitud de `length` caracteres. Si se inicia a partir de 1, indica el primer carácter de la cadena. La numeración del índice empieza a partir de 1.<br /><br /> **Argumentos**<br /><br /> `string`: OBJETO `String`.<br /><br /> `start`: Un `Int16`, `Int32`, `Int64` y `Byte`. El parámetro `start` no puede ser menor que uno.<br /><br /> `length`: Un `Int16`, `Int32`, `Int64` y `Byte`. El parámetro `length` no puede ser menor que cero.<br /><br /> **Valor devuelto**<br /><br /> Objeto `String`.<br /><br /> **Ejemplo**<br /><br /> `-- The following example returns xyz.`<br /><br /> `Substring('abcxyz', 4, 3)`|  
|`StartsWith(string, target)`|Devuelve `true` si el objeto `string` comienza por `target`.<br /><br /> **Argumentos**<br /><br /> `string`: Cadena que se va a buscar.<br /><br /> `target`: La cadena de destino que se busca al principio de `string`.<br /><br /> **Valor devuelto**<br /><br /> `True` si el objeto `string` comienza por `target`; de lo contrario, `false`.<br /><br /> **Ejemplo**<br /><br /> `-- The following example returns true.`<br /><br /> `StartsWith('abc', 'ab')`|  
|`ToLower(string)`|Devuelve una `string` con los caracteres en mayúscula pasados a minúscula.<br /><br /> **Argumentos**<br /><br /> Objeto `String`.<br /><br /> **Valor devuelto**<br /><br /> Objeto `String`.<br /><br /> **Ejemplo**<br /><br /> `-- The following example returns abc.`<br /><br /> `ToLower('ABC')`|  
|`ToUpper(string)`|Devuelve una `string` con los caracteres en minúscula pasados a mayúscula.<br /><br /> **Argumentos**<br /><br /> Objeto `String`.<br /><br /> **Valor devuelto**<br /><br /> Objeto `String`.<br /><br /> **Ejemplo**<br /><br /> `-- The following example returns ABC.`<br /><br /> `ToUpper('abc')`|  
|`Trim(string)`|Devuelve `string` sin espacio en blanco inicial y final.<br /><br /> **Argumentos**<br /><br /> Objeto `String`.<br /><br /> **Valor devuelto**<br /><br /> Objeto `String`.<br /><br /> **Ejemplo**<br /><br /> `-- The following example returns abc.`<br /><br /> `Trim('      abc   ')`|  
  
 Estas funciones devolverán `null` si se proporciona la entrada `null`.  
  
 La funcionalidad equivalente está disponible en el proveedor administrado de Microsoft SQL Client. Para obtener más información, consulte [SqlClient para las funciones de Entity Framework](../../../../../../docs/framework/data/adonet/ef/sqlclient-for-ef-functions.md).  
  
## <a name="see-also"></a>Vea también

- [Funciones canónicas](../../../../../../docs/framework/data/adonet/ef/language-reference/canonical-functions.md)
