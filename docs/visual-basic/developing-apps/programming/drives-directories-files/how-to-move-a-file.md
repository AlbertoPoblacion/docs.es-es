---
title: Procedimiento para mover un archivo en Visual Basic
ms.date: 07/20/2015
helpviewer_keywords:
- files [Visual Basic], moving
ms.assetid: 53a7457b-5815-41ad-b37d-28537c1fb77a
ms.openlocfilehash: 0c909e3dfce1af17cc74ca526ba0409d5e9f93f8
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "58843726"
---
# <a name="how-to-move-a-file-in-visual-basic"></a>Procedimiento para mover un archivo en Visual Basic
El método `My.Computer.FileSystem.MoveFile` se puede usar para mover un archivo a otra carpeta. Si la estructura de destino no existe, se creará.  
  
### <a name="to-move-a-file"></a>Para mover un archivo  
  
-   Use el método `MoveFile` para mover el archivo, y especifique el nombre y la ubicación de los archivos de origen y de destino. En este ejemplo se mueve el archivo denominado `test.txt` de `TestDir1` a `TestDir2`. Observe que el nombre del archivo de destino se especifica aunque coincida con el nombre del archivo de origen.  
  
     [!code-vb[VbVbcnMyFileSystem#24](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMyFileSystem/VB/Class1.vb#24)]  
  
### <a name="to-move-a-file-and-rename-it"></a>Para mover un archivo y cambiarle el nombre  
  
-   Use el método `MoveFile` para mover el archivo, y especifique el nombre y la ubicación del archivo de origen, la ubicación de destino y el nuevo nombre en la ubicación de destino. En este ejemplo se mueve el archivo denominado `test.txt` de `TestDir1` a `TestDir2` y su nombre se cambia a `nexttest.txt`.  
  
     [!code-vb[VbVbcnMyFileSystem#25](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMyFileSystem/VB/Class1.vb#25)]  
  
## <a name="robust-programming"></a>Programación sólida  
 Las condiciones siguientes pueden provocar una excepción:  
  
-   La ruta de acceso no es válida por una de las siguientes razones: es una cadena de longitud cero, solo contiene un espacio en blanco, contiene caracteres no válidos o es una ruta de acceso de dispositivo (empieza por \\\\.\\) (<xref:System.ArgumentException>).  
  
-   La ruta de acceso no es válida porque es `Nothing` (<xref:System.ArgumentNullException>).  
  
-   `destinationFileName` es `Nothing` o una cadena vacía (<xref:System.ArgumentNullException>).  
  
-   El archivo de origen no es válido o no existe (<xref:System.IO.FileNotFoundException>).  
  
-   La ruta de acceso combinada apunta a un directorio existente, el archivo de destino existe y `overwrite` está establecido en `False`, un archivo del directorio de destino con el mismo nombre está en uso o el usuario no tiene permisos suficientes para acceder al archivo (<xref:System.IO.IOException>).  
  
-   Un nombre de archivo o de directorio de la ruta de acceso contiene un signo de dos puntos (:) o tiene un formato no válido (<xref:System.NotSupportedException>).  
  
-   `showUI` está establecido en `True`, `onUserCancel` está establecido en `ThrowException`y el usuario canceló la operación o se produjo un error de E/S no especificado (<xref:System.OperationCanceledException>).  
  
-   La ruta supera la longitud máxima definida por el sistema (<xref:System.IO.PathTooLongException>).  
  
-   El usuario no tiene los permisos necesarios para ver la ruta de acceso (<xref:System.Security.SecurityException>).  
  
-   El usuario no tiene el permiso necesario (<xref:System.UnauthorizedAccessException>).  
  
## <a name="see-also"></a>Vea también

- <xref:Microsoft.VisualBasic.FileIO.FileSystem.MoveFile%2A>
- [Cómo: Cambiar el nombre de un archivo](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-rename-a-file.md)
- [Cómo: Crear una copia de un archivo en otro directorio](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-create-a-copy-of-a-file-in-a-different-directory.md)
- [Cómo: Analizar rutas de acceso a archivos](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-parse-file-paths.md)
