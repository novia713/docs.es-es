---
title: Programación en paralelo en .NET
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- parallel programming
ms.assetid: 4d83c690-ad2d-489e-a2e0-b85b898a672d
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 372ffd7e17f60b8045cd5f89d52456c5f9655de1
ms.sourcegitcommit: 3c1c3ba79895335ff3737934e39372555ca7d6d0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2018
ms.locfileid: "43802308"
---
# <a name="parallel-programming-in-net"></a>Programación en paralelo en .NET

Muchos equipos y estaciones de trabajo tienen varios núcleos de CPU que permiten ejecutar varios subprocesos simultáneamente. Se espera que los equipos en un futuro cercano tengan significativamente más núcleos. Para aprovecharse del hardware de hoy y del mañana, puede paralelizar el código para distribuir el trabajo entre varios procesadores. En el pasado, la paralelización requería manipulación de bajo nivel de los subprocesos y bloqueos. Visual Studio 2010 y .NET Framework 4 mejoran la compatibilidad para la programación paralela proporcionando un nuevo tiempo de ejecución, nuevos tipos de biblioteca de clases y nuevas herramientas de diagnóstico. Estas características simplifican el desarrollo en paralelo, de modo que pueda escribir código paralelo eficaz, específico y escalable de forma natural sin tener que trabajar directamente con subprocesos ni el bloque de subprocesos. La siguiente ilustración proporciona una información general de alto nivel de la arquitectura de programación paralela en .NET Framework 4.

 ![Arquitectura de programación en paralelo de .NET](./media/tpl-architecture.png "TPL_Architecture")

## <a name="related-topics"></a>Temas relacionados

|Tecnología|Descripción|
|----------------|-----------------|
|[Biblioteca TPL](../../../docs/standard/parallel-programming/task-parallel-library-tpl.md)|Proporciona documentación para la clase <xref:System.Threading.Tasks.Parallel?displayProperty=nameWithType>, que incluye versiones paralelas de `For` y bucles `ForEach`, y también para la clase <xref:System.Threading.Tasks.Task?displayProperty=nameWithType>, que representa la manera preferida de expresar las operaciones asincrónicas.|
|[Parallel LINQ (PLINQ)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)|Una implementación paralela de LINQ to Objects que significativamente mejora el rendimiento en muchos casos.|
|[Estructuras de datos para la programación paralela](../../../docs/standard/parallel-programming/data-structures-for-parallel-programming.md)|Proporciona vínculos a documentación sobre las clases de colección seguras para subprocesos, tipos de sincronización ligeros y tipos para la inicialización diferida.|
|[Herramientas de diagnóstico paralelo](../../../docs/standard/parallel-programming/parallel-diagnostic-tools.md)|Proporciona vínculos a documentación sobre las ventanas del depurador de Visual Studio para las tareas y pilas paralelas y para el [visualizador de simultaneidad](/visualstudio/profiling/concurrency-visualizer).|
|[Particionadores personalizados para PLINQ y TPL](../../../docs/standard/parallel-programming/custom-partitioners-for-plinq-and-tpl.md)|Describe cómo funcionan los particionadores y cómo configurar particionadores predeterminados o crear nuevos.|
|[Programadores de tareas](https://msdn.microsoft.com/library/638f8ea5-21db-47a2-a934-86e1e961bf65)|Describe cómo funcionan los programadores y cómo se pueden configurar los programadores predeterminados.|
|[Expresiones lambda en PLINQ y TPL](../../../docs/standard/parallel-programming/lambda-expressions-in-plinq-and-tpl.md)|Proporciona información general sobre expresiones lambda en C# y Visual Basic, y presenta cómo se utilizan en PLINQ y Task Parallel Library.|
|[Información adicional](../../../docs/standard/parallel-programming/for-further-reading-parallel-programming.md)|Proporciona vínculos a información adicional y recursos de ejemplo para programación paralela en .NET.|

## <a name="see-also"></a>Vea también

- [Información general de Async](../async.md)
- [Subprocesamiento administrado](../threading/index.md)
