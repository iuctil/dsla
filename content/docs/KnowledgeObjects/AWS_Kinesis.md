---
title: "AWS Kinesis"
description: "AWS Kinesis"
lead: "AWS Kinesis"
keywords: 
    - Data Engineering
    - AWS
    - Cloud
contributors:
    - Suresh Kumar Balasundaramsivaprakash
date: 2022-03-01T00:00:00+00:00
lastmod: 2022-03-19T00:00:00+00:00
draft: false
toc: true
plotly: false
images: []
weight: 100
menu:
    docs:
        parent: "KnowledgeObjects"
---
![alt text](https://docs.aws.amazon.com/streams/latest/dev/images/architecture.png)
##  What is AWS Kinesis and what functionality does it provide for us?

Amazon Kinesis could be a managed, scalable, cloud-based service that enables data processing of streaming large amounts of information per second. you'll be able to use Amazon Kinesis to securely stream video from camera-equipped devices in homes, offices, factories, and public places to AWS. you'll then use these video streams for video playback, security monitoring, face detection, machine learning, and other analytics.

## Who Should Use AWS Kinesis ?
We recommend Kinesis to be used cases with requirements that are the same as the following: Routing related records to the identical record processor (as in streaming MapReduce). as an example, counting and aggregation are simpler when all records for a given key are routed to the identical record processor.

## How Do I Learn About it?
Learn the components and use cases of the Amazon Kinesis service and acquire started using Amazon Kinesis to form solutions and solve business problems.
[https://cloudacademy.com/learning-paths/getting-started-with-amazon-kinesis-550/]

## Major Components of AWS Kinesis
There are four main components of Kinesis which will be accustomed accomplish different tasks using their AWS services.
- Kinesis Firehose 
- Kinesis Data Analytics 
- Kinesis Data Streams 
- Kinesis Video Streams

## Kinesis Firehose
![alt text](https://miro.medium.com/max/1400/0*V86zf5ZODmE7w_X7.png)

Kinesis Firehose is liable for loading data into Amazon Web Services. It performs a critical function of reworking and loading data into the Cloud services which are primarily used for analytical purposes. a number of these services include Kinesis Analytics, Amazon Redshift, Amazon S3, Amazon Elasticsearch Service etc. This platform requires no continuous administration and automatically scales and manages its functions in step with the information throughput.

## Kinesis Data Analytics
![alt text](https://d1.awsstatic.com/architecture-diagrams/Product-Page-Diagram_Amazon-Kinesis-Data-Analytics_HIW%402x.918e6d6f5672731b9c4616540578ee9192041f0d.png)

Kinesis Data Analytics may be a platform for analysing and processing any Real-Time streaming data using Standard SQL. it's mainly wont to analyze the info being ingested from Kinesis Firehose and Kinesis Data Streams. It can detect the quality data formats and starts by automatically parsing the information while it recommends a schema which might be customized by the user using the interactive schema editor. The function of the Kinesis Analytics within the data pipeline may be understood using the illustration below.

## Kinesis Data Streams
![alt text](https://m-square.com.au/wp-content/uploads/2018/08/diagram-how-it-works-kinesis-data-streams.249630c459ffe210d013ad06a0f6899ebea1304b-1.png)

Kinesis Data Streams provides a platform for continuous processing of Real-Time streaming data. It will be accustomed collect log events from servers and other mobile deployments. The platform strongly focuses on security and allows its users to encrypt sensitive data using server-side encryption and AWS KMS master keys. Kinesis Data Streams may be created very easily by using Kinesis Producer Library

## Kinesis Video Streams
![alt text](https://tutorialslink.com/Article_img/Blog_image/e1f1492f-6618-4c5c-b0b4-d91c0252b579.jpg)

Kinesis Video Streams provides a use-case specific platform with the flexibility to stream video from Camera-equipped devices to Amazon Web Services. It may be incorporated/implemented to be used cases that involve video streaming over the net or for applications like storage of security footage on Cloud Data Warehouse Deployments. The platform also provides support for WebRTC, which is an open-source project that permits real-time media streaming and interaction between web browsers, mobile applications, and connected devices using simple APIs

## Strengths
There are major Strengths of Amazon Kinesis as follows
- Real-time
Amazon Kinesis enables you to ingest, buffer, and process streaming data in real-time, so you'll derive insights in seconds or minutes rather than hours or days.

- Fully managed
Amazon Kinesis is fully managed and runs your streaming applications without requiring you to manage any infrastructure.

- Scalable
Amazon Kinesis can handle any amount of streaming data and process data from many thousands of sources with very low latencies.


## Limitations

- The records of a stream are by default stored and accessible for up to 24 hours. it's possible to increase this duration by 7 days by enabling extended data retention.
- The maximum size of an information Blob, which refers to the information payload before applying Base64-encoding, for one record is of 1 MB. 
- One Shard [Base Throughput unit of Kinesis Data Stream] can support up to 1000 PUT records each second.

## Alternative Options
- Confluent
- Google Cloud Dataflow
- Spark Streaminng
- Azure Event Hubs
- TIBCO Spotfire

## Video on basics of AWS Kinesis

{{< youtube id="ZjKzGl0O6j8" >}}

## References
1. AWS Kinesis [https://aws.amazon.com/kinesis/](url)
2. Architecture Image [https://docs.aws.amazon.com/streams/latest/dev/images/architecture.png](url)
3. https://cloudacademy.com/learning-paths/getting-started-with-amazon-kinesis-550/
4. https://www.youtube.com/watch?v=ZjKzGl0O6j8&ab_channel=CloudGuru
