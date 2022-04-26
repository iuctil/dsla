---
title: "AWS Glue Local Development Quickstart"
description: "AWS Glue Local Development Quickstart"
#lead: "AWS Glue Local Development Quickstart"
keywords: 
    - Data ETL
    - Data Enginnering
contributors:
    - Pankaj Dange
    - Suresh Kumar Balasundaramsivaprakash
date: 2022-04-02T00:00:00+00:00
lastmod: 2022-04-11T00:00:00+00:00
draft: false
toc: true
plotly: false
images: []
weight: 100
menu:
    docs:
        parent: "KnowledgeObjects"
---
![AWS Glue Local](/images/glue_local_logo.png "AWS Glue Local")


 In this article, we will learn how to setup AWS Glue using Docker and Jupyter notebook (with sample ETL code) on local laptop or desktop (Windows). This quick learning article will be super useful for users who wants to get started developing data transformation script without waiting to get an access for AWS cloud.

Note: The goal is to get up and running with AWS Glue ETL functions in the shortest possible time, at no cost and without any AWS environment dependency.

## 	Prerequisites
- Before you start, make sure that Docker is installed and the Docker daemon is running. For installation instructions, see the Docker documentation for Windows. 
- The machine running the Docker hosts the AWS Glue container. Also make sure that you have at least 7 GB of disk space for the image on the host running the Docker.
- Basic python and spark knowledge will be needed
- A desktop Mac or Windows with Docker installed  and running
    - https://docs.docker.com/desktop/windows/install/
## Instllation and Configuration Steps 
#### Setup Glue using Docker
1. Run Docker command using powershell on windows 
    ```
        - docker pull amazon/aws-glue-libs:glue_libs_2.0.0_image_01
    ```
2. Make sure image downloaded successfully run below command (powershell) and validate as mentioned in below screenshot
    ```
        - docker ps
    ```
    
   !["AWS Glue"](/images/glue_docker1.PNG "AWS Glue")

3. Run docker image with below command using powershell
    ```
     docker run -itd -p 8888:8888 -p 4040:4040  --name dskb_glue_2.0.0 amazon/aws-glue-libs:glue_libs_2.0.0_image_01 /home/glue_user/jupyter/jupyter_start.sh -e DISABLE_SSL="true"
    ```
4. Go to Docker Desktop and navigate to Images and click on Run to start the container
    ![AWS Glue Local](/images/glue_docker_desktop_img.PNG "AWS Glue Local")

- Congratulations !!  you have successfully setup Glue and Jupyter notebook using Docker Container

5. If you have to explore more within docker container check below options
     ![AWS Glue Local](/images/glue_docker_insight.PNG "AWS Glue Local")

###### Build & Run Glue ETL/Data Exploration scripts  using Jupyter Notebook 
- We use small example datasets for our use case and go through the transformations of several AWS Glue ETL PySpark functions: Filter, SelectFields, Map and Write Dynamic Frame.

1. Open browser on your local machine and type https://127.0.0.1:8888/lab/
    ![AWS Glue Local](/images/glue_jupyter_local.PNG "AWS Glue Local")
2. Create your notbook as mentioned in above image, load required glue libs,
```python
import sys
from pyspark.context import SparkContext
from awsglue.context import GlueContext
from awsglue.transforms import *
from awsglue.dynamicframe import DynamicFrame
from pyspark.sql.types import *
from pyspark.sql import Row
```
3. Load Glue context
```python
glueContext = GlueContext(SparkContext.getOrCreate())
```
4. Create sample dataset and print schema
```python
order_list = [
               ['10', '62', 'YES', '148901234', '75001'],\
               ['11', '54', 'YES', '148901256', '75034'],\
               ['12', '82', 'YES', '148901300', '75123'],\
               ['13', '91', 'NO', '148901400', '82291'],\
               ['14', '32', 'NO', '148902000', '90293']\
             ]
# Define schema for the order_list
order_schema = StructType([  
                      StructField("order_id", StringType()),
                      StructField("customer_id", StringType()),
                      StructField("essential_item", StringType()),
                      StructField("timestamp", StringType()),
                      StructField("zipcode", StringType())
                    ])

# Create a Spark Dataframe from the python list and the schema
df_orders = spark.createDataFrame(order_list, schema = order_schema)
df_orders.show()
```
![AWS Glue](/images/glue_order_schema.PNG "AWS Glue")
5. How to use Filter function
```python
df_order_filter = Filter.apply(frame = df_order, f = lambda x: x["essential_item"] == 'YES')
df_order_filter.toDF().show()
```

6.  How to use Map function - Map allows  to apply a transformation to each record of a data Frame. For this case, we want to target a certain zip code for next day air shipping. We implement a simple “next_day_air” function and pass it to the data Frame:
```python
# Input 

# This function takes in a dynamic frame record and checks if zipcode # 75034 is present in it. If present, it adds another column 
# “next_day_air” with value as True
# Glue Map - https://docs.aws.amazon.com/glue/latest/dg/aws-glue-api-crawler-pyspark-transforms-map.html
def next_day_air(rec):
  if rec["zip"] == 75034:
    rec["next_day_air"] = True
  return rec
```
```python
mapped_df =  Map.apply(frame = order_schema, f = next_day_air)
mapped_df.toDF().show()
```

7. How to use transformations with JSON data, e.g
```python
# Input 
jsonStr1 = u'{ "zip": 75091, "customers": [{ "id": 623, "address": "108 abc Street, ZX"}, { "id": 231, "address": "763 xyz  Ln, TXT" }]}'
jsonStr2 = u'{ "zip": 81091, "customers": [{ "id": 201, "address": "771 TTT Pkwy, GAO" }]}'
jsonStr3 = u'{ "zip": 75023, "customers": [{ "id": 343, "address": "66 P Street, NJ" }]}'
jsonStr4 = u'{ "zip": 93893, "customers": [{ "id": 932, "address": "7008 Fed Ln, MA"}, { "id": 102, "address": "8107 Dean Dr, CA" }]}'
df_row = spark.createDataFrame([
  Row(json=jsonStr1),
  Row(json=jsonStr2),
  Row(json=jsonStr3),
  Row(json=jsonStr4)
])

df_json = spark.read.json(df_row.rdd.map(lambda r: r.json))
df_json.show()
```

### Conclusion
This article discussed How to set up Glue locally using Docker container and  run the PySpark ETL capabilities of AWS Glue using Jupyter Notebook. 

### References
[1] https://aws.amazon.com/blogs/big-data/developing-aws-glue-etl-jobs-locally-using-a-container/#notebook_pyspark_code_sample

[2] https://docs.aws.amazon.com/glue/latest/dg/aws-glue-api-crawler-pyspark-transforms-map.html

[3] https://aws.amazon.com/blogs/big-data/building-an-aws-glue-etl-pipeline-locally-without-an-aws-account/
    