---
title: ManualResetEvent y ManualResetEventSlim
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- threading [.NET Framework], ManualResetEvent class
- ManualResetEvent class, about ManualResetEvent class
ms.assetid: 465fdcf9-ba24-4d8d-a43f-d983b7cb0cc6
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 4949540b9f61e71301647a83a1c05d8b4c941412
ms.sourcegitcommit: ad99773e5e45068ce03b99518008397e1299e0d1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/23/2018
ms.locfileid: "46581277"
---
# <a name="manualresetevent-and-manualreseteventslim"></a>ManualResetEvent y ManualResetEventSlim
La clase <xref:System.Threading.ManualResetEvent?displayProperty=nameWithType> representa un evento de identificador de espera local que se debe restablecer manualmente después de que se le señale. Esta clase representa un caso especial de su clase base, <xref:System.Threading.EventWaitHandle?displayProperty=nameWithType>. Consulte la documentación conceptual [EventWaitHandle](../../../docs/standard/threading/eventwaithandle.md) para información sobre el uso las características de los eventos de restablecimiento manual.  
  
 Un objeto <xref:System.Threading.ManualResetEvent> permanece señalado hasta que se llama a su método <xref:System.Threading.EventWaitHandle.Reset%2A?displayProperty=nameWithType>. Se puede liberar cualquier número de subprocesos en espera, o subprocesos que esperan el evento una vez señalado, mientras se señala el estado del objeto.
  
 En [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)], puede usar la clase <xref:System.Threading.ManualResetEventSlim?displayProperty=nameWithType> para mejorar el rendimiento cuando se espera que los tiempos de espera sean breves y cuando el evento no cruza un límite de proceso. <xref:System.Threading.ManualResetEventSlim> usa giros de ocupado durante un breve tiempo mientras se espera que se señale el evento. Cuando los tiempos de espera son breves, los giros pueden ser mucho más económicos que si se espera con identificadores de espera. Sin embargo, si no se señala el evento dentro de cierto período de tiempo, <xref:System.Threading.ManualResetEventSlim> recurre a una espera de controlador de evento habitual.  
  
## <a name="see-also"></a>Vea también

- [Subprocesamiento](../../../docs/standard/threading/index.md)  
- [Objetos y características de subprocesos](../../../docs/standard/threading/threading-objects-and-features.md)  
- [Wait Handles](https://msdn.microsoft.com/library/48d10b6f-5fd7-407c-86ab-0179aef72489) (Clases WaitHandle)  
- [AutoResetEvent](../../../docs/standard/threading/autoresetevent.md)  
- [SpinWait](../../../docs/standard/threading/spinwait.md)  
- [Semaphore and SemaphoreSlim](../../../docs/standard/threading/semaphore-and-semaphoreslim.md) (Clases Semaphore y SemaphoreSlim)
