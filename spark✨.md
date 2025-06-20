# Machine-learning-with-apache-spark✨

- [Machine-learning-with-apache-spark✨](#machine-learning-with-apache-spark)
  - [Getting started](#getting-started)
  - [Dataframes](#dataframes)
  - [Regression](#regression)
    - [Linear regression](#linear-regression)
    - [GBT](#gbt)
    - [LightGBM](#lightgbm)
    - [RegressionEvaluator](#regressionevaluator)
  - [Classification](#classification)
    - [Classification models](#classification-models)
    - [MulticlassClassificationEvaluator](#multiclassclassificationevaluator)
  - [Metrics](#metrics)
  - [Unsupervised learning](#unsupervised-learning)
  - [Modeling: Pipelines and Saving Models](#modeling-pipelines-and-saving-models)
    - [Prepare](#prepare)
    - [Create the model](#create-the-model)
    - [Save the model](#save-the-model)
    - [Load the model](#load-the-model)
    - [Predict](#predict)

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

## Dataframes
```py

# Create a spark session
spark = SparkSession.builder.appName("Model Persistence").getOrCreate()
# Download the data set
!wget https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-BD0231EN-SkillsNetwork/datasets/diamonds.csv
# Load the dataset into a spark dataframe
diamond_data = spark.read.csv("diamonds.csv", header=True, inferSchema=True)

# Display sample data from dataset
diamond_data.show(5)

# Print the schema of the dataset
diamond_data.printSchema()

# Print the number of rows in the dataframe
df.count()

# Drop Duplicates
df = df.dropDuplicates()

# Drop Null values
df=df.dropna()

# Write the data to a Parquet fileSSSSS
df.write.mode("overwrite").parquet("student-hw.parquet")

# Reduce the number of partitions in the dataframe to one - and then save to a parquet
df = df.repartition(1)

# Read parquet
df = spark.read.parquet("student-hw-single.parquet")
```
Notes: To improve parallellism, spark stores each dataframe in multiple partitions.
When the data is saved as parquet file, each partition is saved as a separate file!!!

For data transformations and descriptive staristics:

```py
#import the expr function that helps in transforming the data
from pyspark.sql.functions import expr

# Convert pounds to kilograms
# Multiply weight_pounds with 0.453592 to get a new column weight_kg
df = df.withColumn("weight_kg", expr("weight_pounds * 0.453592"))

from pyspark.sql import functions as F
diamond_data.groupBy("cut").avg("price").show()
diamond_data.groupBy("color").agg(F.max("price").alias("max_price"), F.min("price").alias("min_price")).show()
diamond_data.stat.corr("carat", "price") 
diamond_data.describe(["carat", "depth", "table", "price"]).show()
diamond_data.stat.crosstab("cut", "clarity").show()
diamond_data.withColumn("carat_group", F.floor(diamond_data["carat"] / 0.2)) \
    .groupBy("carat_group") \
    .avg("price") \
    .orderBy("carat_group") \
    .show()
```


## Regression


| Built-in Model                  | `pyspark.ml.regression`       |
| ------------------------------- | ----------------------------- |
| 💡 Linear Regression             | `LinearRegression`            |
| 🌲 Decision Tree Regressor       | `DecisionTreeRegressor`       |
| 🌳 Random Forest Regressor       | `RandomForestRegressor`       |
| 🎯 GBT Regressor (Boosting)      | `GBTRegressor`                |
| 🤖 AFT Survival Regression       | `AFTSurvivalRegression`       |
| 🧮 Generalized Linear Regression | `GeneralizedLinearRegression` |

Notes:
- Spark ML требует, чтобы все входные признаки были в одном столбце типа Vector, а не в нескольких числовых колонках

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

### RegressionEvaluator

| 📏 Metric       | `.setMetricName()` value | Description                                                                     |
| -------------- | ------------------------ | ------------------------------------------------------------------------------- |
| 🧮 **RMSE**     | `"rmse"`                 | Root Mean Squared Error – penalizes large errors more heavily.                  |
| ➕ **MSE**      | `"mse"`                  | Mean Squared Error – average squared difference between predicted and actual.   |
| ➖ **MAE**      | `"mae"`                  | Mean Absolute Error – average absolute difference between predicted and actual. |
| 📈 **R² Score** | `"r2"`                   | Coefficient of Determination – proportion of variance explained by the model.   |


## Classification

### Classification models

| Model                    | `pyspark.ml.classification`      | Task Type             | Notes                                               |
| ------------------------ | -------------------------------- | --------------------- | --------------------------------------------------- |
| 📈 Logistic Regression    | `LogisticRegression`             | Binary / Multiclass   | Supports regularization, baseline model             |
| ⚖️ Linear SVM             | `LinearSVC`                      | Binary only           | No probability outputs, fast and scalable           |
| 📊 Naive Bayes            | `NaiveBayes`                     | Binary / Multiclass   | Good for categorical/text data                      |
| 🌳 Decision Tree          | `DecisionTreeClassifier`         | Binary / Multiclass   | Interpretable, prone to overfitting                 |
| 🌲 Random Forest          | `RandomForestClassifier`         | Binary / Multiclass   | Robust, good default ensemble                       |
| 🔥 Gradient-Boosted Trees | `GBTClassifier`                  | Binary only           | Powerful, but no multiclass support                 |
| 🧩 One-vs-Rest            | `OneVsRest`                      | Multiclass via binary | Wraps binary classifiers for multiclass             |
| 🧠 Multilayer Perceptron  | `MultilayerPerceptronClassifier` | Binary / Multiclass   | Simple feedforward neural net                       |
| 🧮 Factorization Machines | `FMClassifier`                   | Binary only           | Great for sparse feature data (e.g. CTR prediction) |

### MulticlassClassificationEvaluator

| Metric          | `.setMetricName()` value | Description                                            |
| --------------- | ------------------------ | ------------------------------------------------------ |
| 🧮 **Accuracy**  | `"accuracy"`             | Proportion of correct predictions (macro average).     |
| 📐 **F1 Score**  | `"f1"`                   | Harmonic mean of precision and recall (macro average). |
| 🎯 **Precision** | `"weightedPrecision"`    | Precision weighted by class frequencies.               |
| 🎯 **Recall**    | `"weightedRecall"`       | Recall weighted by class frequencies.                  |

## Metrics 

| 📦 Evaluator Class                     | 🧠 Task Type                  | 📏 Supported Metrics (`.setMetricName()`)                        | 🔎 Description                                                           |
| ------------------------------------- | ---------------------------- | --------------------------------------------------------------- | ----------------------------------------------------------------------- |
| 🧮 `MulticlassClassificationEvaluator` | Classification (multi-class) | `"accuracy"`, `"f1"`, `"weightedPrecision"`, `"weightedRecall"` | Evaluates multi-class classification models.                            |
| ✅ `BinaryClassificationEvaluator`     | Classification (binary)      | `"areaUnderROC"`, `"areaUnderPR"`                               | Evaluates binary classifiers based on ROC or PR curves.                 |
| 📉 `RegressionEvaluator`               | Regression                   | `"rmse"`, `"mse"`, `"mae"`, `"r2"`                              | Evaluates regression models.                                            |
| 📊 `ClusteringEvaluator`               | Clustering                   | `"silhouette"`                                                  | Measures clustering quality using silhouette score (based on distance). |

## Unsupervised learning

| 🔢 Model                           | 🧱 PySpark Class                     | 🧠 Task Type              | 📝 Notes                                                       |
| --------------------------------- | ----------------------------------- | ------------------------ | ------------------------------------------------------------- |
| 📊 **K-Means**                     | `KMeans`                            | Clustering               | Fast, popular centroid-based clustering.                      |
| 🧭 **Gaussian Mixture**            | `GaussianMixture`                   | Clustering               | Soft clustering (probabilistic assignment).                   |
| 🔳 **Bisecting K-Means**           | `BisectingKMeans`                   | Clustering               | Hierarchical divisive clustering.                             |
| 🧮 **LDA**                         | `LDA` (Latent Dirichlet Allocation) | Topic Modeling           | Used for discovering abstract topics in text.                 |
| 🧊 **PCA**                         | `PCA`                               | Dimensionality Reduction | Projects features onto principal components.                  |
| 🧬 **Truncated SVD**               | `TruncatedSVD` *(SynapseML)*        | Dimensionality Reduction | Similar to PCA but works on sparse data (requires SynapseML). |
| 🧱 **Normalizer / StandardScaler** | `Normalizer`, `StandardScaler`      | Preprocessing            | Not models but often used before unsupervised learning.       |


## Modeling: Pipelines and Saving Models

### Prepare 

```py
!pip install pyspark==3.1.2 -q
!pip install findspark -q

# FindSpark simplifies the process of using Apache Spark with Python
import findspark
findspark.init()

from pyspark.ml.regression import LinearRegression
from pyspark.ml.feature import VectorAssembler
from pyspark.sql import SparkSession
from pyspark.ml import Pipeline
# import functions/Classes for metrics
from pyspark.ml.evaluation import RegressionEvaluator


# Create a spark session
spark = SparkSession.builder.appName("Model Persistence").getOrCreate()

# Download the data set
!wget https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-BD0231EN-SkillsNetwork/datasets/diamonds.csv

# Load the dataset into a spark dataframe
diamond_data = spark.read.csv("diamonds.csv", header=True, inferSchema=True)

# Display sample data from dataset
diamond_data.show(5)
```
### Create the model 
```py
# Assemble the columns columns carat,depth and table into a single column named "features"
assembler = VectorAssembler(inputCols=["carat", "depth", "table"], outputCol="features")
diamond_transformed_data = assembler.transform(diamond_data)

# Print the vectorized features and label columns
diamond_transformed_data.select("features","price").show()

# Split the dataset into training and testing sets in the ratio of 70:30.
(training_data, testing_data) = diamond_transformed_data.randomSplit([0.7, 0.3])

# Train linear regression model
lr = LinearRegression(labelCol="price", featuresCol="features")
pipeline = Pipeline(stages=[lr])
model = pipeline.fit(training_data)
```

### Save the model 
```py
# Create a folder "diamond_model". This is where the model will to be saved
!mkdir diamond_model
!mkdir diamond_model

# Persist the model to the folder "diamond_model"
model.write().overwrite().save("./diamond_model/")
```
### Load the model
```py
# Load the model from the folder "diamond_model"
from pyspark.ml.pipeline import PipelineModel
​
# Load persisted model
loaded_model = PipelineModel.load("./diamond_model/")                                                                       
```

### Predict 
```py 
predictions = loaded_model.transform(testing_data)
predictions.select("prediction").show(5)

metrics = {}
for metric in ['r2', 'mae', 'rmse']:
    evaluator = RegressionEvaluator(labelCol="price", predictionCol="prediction", metricName=metric)
    metrics[metric] = evaluator.evaluate(predictions)
print(metrics)

```
