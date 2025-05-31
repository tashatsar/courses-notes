# Machine-learning-with-apache-spark✨

## Getting started 

**Importing Libraries**
```py
# FindSpark simplifies the process of using Apache Spark with Python

import findspark
findspark.init()

# import SparkSession
from pyspark.sql import SparkSession
```

Notes:
- SparkContext — это "старый способ" начать работу со Spark, позволяет подключиться к кластеру и управлять вычислениями, но сам по себе не включает работу с DataFrame и SQL.
- SparkSession — это "новый и универсальный способ", появившийся начиная с Spark 2.0, объединяет в себе SparkContext, SQLContext и HiveContext. То есть может работать с RDD (как SparkContext), может работать с DataFrame, SQL, Hive, Parquet и т.п.
- findspark нужен, если переменные окружения SPARK_HOME и PYTHONPATH не настроены. Например, при работе в Jupyter Notebook локально, когда PySpark не находится автоматически. Не нужен в настроенной среде (например, Databricks, EMR, Docker, или внутри PySpark-кластера) или используется PySpark из pip (pip install pyspark).


```py
# create spark session
spark = SparkSession.builder.appName("Diamond data analysis").getOrCreate()

# load data
# !wget https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-BD0231EN-SkillsNetwork/datasets/diamonds.csv

# data to a df
diamond_data = spark.read.csv("diamonds.csv", header=True, inferSchema=True)

# explore data
diamond_data.printSchema()
diamond_data.head(5)
diamond_data.show(5)

# stop the spark session
spark.stop()
```

## Regression


| Built-in Model                            |`pyspark.ml.regression` | 
| -------------------------------- | ------------------------------- | 
| 💡 Linear Regression             | `LinearRegression`              | 
| 🌲 Decision Tree Regressor       | `DecisionTreeRegressor`         | 
| 🌳 Random Forest Regressor       | `RandomForestRegressor`         | 
| 🎯 GBT Regressor (Boosting)      | `GBTRegressor`                  | 
| 🤖 AFT Survival Regression       | `AFTSurvivalRegression`         | 
| 🧮 Generalized Linear Regression | `GeneralizedLinearRegression`   |

Notes:
- Spark ML требует, чтобы все входные признаки были в одном столбце типа Vector, а не в нескольких числовых колонках

| 📏 Metric       | `.setMetricName()` value | Description                                                                     |
| --------------- | ------------------------ | ------------------------------------------------------------------------------- |
| 🧮 **RMSE**     | `"rmse"`                 | Root Mean Squared Error – penalizes large errors more heavily.                  |
| ➕ **MSE**       | `"mse"`                  | Mean Squared Error – average squared difference between predicted and actual.   |
| ➖ **MAE**       | `"mae"`                  | Mean Absolute Error – average absolute difference between predicted and actual. |
| 📈 **R² Score** | `"r2"`                   | Coefficient of Determination – proportion of variance explained by the model.   |


### Linear regression

Let's use `diamond_data` from the previous section:

```py

from pyspark.ml.feature import VectorAssembler
from pyspark.ml.regression import LinearRegression, GBTRegressor
from pyspark.ml.evaluation import RegressionEvaluator

# Prepare feature vector
assembler = VectorAssembler(inputCols=["carat", "depth", "table"], outputCol="features")
diamond_transformed_data = assembler.transform(diamond_data)

# Print the vectorized features and label columns
diamond_transformed_data.select("features","price").show()

# Train-test split
(training_data, testing_data) = diamond_transformed_data.randomSplit([0.7, 0.3], seed=42)

# Train LR model
lr = LinearRegression(featuresCol="features", labelCol="price")
model = lr.fit(training_data)

# Make prediction
predictions = model.transform(testing_data)

# Print metrics
metrics = {}
for metric in ['r2', 'mae', 'rmse']:
    evaluator = RegressionEvaluator(labelCol="price", predictionCol="prediction", metricName=metric)
    metrics[metric] = evaluator.evaluate(predictions)
print(metrics)

```

### GBT
```oy
from pyspark.ml.regression import GBTRegressor

gbt = GBTRegressor(featuresCol="features", labelCol="price")
model = gbt.fit(training_data)
predictions = model.transform(testing_data)

metrics = {}
for metric in ['r2', 'mae', 'rmse']:
    evaluator = RegressionEvaluator(labelCol="price", predictionCol="prediction", metricName=metric)
    metrics[metric] = evaluator.evaluate(predictions)
print(metrics)

```


### LightGBM

*Works in theory

```py
!pip install synapseml

from pyspark.sql import SparkSession

from pyspark.ml.feature import VectorAssembler
from pyspark.ml.evaluation import RegressionEvaluator

from synapse.ml.lightgbm import LightGBMRegressor

spark = SparkSession.builder \
    .appName("LightGBM with SynapseML") \
    .config("spark.jars.packages", "com.microsoft.azure:synapseml_2.12:0.11.2") \
    .getOrCreate()

# MOAR RESOURCES, MOAAAR
#spark = SparkSession.builder \
#    .appName("SynapseML Example") \
#    .config("spark.jars.packages", "com.microsoft.azure:synapseml_2.12:0.11.2") \
#    .config("spark.executor.memory", "2g") \
#    .config("spark.driver.memory", "2g") \
#    .getOrCreate()

!wget https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-BD0231EN-SkillsNetwork/datasets/diamonds.csv
diamond_data = spark.read.csv("diamonds.csv", header=True, inferSchema=True)

assembler = VectorAssembler(inputCols=["carat", "depth", "table"], outputCol="features")
diamond_transformed_data = assembler.transform(diamond_data)
(training_data, testing_data) = diamond_transformed_data.randomSplit([0.7, 0.3], seed=42)

lgbm = LightGBMRegressor(
    featuresCol="features",
    labelCol="price",
    # numIterations=100, learningRate=0.1, numLeaves=31
)

model = lgbm.fit(train_data)
predictions = model.transform(testing_data)
metrics = {}
for metric in ['r2', 'mae', 'rmse']:
    evaluator = RegressionEvaluator(labelCol="price", predictionCol="prediction", metricName=metric)
    metrics[metric] = evaluator.evaluate(predictions)
print(metrics)
```

## Classification

| Model                      | `pyspark.ml.classification`              | Task Type          | Notes                                            |
| ----------------------------- | -------------------------------- | --------------------- | --------------------------------------------------- |
| 📈 Logistic Regression   | `LogisticRegression`             | Binary / Multiclass   | Supports regularization, baseline model             |
| ⚖️ Linear SVM             | `LinearSVC`                      | Binary only           | No probability outputs, fast and scalable           |
| 📊 Naive Bayes            | `NaiveBayes`                     | Binary / Multiclass   | Good for categorical/text data                      |
| 🌳 Decision Tree          | `DecisionTreeClassifier`         | Binary / Multiclass   | Interpretable, prone to overfitting                 |
| 🌲 Random Forest          | `RandomForestClassifier`         | Binary / Multiclass   | Robust, good default ensemble                       |
| 🔥 Gradient-Boosted Trees | `GBTClassifier`                  | Binary only           | Powerful, but no multiclass support                 |
| 🧩 One-vs-Rest            | `OneVsRest`                      | Multiclass via binary | Wraps binary classifiers for multiclass             |
| 🧠 Multilayer Perceptron  | `MultilayerPerceptronClassifier` | Binary / Multiclass   | Simple feedforward neural net                       |
| 🧮 Factorization Machines | `FMClassifier`                   | Binary only           | Great for sparse feature data (e.g. CTR prediction) |

### MulticlassClassificationEvaluator

| Metric        | `.setMetricName()` value | Description                                            |
| ---------------- | ------------------------ | ------------------------------------------------------ |
| 🧮 **Accuracy**  | `"accuracy"`             | Proportion of correct predictions (macro average).     |
| 📐 **F1 Score**  | `"f1"`                   | Harmonic mean of precision and recall (macro average). |
| 🎯 **Precision** | `"weightedPrecision"`    | Precision weighted by class frequencies.               |
| 🎯 **Recall**    | `"weightedRecall"`       | Recall weighted by class frequencies.                  |

## Metrics 

| 📦 Evaluator Class                     | 🧠 Task Type                 | 📏 Supported Metrics (`.setMetricName()`)                       | 🔎 Description                                                          |
| -------------------------------------- | ---------------------------- | --------------------------------------------------------------- | ----------------------------------------------------------------------- |
| 🧮 `MulticlassClassificationEvaluator` | Classification (multi-class) | `"accuracy"`, `"f1"`, `"weightedPrecision"`, `"weightedRecall"` | Evaluates multi-class classification models.                            |
| ✅ `BinaryClassificationEvaluator`      | Classification (binary)      | `"areaUnderROC"`, `"areaUnderPR"`                               | Evaluates binary classifiers based on ROC or PR curves.                 |
| 📉 `RegressionEvaluator`               | Regression                   | `"rmse"`, `"mse"`, `"mae"`, `"r2"`                              | Evaluates regression models.                                            |
| 📊 `ClusteringEvaluator`               | Clustering                   | `"silhouette"`                                                  | Measures clustering quality using silhouette score (based on distance). |

