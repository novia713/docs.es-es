---
title: Glosario de aprendizaje automático
description: Un glosario de términos sobre aprendizaje automático.
author: jralexander
ms.author: johalex
ms.date: 05/31/2018
ms.topic: conceptual
ms.openlocfilehash: 6b175a8e89479dae81a7e5769e8d10c09a193898
ms.sourcegitcommit: 213292dfbb0c37d83f62709959ff55c50af5560d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/25/2018
ms.locfileid: "47081103"
---
# <a name="machine-learning-glossary"></a>Glosario de aprendizaje automático

La lista siguiente es una compilación de los términos importantes sobre aprendizaje automático que resultan de utilidad al crear los modelos personalizados.

## <a name="accuracy"></a>Exactitud

En [clasificación](#classification), la exactitud es el número de elementos correctamente clasificados dividido entre el número total de elementos en el conjunto de pruebas. Va desde 0 (el menos preciso) a 1 (el más preciso). La exactitud es una de las métricas de evaluación del rendimiento de su modelo. Trátela junto con el valor de [precisión](#precision), el de [recuperación](#recall) y la [puntuación F](#f-score).

API de ML.NET relacionada: <xref:Microsoft.ML.Models.BinaryClassificationMetrics.Accuracy?displayProperty=nameWithType>.

## <a name="area-under-the-curve-auc"></a>Área bajo la curva (AUC)

En [clasificación binaria](#binary-classification), una métrica de evaluación que es el valor del área bajo la curva que traza la tasa de verdaderos positivos (en el eje y) en relación con la tasa de falsos positivos (en el eje x). Va de 0,5 (el peor) a 1 (el mejor). También conocida como el área bajo la curva ROC; es decir, la curva característica operativa del receptor. Para obtener más información, consulte el artículo de Wikipedia [Curva ROC](https://en.wikipedia.org/wiki/Receiver_operating_characteristic).

API de ML.NET relacionada:<xref:Microsoft.ML.Models.BinaryClassificationMetrics.Auc?displayProperty=nameWithType>.

## <a name="binary-classification"></a>Clasificación binaria

Un caso de [clasificación](#classification) donde la [etiqueta](#label) es solo una de dos clases. Para obtener más información, vea la sección [Clasificación binaria](tasks.md#binary-classification) del tema [Tareas de aprendizaje automático](tasks.md).

## <a name="classification"></a>Clasificación

Cuando los datos se usan para predecir una categoría, la tarea de [aprendizaje automático supervisado](#supervised-machine-learning) se llama clasificación. La [clasificación binaria](#binary-classification) hace referencia a la predicción de únicamente dos categorías (por ejemplo, clasificar una imagen como la foto de un "gato" o un "perro"). La [clasificación multiclase ](#multiclass-classification) hace referencia a la predicción de varias categorías (por ejemplo, clasificar una imagen como la foto de una raza específica de perro).

## <a name="coefficient-of-determination"></a>Coeficiente de determinación

En [regresión](#regression), una métrica de evaluación que indica en qué grado los datos se ajustan a un modelo. Va de 0 a 1. Un valor de 0 significa que los datos son aleatorios o no pueden ajustarse al modelo. Un valor de 1 significa que el modelo coincide exactamente con los datos. Esto se conoce a menudo como r<sup>2</sup>, R<sup>2</sup>, o r cuadrado.

API de ML.NET relacionada: <xref:Microsoft.ML.Models.RegressionMetrics.RSquared?displayProperty=nameWithType>.

## <a name="feature"></a>Característica

Una propiedad medible del fenómeno que se mide, generalmente un valor numérico (doble). Las características múltiples se conocen como **vector de características** y generalmente se almacenan como `double[]`. Las características definen los elementos importantes del fenómeno que se mide. Para obtener más información, vea el artículo [Feature](https://en.wikipedia.org/wiki/Feature_(machine_learning)) (Característica) en Wikipedia.

## <a name="feature-engineering"></a>Ingeniería de características

La ingeniería de características es el proceso que implica la definición de un conjunto de [características](#feature) y el desarrollo de software que produce vectores de características a partir de los datos de fenómenos disponibles, es decir, la extracción de características. Para obtener más información, vea el artículo [Feature engineering](https://en.wikipedia.org/wiki/Feature_engineering) (Ingeniería de características) en Wikipedia.

## <a name="f-score"></a>Puntuación F

En [clasificación](#classification), una métrica de evaluación que equilibra [precisión](#precision) y [recuperación](#recall).

API de ML.NET relacionada: <xref:Microsoft.ML.Models.BinaryClassificationMetrics.F1Score?displayProperty=nameWithType>.

## <a name="hyperparameter"></a>Hiperparámetro

Un parámetro de un algoritmo de aprendizaje automático. Algunos ejemplos son el número de árboles para aprender en un bosque de decisión o el tamaño de paso en un algoritmo de gradiente descendente. Los valores de los *hiperparámetros* se establecen antes de entrenar el modelo y rigen el proceso de búsqueda de los parámetros de la función de predicción; por ejemplo, los puntos de comparación en un árbol de decisión o las ponderaciones en un modelo de regresión lineal. Para obtener más información, vea el artículo [Hyperparameter](https://en.wikipedia.org/wiki/Hyperparameter_(machine_learning)) (Hiperparámetro) en Wikipedia.

## <a name="label"></a>Etiqueta

El elemento que se va a predecir con el modelo de aprendizaje automático. Por ejemplo, una raza de perro o el precio futuro de unas acciones.

## <a name="log-loss"></a>Pérdida de registro

En [clasificación](#classification), una métrica de evaluación que caracteriza la precisión de un clasificador. Cuanto menor sea la pérdida de registro, más preciso será un clasificador.

API de ML.NET relacionada: <xref:Microsoft.ML.Models.BinaryClassificationMetrics.LogLoss?displayProperty=nameWithType>.

## <a name="mean-absolute-error-mae"></a>Error de media absoluto

En [regresión](#regression), una métrica de evaluación que es el promedio de todos los errores del modelo, donde el error del modelo es la distancia entre el valor de la [etiqueta](#label) predicho y el valor de la etiqueta correcto.

API de ML.NET relacionada: <xref:Microsoft.ML.Models.RegressionMetrics.L1?displayProperty=nameWithType>.

## <a name="model"></a>Modelo

Tradicionalmente, los parámetros de la función de predicción. Por ejemplo, las ponderaciones en un modelo de regresión lineal o los puntos de división en un árbol de decisión. En ML.NET, un modelo contiene toda la información necesaria para predecir la [etiqueta](#label) de un objeto de dominio (por ejemplo, imagen o texto). Esto significa que los modelos de ML.NET incluyen los pasos de caracterización necesarios, así como los parámetros para la función de predicción.

## <a name="multiclass-classification"></a>Clasificación multiclase

Un caso de [clasificación](#classification) donde la [etiqueta](#label) es una de tres o más clases. Para obtener más información, vea la sección [Clasificación multiclase](tasks.md#multiclass-classification) del tema [Tareas de aprendizaje automático](tasks.md).

## <a name="n-gram"></a>N-grama

Un esquema de extracción de características para datos de texto: cualquier secuencia de N palabras se convierte en un valor de [característica](#feature).

## <a name="numerical-feature-vector"></a>Vector de características numérico

Un vector de [características](#feature) que se compone únicamente de valores numéricos. Esto es similar a `double[]`.

## <a name="pipeline"></a>Canalización

Todas las operaciones necesarias para ajustar un modelo a un conjunto de datos. Una canalización consta de pasos de importación, transformación, caracterización y aprendizaje de datos. Una vez que una canalización está entrenada, se convierte en un modelo.

## <a name="precision"></a>Precisión

En [clasificación](#classification), la precisión de una clase es el número de elementos con una predicción correcta en cuando a pertenencia a esa clase dividido entre el número total de elementos cuya predicción señalaba la pertenencia a esa clase.

API de ML.NET relacionada:<xref:Microsoft.ML.Models.BinaryClassificationMetrics.NegativePrecision?displayProperty=nameWithType>, <xref:Microsoft.ML.Models.BinaryClassificationMetrics.PositivePrecision?displayProperty=nameWithType>.

## <a name="recall"></a>Recuperación

En [clasificación](#classification), la recuperación de una clase es el número de elementos con una predicción correcta en cuando a pertenencia a esa clase dividido entre el número total de elementos que efectivamente pertenecen a la clase.

API de ML.NET relacionada:<xref:Microsoft.ML.Models.BinaryClassificationMetrics.NegativeRecall?displayProperty=nameWithType>, <xref:Microsoft.ML.Models.BinaryClassificationMetrics.PositiveRecall?displayProperty=nameWithType>.

## <a name="regression"></a>Regresión

Una tarea de [aprendizaje automático supervisada](#supervised-machine-learning) donde el resultado es un valor real, por ejemplo, doble. Por ejemplo, la predicción de los precios de las acciones. Para obtener más información, vea la sección [Regresión](tasks.md#regression) del tema [Tareas de aprendizaje automático](tasks.md).

## <a name="relative-absolute-error"></a>Error absoluto relativo

En [regresión](#regression), una métrica de evaluación que es la suma de todos los errores absolutos dividida entre la suma de las distancias entre los valores de [etiqueta](#label) correctos y el promedio de todos los valores de etiqueta correctos.

## <a name="relative-squared-error"></a>Error cuadrático relativo

En [regresión](#regression), una métrica de evaluación que es la suma de todos los errores absolutos cuadráticos dividida entre la suma de las distancias cuadráticas existente entre los valores de [etiqueta](#label) correctos y el promedio de todos los valores de etiqueta correctos.

## <a name="root-of-mean-squared-error-rmse"></a>Raíz cuadrada del error cuadrático medio

En [regresión](#regression), una métrica de evaluación que es la raíz cuadrada del promedio de los cuadrados de los errores.

API de ML.NET relacionada: <xref:Microsoft.ML.Models.RegressionMetrics.Rms?displayProperty=nameWithType>.

## <a name="supervised-machine-learning"></a>Aprendizaje automático supervisado

Una subclase de aprendizaje automático en la que un modelo deseado predice la etiqueta de datos aún no vistos. Algunos ejemplos son la clasificación, la regresión y la predicción estructurada. Para obtener más información, vea el artículo [Aprendizaje supervisado](https://en.wikipedia.org/wiki/Supervised_learning) en Wikipedia.

## <a name="training"></a>Aprendizaje

El proceso de identificación de un [modelo](#model) para un conjunto de datos de entrenamiento determinado. Para un modelo lineal, esto significa buscar las ponderaciones. Para un árbol, implica la identificación de los puntos de división.

## <a name="transform"></a>Transformación

Un componente de [canalización](#pipeline) que transforma los datos. Por ejemplo, de texto a vector de números.

## <a name="unsupervised-machine-learning"></a>Aprendizaje automático no supervisado

Una subclase de aprendizaje automático en la que un modelo deseado encuentra una estructura oculta (o latente) en los datos. Algunos ejemplos son la agrupación en clústeres, el modelado de temas y la reducción de la dimensionalidad. Para obtener más información, vea el artículo [Aprendizaje no supervisado](https://en.wikipedia.org/wiki/Unsupervised_learning) en Wikipedia.
