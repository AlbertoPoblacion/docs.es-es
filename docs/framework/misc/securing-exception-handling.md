---
title: Proteger control de excepciones
ms.date: 03/30/2017
dev_langs:
- cpp
helpviewer_keywords:
- code security, exception handling
- security [.NET Framework], exception handling
- secure coding, exception handling
- exception handling, security
ms.assetid: 1f3da743-9742-47ff-96e6-d0dd1e9e1c19
author: mairaw
ms.author: mairaw
ms.openlocfilehash: bc8cd20a4183ffd002f1399b6b50c8956208a21b
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61868813"
---
# <a name="securing-exception-handling"></a>Proteger control de excepciones
En Visual C++ y Visual Basic, se ejecuta una expresión de filtro más arriba en la pila antes de cualquier **finalmente** instrucción. El **catch** bloque asociado con ese filtro se ejecuta después el **finalmente** instrucción. Para obtener más información, consulte [excepciones filtradas por el usuario](../../../docs/standard/exceptions/using-user-filtered-exception-handlers.md). Esta sección examinan las implicaciones de seguridad de este pedido. Considere el siguiente ejemplo de pseudocódigo que ilustra el orden en que las instrucciones de filtro y **finalmente** ejecutar las instrucciones.  
  
```cpp  
void Main()   
{  
    try   
    {  
        Sub();  
    }   
    except (Filter())   
    {  
        Console.WriteLine("catch");  
    }  
}  
bool Filter () {  
    Console.WriteLine("filter");  
    return true;  
}  
void Sub()   
{  
    try   
    {  
        Console.WriteLine("throw");  
        throw new Exception();  
    }   
    finally   
    {  
        Console.WriteLine("finally");  
    }  
}                        
```  
  
 Este código imprime lo siguiente.  
  
```  
Throw  
Filter  
Finally  
Catch  
```  
  
 El filtro se ejecuta antes que la **finalmente** instrucción, por lo que se pueden introducir problemas de seguridad en todo aquello que hace que un estado cambie a aprovechar la ejecución de otro código. Por ejemplo:  
  
```cpp  
try   
{  
    Alter_Security_State();  
    // This means changing anything (state variables,  
    // switching unmanaged context, impersonation, and   
    // so on) that could be exploited if malicious   
    // code ran before state is restored.  
    Do_some_work();  
}   
finally   
{  
    Restore_Security_State();  
    // This simply restores the state change above.  
}  
```  
  
 Este pseudocódigo permite que un filtro situado más arriba en la pila para ejecutar código arbitrario. Otros ejemplos de operaciones que pueden tener un efecto similar son temporal suplantación de identidad de otro, un marcador interno que omita alguna comprobación de seguridad, o cambiar la referencia cultural asociada al subproceso. La solución recomendada es introducir un controlador de excepciones para aislar los cambios del código para el estado del subproceso de bloques de filtro de los llamadores. Sin embargo, es importante que el controlador de excepciones se ha introducido correctamente o no se corregirá este problema. En el ejemplo siguiente se cambia la referencia cultural de interfaz de usuario, pero cualquier tipo de cambio de estado de subproceso podría mostrarse de forma similar.  
  
```cpp  
YourObject.YourMethod()  
{  
   CultureInfo saveCulture = Thread.CurrentThread.CurrentUICulture;  
   try {  
      Thread.CurrentThread.CurrentUICulture = new CultureInfo("de-DE");  
      // Do something that throws an exception.  
}  
   finally {  
      Thread.CurrentThread.CurrentUICulture = saveCulture;  
   }  
}  
```  
  
```vb  
Public Class UserCode  
   Public Shared Sub Main()  
      Try  
         Dim obj As YourObject = new YourObject  
         obj.YourMethod()  
      Catch e As Exception When FilterFunc  
         Console.WriteLine("An error occurred: '{0}'", e)  
         Console.WriteLine("Current Culture: {0}",   
Thread.CurrentThread.CurrentUICulture)  
      End Try  
   End Sub  
  
   Public Function FilterFunc As Boolean  
      Console.WriteLine("Current Culture: {0}", Thread.CurrentThread.CurrentUICulture)  
      Return True  
   End Sub  
  
End Class  
```  
  
 En este caso es la solución adecuada ajustar la existente **intente**/**finalmente** bloquear un **intente**/**catch** bloque. Introducir un **catch throw** cláusula existentes **intente**/**finalmente** bloque no soluciona el problema, tal como se muestra en el ejemplo siguiente.  
  
```cpp  
YourObject.YourMethod()  
{  
    CultureInfo saveCulture = Thread.CurrentThread.CurrentUICulture;  
  
    try   
    {  
        Thread.CurrentThread.CurrentUICulture = new CultureInfo("de-DE");  
        // Do something that throws an exception.  
    }  
    catch { throw; }  
    finally   
    {  
        Thread.CurrentThread.CurrentUICulture = saveCulture;  
    }  
}  
```  
  
 Esto no soluciona el problema porque el **finalmente** instrucción no se ha ejecutado antes el `FilterFunc` obtiene control.  
  
 En el ejemplo siguiente se corrige el problema asegurándose de que el **finalmente** cláusula ha ejecutado antes de generar una excepción de los bloques de filtro de excepción de los llamadores.  
  
```cpp  
YourObject.YourMethod()  
{  
    CultureInfo saveCulture = Thread.CurrentThread.CurrentUICulture;  
    try    
    {  
        try   
        {  
            Thread.CurrentThread.CurrentUICulture = new CultureInfo("de-DE");  
            // Do something that throws an exception.  
        }  
        finally   
        {  
            Thread.CurrentThread.CurrentUICulture = saveCulture;  
        }  
    }  
    catch { throw; }  
}  
```  
  
## <a name="see-also"></a>Vea también

- [Instrucciones de codificación segura](../../../docs/standard/security/secure-coding-guidelines.md)
