---
title: Explicación de las predicciones del modelo mediante la importancia de características de permutación
description: Descripción de la importancia de características de modelos con importancia de característica de permutación en ML.NET
ms.date: 05/02/2019
author: luisquintanilla
ms.author: luquinta
ms.custom: mvc,how-to
ms.openlocfilehash: 2f444508990a902a1c61b72b1be2263d8d93ba70
ms.sourcegitcommit: ca2ca60e6f5ea327f164be7ce26d9599e0f85fe4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/06/2019
ms.locfileid: "65065648"
---
# <a name="explain-model-predictions-using-permutation-feature-importance"></a>Explicación de las predicciones del modelo mediante la importancia de características de permutación

Obtenga información sobre cómo explicar predicciones del modelo de Machine Learning de ML.NET al comprender que las características de contribución deben realizar predicciones mediante la importancia de características de permutación (PFI).

A menudo se piensa en los modelos de Machine Learning como cajas negras que toman entradas y generan salidas. Rara vez se entienden los pasos intermedios o las interacciones entre las características que afectan a la salida. A medida que el aprendizaje automático se introduce en otros aspectos de la vida diaria como la asistencia sanitaria, es de vital importancia comprender por qué un modelo de Machine Learning toma esas decisiones. Por ejemplo, si un modelo de Machine Learning realiza diagnósticos, los profesionales sanitarios necesitan una forma de buscar en los factores que se incluyeron en la realización de dicho diagnóstico. Proporcionar el diagnóstico correcto puede marcar una gran diferencia en el hecho de que un paciente tenga una recuperación rápida o no. Por lo tanto, cuanto mayor sea el nivel de explicación en un modelo, mayor será la confianza que tengan los profesionales sanitarios para aceptar o rechazar las decisiones tomadas por el modelo.

Se utilizan diversas técnicas para explicar modelos, una de los cuales es PFI. PFI es una técnica utilizada para explicar los modelos de clasificación y regresión que se inspira en el artículo [Random Forests*de* Breiman](https://www.stat.berkeley.edu/~breiman/randomforest2001.pdf) (consulte la sección 10). En un nivel alto, esto funciona de manera es revolviendo los datos de manera aleatoria en una característica a la vez para todo el conjunto de datos y calculando cuánto se reduce la métrica de rendimiento de interés. Cuanto mayor sea el cambio, más importante será esa característica. 

Además, al resaltar las características más importantes, los compiladores del modelo pueden centrarse en el uso de un subconjunto de características más significativas que potencialmente pueden reducir el ruido y el tiempo de entrenamiento.

## <a name="load-the-data"></a>Carga de los datos

Las características del conjunto de datos que se usa para este ejemplo están en las columnas 1 a 12. El objetivo es predecir `Price`. 

| Columna | Característica | Descripción 
| --- | --- | --- |
| 1 | CrimeRate | Tasa de criminalidad per cápita
| 2 | ResidentialZones | Zonas residenciales en la ciudad
| 3 | CommercialZones | Zonas no residenciales en la ciudad
| 4 | NearWater | Proximidad a un cuerpo de agua
| 5 | ToxicWasteLevels | Niveles de toxicidad (PPM)
| 6 | AverageRoomNumber | Número promedio de salas en casa
| 7 | HomeAge | Antigüedad de la casa
| 8 | BusinessCenterDistance | Distancia al distrito comercial más cercano
| 9 | HighwayAccess | Proximidad a las autopistas
| 10 | TaxRate | Tasa de impuestos sobre la propiedad
| 11 | StudentTeacherRatio | Proporción de alumnos por profesores
| 12 | PercentPopulationBelowPoverty | Porcentaje de la población que vive por debajo de pobreza
| 13 | Price | Precio de la vivienda

A continuación, se muestra un ejemplo del conjunto de datos:

```text
1,24,13,1,0.59,3,96,11,23,608,14,13,32
4,80,18,1,0.37,5,14,7,4,346,19,13,41
2,98,16,1,0.25,10,5,1,8,689,13,36,12
```

Los datos en este ejemplo se pueden modelar mediante una clase como `HousingPriceData`:

```csharp
class HousingPriceData
{
    [LoadColumn(0)]
    public float CrimeRate { get; set; }

    [LoadColumn(1)]
    public float ResidentialZones { get; set; }

    [LoadColumn(2)]
    public float CommercialZones { get; set; }

    [LoadColumn(3)]
    public float NearWater { get; set; }

    [LoadColumn(4)]
    public float ToxicWasteLevels { get; set; }

    [LoadColumn(5)]
    public float AverageRoomNumber { get; set; }

    [LoadColumn(6)]
    public float HomeAge { get; set; }

    [LoadColumn(7)]
    public float BusinessCenterDistance { get; set; }

    [LoadColumn(8)]
    public float HighwayAccess { get; set; }

    [LoadColumn(9)]
    public float TaxRate { get; set; }

    [LoadColumn(10)]
    public float StudentTeacherRatio { get; set; }

    [LoadColumn(11)]
    public float PercentPopulationBelowPoverty { get; set; }

    [LoadColumn(12)]
    [ColumnName("Label")]
    public float Price { get; set; }
}
```

Cargue los datos en un [`IDataView`](xref:Microsoft.ML.IDataView).

## <a name="train-the-model"></a>Entrenar el modelo

El ejemplo de código siguiente ilustra el proceso de entrenamiento de un modelo de regresión lineal para predecir los precios de la vivienda.

```csharp
// 1. Get the column name of input features.
string[] featureColumnNames = 
    data.Schema
        .Select(column => column.Name)
        .Where(columnName => columnName != "Label").ToArray();

// 2. Define estimator with data pre-processing steps
IEstimator<ITransformer> dataPrepEstimator =
    mlContext.Transforms.Concatenate("Features", featureColumnNames)
        .Append(mlContext.Transforms.NormalizeMinMax("Features"));

// 3. Create transformer using the data pre-processing estimator
ITransformer dataPrepTransformer = dataPrepEstimator.Fit(data);

// 4. Pre-process the training data
IDataView preprocessedTrainData = dataPrepTransformer.Transform(data);

// 5. Define Stochastic Dual Coordinate Ascent machine learning estimator
var sdcaEstimator = mlContext.Regression.Trainers.Sdca();

// 6. Train machine learning model
var sdcaModel = sdcaEstimator.Fit(preprocessedTrainData);
```

## <a name="explain-the-model-with-permutation-feature-importance-pfi"></a>Explicar el modelo con la importancia de características de permutación (PFI)

En ML.NET, use el método [`PermutationFeatureImportance`](xref:Microsoft.ML.PermutationFeatureImportanceExtensions) para la tarea correspondiente.

```csharp
ImmutableArray<RegressionMetricsStatistics> permutationFeatureImportance = 
    mlContext
        .Regression
        .PermutationFeatureImportance(sdcaModel, preprocessedTrainData, permutationCount:3);
```

El resultado del uso de [`PermutationFeatureImportance`](xref:Microsoft.ML.PermutationFeatureImportanceExtensions) en el conjunto de datos de entrenamiento es un [`ImmutableArray`](xref:System.Collections.Immutable.ImmutableArray) de objetos [`RegressionMetricsStatistics`](xref:Microsoft.ML.Data.RegressionMetricsStatistics). [`RegressionMetricsStatistics`](xref:Microsoft.ML.Data.RegressionMetricsStatistics) proporciona estadísticas de resumen, como desviación media y estándar para diversas observaciones de [`RegressionMetrics`](xref:Microsoft.ML.Data.RegressionMetrics) equivalentes al número de permutaciones especificadas por el parámetro `permutationCount`.

La importancia o, en este caso, la disminución de la media absoluta de la métrica de R cuadrado calculada con [`PermutationFeatureImportance`](xref:Microsoft.ML.PermutationFeatureImportanceExtensions), se puede ordenar de las más importante a la menos importante.  

```csharp
// Order features by importance
var featureImportanceMetrics =
    permutationFeatureImportance
        .Select((metric, index) => new { index, metric.RSquared })
        .OrderByDescending(myFeatures => Math.Abs(myFeatures.RSquared.Mean));

Console.WriteLine("Feature\tPFI");

foreach (var feature in featureImportanceMetrics)
{
    Console.WriteLine($"{featureColumnNames[feature.index],-20}|\t{feature.RSquared.Mean:F6}");
}
```

Imprimir los valores para cada una de las características de `featureImportanceMetrics` generaría resultados similares a los siguientes. Tenga en cuenta que debe esperar para ver resultados diferentes porque estos valores varían en función de los datos que se proporcionan.  

| Característica | Cambiar a R cuadrado |
|:--|:--:|
HighwayAccess       |   -0,042731
StudentTeacherRatio |   -0,012730
BusinessCenterDistance| -0,010491
TaxRate             |   -0,008545
AverageRoomNumber   |   -0,003949
CrimeRate           |   -0,003665
CommercialZones     |   0,002749
HomeAge             |   -0,002426
ResidentialZones    |   -0,002319
NearWater           |   0,000203
PercentPopulationLivingBelowPoverty|    0,000031
ToxicWasteLevels    |   -0,000019

Al echar un vistazo a las cinco características más importantes de este conjunto de datos, el precio de una casa previsto por este modelo viene determinado por su proximidad a las autopistas, la proporción de alumnos por profesores en la zona, la proximidad a los principales centros de empleo, tasa de impuestos sobre la propiedad y el número promedio de dormitorios en una casa.
