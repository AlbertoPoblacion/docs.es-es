---
title: 'Cómo: Buscar caracteres en una cadena (LINQ)'
ms.date: 07/20/2015
ms.assetid: 499ebbe0-746c-4235-9dba-ce722c12b50e
ms.openlocfilehash: 9da6d5abd6155a7af5ec59e17693e8acae7e7b73
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/22/2019
ms.locfileid: "74347722"
---
# <a name="how-to-query-for-characters-in-a-string-linq-visual-basic"></a>Cómo: buscar caracteres en una cadena (LINQ) (Visual Basic)

Como la clase <xref:System.String> implementa la interfaz <xref:System.Collections.Generic.IEnumerable%601> genérica, cualquier cadena puede consultarse como una secuencia de caracteres. Pero esto no es un uso habitual de LINQ. Para operaciones de coincidencia de patrones complejas, use la clase <xref:System.Text.RegularExpressions.Regex>.

## <a name="example"></a>Ejemplo

En el ejemplo siguiente se consulta una cadena para determinar el número de dígitos numéricos que contiene. Tenga en cuenta que la consulta se "reutiliza" después de que se ejecute la primera vez. Esto es posible porque la propia consulta no almacena ningún resultado real.

```vb
Class QueryAString

    Shared Sub Main()

        ' A string is an IEnumerable data source.
        Dim aString As String = "ABCDE99F-J74-12-89A"

        ' Select only those characters that are numbers
        Dim stringQuery = From ch In aString
                          Where Char.IsDigit(ch)
                          Select ch
        ' Execute the query
        For Each c As Char In stringQuery
            Console.Write(c & " ")
        Next

        ' Call the Count method on the existing query.
        Dim count As Integer = stringQuery.Count()
        Console.WriteLine(System.Environment.NewLine & "Count = " & count)

        ' Select all characters before the first '-'
        Dim stringQuery2 = aString.TakeWhile(Function(c) c <> "-")

        ' Execute the second query
        For Each ch In stringQuery2
            Console.Write(ch)
        Next

        Console.WriteLine(System.Environment.NewLine & "Press any key to exit")
        Console.ReadKey()
    End Sub
End Class
' Output:
' 9 9 7 4 1 2 8 9
' Count = 8
' ABCDE99F
```

## <a name="compiling-the-code"></a>Compilar el código

Cree un proyecto de aplicación de consola de VB.NET con una instrucción `Imports` para el espacio de nombres System. Linq.

## <a name="see-also"></a>Vea también

- [LINQ y cadenas (Visual Basic)](linq-and-strings.md)
- [Cómo combinar consultas LINQ con expresiones regulares (Visual Basic)](how-to-combine-linq-queries-with-regular-expressions.md)
