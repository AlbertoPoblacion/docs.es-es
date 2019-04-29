---
title: Objetos BFILE de Oracle
ms.date: 03/30/2017
ms.assetid: 341bbf84-4734-4d44-8723-ccedee954e21
ms.openlocfilehash: 5bb9f7e67016cf4b1d467935fe302ab4a40edbfa
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61771974"
---
# <a name="oracle-bfiles"></a>Objetos BFILE de Oracle
El proveedor de datos .NET Framework para Oracle incluye la clase <xref:System.Data.OracleClient.OracleBFile>, que se utiliza para trabajar con el tipo de datos <xref:System.Data.OracleClient.OracleType.BFile> de Oracle.  
  
 Oracle **BFILE** es de tipo de datos Oracle **LOB** tipo de datos que contiene una referencia a datos binarios con un tamaño máximo de 4 gigabytes. Oracle **BFILE** difiere de otro Oracle **LOB** tipos de datos en que sus datos se almacenan en un archivo físico en el sistema operativo en lugar de en el servidor. Tenga en cuenta que el **BFILE** tipo de datos proporciona acceso de solo lectura a los datos.  
  
 Otras características de un **BFILE** tipo de datos que lo distinguen de un **LOB** son que el tipo de datos:  
  
- contiene datos no estructurados.  
  
- admite el troceo en el servidor.  
  
- utiliza semántica de copia de referencia. Por ejemplo, si realiza una operación de copia en un **BFILE**, solo el **BFILE** se copia el localizador (que es una referencia al archivo). Los datos del archivo no se copian.  
  
 El **BFILE** se debe usar el tipo de datos para hacer referencia a los LOB que son de gran tamaño y por lo tanto, no es práctico almacenar en la base de datos. Más sobrecarga de comunicación, el servidor y el cliente está implicada cuando se usa un **BFILE** tipo de datos en comparación con el **LOB** tipo de datos. Resulta más eficaz para tener acceso a un **BFILE** si sólo necesita obtener una pequeña cantidad de datos. En cambio, si necesita obtener el objeto entero, es más eficiente tener acceso a los LOB residentes en la base de datos.  
  
 Cada distinto de NULL **OracleBFile** objeto está asociado con dos entidades que definen la ubicación del archivo físico subyacente:  
  
1. Un objeto DIRECTORY de Oracle, que es un alias de base de datos de un directorio del sistema de archivos, y  
  
2. el nombre de archivo del archivo físico subyacente, que se encuentra en el directorio asociado con el objeto DIRECTORY.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo de C# siguiente se muestra cómo puede crear un **BFILE** en Oracle, tabla y, a continuación, recuperarlo en forma de un **OracleBFile** objeto. En el ejemplo se muestra cómo utilizar el <xref:System.Data.OracleClient.OracleDataReader> objeto y el **OracleBFile** **Seek** y **lectura** métodos. Tenga en cuenta que para usar este ejemplo, primero debe crear un directorio denominado "c:\\\bfiles" y el archivo llamado "MyFile.jpg" en el servidor de Oracle.  
  
```csharp  
using System;  
using System.IO;  
using System.Data;  
using System.Data.OracleClient;  
  
public class Sample  
{  
   public static void Main(string[] args)  
   {  
      OracleConnection connection = new OracleConnection(  
        "Data Source=Oracle8i;Integrated Security=yes");  
      connection.Open();  
  
      OracleCommand command = connection.CreateCommand();  
      command.CommandText =   
        "CREATE or REPLACE DIRECTORY MyDir as 'c:\\bfiles'";  
      command.ExecuteNonQuery();  
      command.CommandText =   
        "DROP TABLE MyBFileTable";  
      try {  
        command.ExecuteNonQuery();  
      }  
      catch {  
      }  
      command.CommandText =   
        "CREATE TABLE MyBFileTable(col1 number, col2 BFILE)";  
      command.ExecuteNonQuery();  
      command.CommandText =   
        "INSERT INTO MyBFileTable values ('2', BFILENAME('MyDir', " +  
        "'MyFile.jpg'))";  
      command.ExecuteNonQuery();  
      command.CommandText = "SELECT * FROM MyBFileTable";  
  
        byte[] buffer = new byte[100];  
  
      OracleDataReader reader = command.ExecuteReader();  
      using (reader) {  
          if (reader.Read()) {  
                OracleBFile bFile = reader.GetOracleBFile(1);  
                using (bFile) {  
                  bFile.Seek(0, SeekOrigin.Begin);  
                  bFile.Read(buffer, 0, 100);  
              }  
          }  
      }  
  
      connection.Close();  
   }  
  
}  
```  
  
## <a name="see-also"></a>Vea también

- [Oracle y ADO.NET](../../../../docs/framework/data/adonet/oracle-and-adonet.md)
- [Proveedores administrados de ADO.NET y Centro para desarrolladores de DataSet](https://go.microsoft.com/fwlink/?LinkId=217917)
