---
title: 'Procedimiento Copiar, eliminar y mover archivos y carpetas: Guía de programación de C#'
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- I/O [C#]
ms.assetid: 62e52cd7-9597-4e4a-acf9-1315f5cdbf05
ms.openlocfilehash: dd32798062dbfc9a10acd27ce51d8d5dd3b164f6
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/19/2019
ms.locfileid: "69590095"
---
# <a name="how-to-copy-delete-and-move-files-and-folders-c-programming-guide"></a>Procedimiento Copiar, eliminar y mover archivos y carpetas (Guía de programación de C#)
En los siguientes ejemplos se muestra cómo copiar, mover y eliminar archivos y carpetas de una manera sincrónica con las clases <xref:System.IO.File?displayProperty=nameWithType>, <xref:System.IO.Directory?displayProperty=nameWithType>, <xref:System.IO.FileInfo?displayProperty=nameWithType> y <xref:System.IO.DirectoryInfo?displayProperty=nameWithType> desde el espacio de nombres <xref:System.IO?displayProperty=nameWithType>. En estos ejemplos no se proporciona una barra de progreso ni ninguna otra interfaz de usuario. Si desea proporcionar un cuadro de diálogo de progreso estándar, consulte [Cómo: Proporcionar un cuadro de diálogo de progreso para operaciones de archivos](how-to-provide-a-progress-dialog-box-for-file-operations.md).  
  
 Use <xref:System.IO.FileSystemWatcher?displayProperty=nameWithType> para proporcionar eventos que le permitan calcular el progreso al realizar operaciones en varios archivos. Otro enfoque consiste en usar la invocación de plataforma para llamar a los métodos pertinentes relacionados con archivos en el shell de Windows. Para obtener información sobre cómo realizar estas operaciones de archivo de forma asincrónica, vea [E/S de archivos asincrónica](../../../standard/io/asynchronous-file-i-o.md).  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se muestra cómo copiar archivos y directorios.  
  
 [!code-csharp[csFilesandFolders#7](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csFilesAndFolders/CS/FileIteration.cs#7)]  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se muestra cómo mover archivos y directorios.  
  
 [!code-csharp[csFilesandFolders#8](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csFilesAndFolders/CS/FileIteration.cs#8)]  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se muestra cómo eliminar archivos y directorios.  
  
 [!code-csharp[csFilesandFolders#9](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csFilesAndFolders/CS/FileIteration.cs#9)]  
  
## <a name="see-also"></a>Vea también

- <xref:System.IO?displayProperty=nameWithType>
- [Guía de programación de C#](../index.md)
- [Registro y sistema de archivos (Guía de programación de C#)](index.md)
- [Cómo: Proporcionar un cuadro de diálogo de progreso para operaciones de archivos](how-to-provide-a-progress-dialog-box-for-file-operations.md)
- [E/S de archivos y secuencias](../../../standard/io/index.md)
- [Tareas de E/S comunes](../../../standard/io/common-i-o-tasks.md)
