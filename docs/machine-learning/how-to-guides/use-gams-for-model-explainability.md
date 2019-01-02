---
title: Uso de modelos aditivos generalizados y funciones de forma para la explicación del modelo en ML.NET
description: Uso de modelos aditivos generalizados y funciones de forma para la explicación del modelo en ML.NET
ms.date: 12/04/2018
ms.custom: mvc,how-to
ms.openlocfilehash: 489aee34d0404293bc080b934636c01bdab92fe9
ms.sourcegitcommit: ccd8c36b0d74d99291d41aceb14cf98d74dc9d2b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/10/2018
ms.locfileid: "53156633"
---
# <a name="use-generalized-additive-models-and-shape-functions-for-model-explainability-in-mlnet"></a><span data-ttu-id="8261a-103">Uso de modelos aditivos generalizados y funciones de forma para la explicación del modelo en ML.NET</span><span class="sxs-lookup"><span data-stu-id="8261a-103">Use Generalized Additive Models and shape functions for model explainability in ML.NET</span></span>

<span data-ttu-id="8261a-104">Al crear modelos de Machine Learning, a menudo no es suficiente crear simplemente predicciones.</span><span class="sxs-lookup"><span data-stu-id="8261a-104">When creating machine learning models, it is often not enough to simply make predictions.</span></span> <span data-ttu-id="8261a-105">Con frecuencia, los desarrolladores del aprendizaje automático, las personas que toman decisiones y aquellas que se ven afectadas por los modelos deben comprender cómo los modelos de Machine Learning toman decisiones y las características que contribuyen a su rendimiento.</span><span class="sxs-lookup"><span data-stu-id="8261a-105">Often, machine learning developers, decision makers, and those affected by the models need to understand how machine learning models make decisions and which features contribute to their performance.</span></span> <span data-ttu-id="8261a-106">Los **modelos aditivos generalizados (GAM)** se usan internamente en Microsoft para la explicación del modelo con el fin de ayudar a los desarrolladores de aprendizaje automático a crear modelos de alta capacidad que puedan interpretar fácilmente otros usuarios.</span><span class="sxs-lookup"><span data-stu-id="8261a-106">**Generalized Additive Models (GAMs)** are used internally at Microsoft for model explainability to help machine learning developers create high-capacity models that can be easily interpreted by others.</span></span>

<span data-ttu-id="8261a-107">Los GAM son una clase de **modelos interpretables** que son modelos lineales donde los términos son funciones no lineales, denominadas "funciones de forma" de una sola variable.</span><span class="sxs-lookup"><span data-stu-id="8261a-107">GAMs are a class of **interpretable models** that are linear models where the terms are nonlinear functions, called "shape functions" of a single variable.</span></span> <span data-ttu-id="8261a-108">Al igual que los modelos lineales, se interpretan con facilidad, pero dado que los modelos aprenden funciones de características en lugar de una sola ponderación, pueden modelar relaciones más complejas que un modelo lineal simple.</span><span class="sxs-lookup"><span data-stu-id="8261a-108">As linear models, they are easily interpreted but because the models learn functions of features instead of a single weight, they can model more complex relationships than a simple linear model.</span></span> <span data-ttu-id="8261a-109">El indicador de GAM resultante tiene un término de interceptación que representa la predicción promedia con respecto al conjunto de aprendizaje, y las funciones de forma que representan la desviación de la predicción promedia.</span><span class="sxs-lookup"><span data-stu-id="8261a-109">The resulting GAM predictor has an intercept term that represents the average prediction over the training set, and shape functions that represent the deviation from the average prediction.</span></span> <span data-ttu-id="8261a-110">Las funciones de forma se pueden inspeccionar a ojo para ver la respuesta del modelo a valores distintos de una característica, y se visualizan como el siguiente gráfico creado al final del código de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="8261a-110">The shape functions can be inspected by eye to see the response of the model to different values of a feature, and visualized like the following graph that is created at the end of the code example.</span></span> <span data-ttu-id="8261a-111">El instructor de GAM en ML.NET se implementa mediante árboles impulsados por gradiente superficiales (por ejemplo, troncos) para aprender funciones de forma no paramétrica, y se basa en el método descrito en [Intelligible Models for Classification and Regression](https://www.cs.cornell.edu/~yinlou/papers/lou-kdd12.pdf) (Modelos inteligibles para clasificación y regresión) de Lou, Caruana y Gehrke.</span><span class="sxs-lookup"><span data-stu-id="8261a-111">The GAM trainer in ML.NET is implemented using shallow gradient boosted trees (for example tree stumps) to learn nonparametric shape functions, and is based on the method described in [Intelligible Models for Classification and Regression](https://www.cs.cornell.edu/~yinlou/papers/lou-kdd12.pdf) by Lou, Caruana, and Gehrke.</span></span>

```csharp
// Train the Generalized Additive Model
var gamTrainer = mlContext.Regression.Trainers.GeneralizedAdditiveModels()
var gamModel = gamTrainer.Fit(data);
 
// The intercept for Generalize Additive Models represent the average prediction for the training data
var intercept = gamModel.Intercept;
 
// Get the feature names from the training set
var featureNames = data.Schema.GetColumns()
                .Select(tuple => tuple.column.Name) // Get the column names
                .Where(name => name != labelName) // Drop the Label
                .ToArray();
 
// Get the index of a variable from the training data
var myFeatureIndex = featureNames.ToList().FindIndex(str => str.Equals("MyFeature"));
 
// The shape functions represent the deviation from the average prediction as a function of the feature value
// It is represented by a discrete set of bins
// First, get the array of bin upper bounds from the model for this feature
var myFeatureBins = gamModel.GetFeatureBinUpperBounds(myFeatureIndex);
// Then get the array of bin weights; these are the effect size for each bin
var myFeatureWeights = gamModel.GetFeatureWeights(myFeatureIndex);
 
// Write out the shape function for the feature (see the following figure for what this looks like)
for (int i = 0; i < myFeatureBins.Length; i++)
  Console.WriteLine($"x < {myFeatureBins[i]:0.00} => {myFeatureWeights[i]:0.000}");
```

![Gráfico de función de forma de modelos aditivos generalizados](./media/use-gams-for-model-explainability/gam-shape-function-graph.png)

<span data-ttu-id="8261a-113">Para ver un ejemplo de cómo entrenar un modelo de GAM e inspeccionar e interpretar los resultados, consulte el [repositorio de GitHub dotnet/machinelearning](https://github.com/dotnet/machinelearning/blob/master/docs/samples/Microsoft.ML.Samples/Dynamic/GeneralizedAdditiveModels.cs).</span><span class="sxs-lookup"><span data-stu-id="8261a-113">For a sample of how to train a GAM model and inspect and interpret the results, see [the dotnet/machinelearning GitHub repository](https://github.com/dotnet/machinelearning/blob/master/docs/samples/Microsoft.ML.Samples/Dynamic/GeneralizedAdditiveModels.cs).</span></span>