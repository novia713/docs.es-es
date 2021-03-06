---
title: Modelos para la programación asincrónica
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- asynchronous design patterns, .NET Framework
- .NET Framework, asynchronous design patterns
ms.assetid: 4ece5c0b-f8fe-4114-9862-ac02cfe5a5d7
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: e399a512d2bee636aec35e008c0632ce9c5fa781
ms.sourcegitcommit: c7f3e2e9d6ead6cc3acd0d66b10a251d0c66e59d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/09/2018
ms.locfileid: "44249041"
---
# <a name="asynchronous-programming-patterns"></a>Modelos para la programación asincrónica

.NET Framework proporciona tres patrones para realizar las operaciones asincrónicas:  
  
- **Patrón de programación asincrónica (APM)** (también llamado patrón <xref:System.IAsyncResult>), en el que las operaciones asincrónicas requieren los métodos `Begin` y `End` (por ejemplo, `BeginWrite` y `EndWrite` para las operaciones asincrónicas de escritura). Este patrón ya no se recomienda para nuevo desarrollo. Para más información, consulte [Modelo de programación asincrónica (APM)](../../../docs/standard/asynchronous-programming-patterns/asynchronous-programming-model-apm.md).  
  
- **Patrón asincrónico basado en eventos (EAP)**, que requiere un método con el sufijo `Async`, así como uno o más eventos, tipos de delegado de controlador de eventos y tipos derivados de `EventArg`. EAP apareció por primera vez en .NET Framework 2.0. Ya no se recomienda para nuevo desarrollo. Para más información, consulte [Modelo asincrónico basado en eventos (EAP)](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-eap.md).  
  
- **Patrón asincrónico basado en tareas (TAP)**, que utiliza un método único para representar el inicio y la finalización de una operación asincrónica. TAP se introdujo en .NET Framework 4 y es el método recomendado para programación asincrónica en .NET Framework. Las palabras clave [async](~/docs/csharp/language-reference/keywords/async.md) y [await](~/docs/csharp/language-reference/keywords/await.md) en C# y los operadores [Async y](~/docs/visual-basic/language-reference/modifiers/async.md) [Await](~/docs/visual-basic/language-reference/operators/await-operator.md) en Visual Basic agregan compatibilidad de lenguaje para TAP. Para más información, consulte [Patrón asincrónico basado en tareas (TAP)](../../../docs/standard/asynchronous-programming-patterns/task-based-asynchronous-pattern-tap.md).  
  
## <a name="comparing-patterns"></a>Comparación de patrones  

Para una comparación rápida de cómo los tres patrones modelan las operaciones asincrónicas, considere un método `Read` que lea una determinada cantidad de datos en un búfer proporcionado comenzando en un desplazamiento especificado:  
  
```csharp  
public class MyClass  
{  
    public int Read(byte [] buffer, int offset, int count);  
}  
```  
  
El equivalente de APM para este método expondría los métodos `BeginRead` y `EndRead`:  
  
```csharp  
public class MyClass  
{  
    public IAsyncResult BeginRead(  
        byte [] buffer, int offset, int count,   
        AsyncCallback callback, object state);  
    public int EndRead(IAsyncResult asyncResult);  
}  
```  
  
El equivalente EAP expondría el siguiente conjunto de tipos y miembros:  
  
```csharp  
public class MyClass  
{  
    public void ReadAsync(byte [] buffer, int offset, int count);  
    public event ReadCompletedEventHandler ReadCompleted;  
}  
```  
  
El equivalente TAP expondría el siguiente método `ReadAsync` único:  
  
```csharp  
public class MyClass  
{  
    public Task<int> ReadAsync(byte [] buffer, int offset, int count);  
}  
```  
  
Para obtener información completa sobre TAP, APM y EAP, consulte los vínculos de la sección siguiente.  
  
## <a name="related-topics"></a>Temas relacionados

| Title | Descripción |
| ----- | ----------- |
| [Modelo para la programación asincrónica (APM)](../../../docs/standard/asynchronous-programming-patterns/asynchronous-programming-model-apm.md) | Describe el patrón heredado que utiliza la interfaz <xref:System.IAsyncResult> para proporcionar un comportamiento asincrónico. Este patrón ya no se recomienda para nuevo desarrollo. |
| [Modelo asincrónico basado en eventos (EAP)](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-eap.md) | Describe el patrón heredado basado en eventos para proporcionar el comportamiento asincrónico. Este patrón ya no se recomienda para nuevo desarrollo. |
| [Modelo asincrónico basado en tareas [TAP]](../../../docs/standard/asynchronous-programming-patterns/task-based-asynchronous-pattern-tap.md) | Describe el nuevo patrón asincrónico basado en el espacio de nombres <xref:System.Threading.Tasks>. Este patrón es el método recomendado para la programación asincrónica en .NET Framework 4 y versiones posteriores. |

## <a name="see-also"></a>Vea también

- [Programación asincrónica en C#](~/docs/csharp/async.md)   
- [Programación asincrónica en F#](~/docs/fsharp/tutorials/asynchronous-and-concurrent-programming/async.md)   
- [Programación asincrónica con Async y Await (Visual Basic)](~/docs/visual-basic/programming-guide/concepts/async/index.md)
