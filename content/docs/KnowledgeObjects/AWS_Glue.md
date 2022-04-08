# AWS Glue

## 	What is Glue and what functionality does it provide for us?

Glue is a fully managed serverless extract-transform-load (ETL) service that helps us organize and format our data for use with a data warehouse like Redshift, for example,
or if we wanted to, we could use it with data lake in S3 (Simple Storage Service). 

![alt text](../img/glue1.png)

## When Should You Use It?
- When to do data integration as the process of setting up and putting together data for analytics, application development, and machine learning.
- It seamlessly integrate with AWS services. 
AWS Glue is integrated across a wide range of AWS services, so it natively supports data stored in Amazon Aurora, Amazon RDS engines, Amazon Redshift, Amazon S3, as well as common database engines and Amazon VPC. This leads to reduced hassle while onboarding.
- Do not want handle operational complexity and focus on business use case, it is serverless, so there are no compute resources to configure and manage. It handles provisioning, configuration, and scaling of the resources required to run your ETL jobs on a fully managed, scale-out Apache Spark environment. This is quite cost-effective as you pay only for the resources used while your jobs are running.

## How Do I Learn About it?
- AWS digital training offers free self paced tarining 
    - https://aws.amazon.com/training/digital/
- AWS Training and Certification Blogs
    - https://aws.amazon.com/blogs/training-and-certification/?nc2=sb_bl

## FAQ's
- https://aws.amazon.com/glue/faqs/

## Terminologies & Configurations
- DPU's : Data Processing Units

    - 1 DPU has 4vCPU and 16Gig Memory
    - Apache Spark, Python , Spark Streaming    
- Security - Support encryption at Rest.

## Main Components in Glue
- AWS Glue Data Catalog - This is basically a central repository for your metadata, built to hold information in metadata tables — with each table pointing to a single data store. In other words, it acts as an index to your data schema, location, and runtime metrics, which are then used to identify the targets and sources of your ETL (Extract, Transform, Load) jobs. 
- Job Scheduling System - The job scheduling system, on the other hand, is intended to help you automate and chain your ETL pipelines. It comes in the form of a flexible scheduler that’s capable of setting up event-based triggers and job execution schedules. 
- ETL Engine - AWS Glue’s ETL engine is the one component that handles ETL code generation. It automatically provides this in Python or Scala, and then proceeds to even give you the option of customizing the code. 

## Strengths
- Serverless - As a serverless data integration service, AWS Glue saves you the trouble of building and maintaining infrastructure. It is Amazon that provides and manages the servers. 
- Automatic Schema Discovery
- Automatic ETL code - AWS Glue is capable of automatically generating ETL pipeline code in Scala or Python — based on your data sources and destination. This not only streamlines the data integration operations but also gives you the privilege of parallelizing heavy workloads. 
- Increased data visibility - By acting as the metadata repository for information on your data sources and stores, the AWS Glue Data Catalog helps you keep tabs on all your data assets. 
- Developer endpoints - For users who prefer to manually create and test their own custom ETL scripts, AWS Glue facilitates the whole development process through what it calls “developer endpoints.”
- Job scheduling - AWS Glue provides easy-to-use tools for creating and following up job tasks based on schedule and event triggers, or perhaps on-demand. 
- Pay-as-you-go - The service doesn’t force you to commit to long-term subscription plans. Instead, you can minimize your usage costs by paying only when you need to use it.
## Limitations
- Even it is serverless and managed service it needs expertise in apache spark to do customizations compared to Talend, Informatics or similar ETL tools.
- AWS Glue is good match with AWS services(S3, Redshift, RDS) but it is not easy to use with other non AWS services or multicloud environment.
- It is not ideal for real-time data use case
- 
## Alternative Options
- AWS Batch
- AWS DMS - Data Migration Tool
- Databricks
- Informatica PowerCenter
- Alteryx Designer
- Talend Data Fabric
- Oracle GoldenGate
- Splunk 

## References
1. Amazon’s official documentation - https://docs.aws.amazon.com/glue/index.html
2. https://www.gartner.com/reviews/market/data-integration-tools/vendor/amazon-web-services/product/aws-glue/alternatives
