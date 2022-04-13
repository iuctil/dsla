---
title: "Snowflake Datawarehouse Solution Part 1"
description: "Snowflake Datawarehouse Solution, A Cloud Datawarehouse solution."
#lead: "Google Data Studio is a free tool created by Google used to visualize data and create dashboards."
keywords: 
    - Data warehouse
    - BigData
contributors:
    - Vishwanadh Mandala
date: 2022-02-19T00:00:00+00:00
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
## 	What is Cloud Datawarehouse solution?

It is a set of data warehousing managed services for structural, semi-structural, and unstructured data storage needs. And also, cloud Dataware housing solutions optimized for data engineering, BI, and analytical solutions.

## Ideal Cloud Dataware house should address the below key areas
- Ease of creating instances/instances of Data lake or Data warehouse.
- Ease of managing the Datawarehousing setup such as access, running programs, logs, errors, audits, etc.,
- Ease of scalability or de-scalability.
- Ease of shutting down entire clusteer setup/closing the account.
- Ease in migrations from existing on-premise/other data warehousing.
- Ease of bringing the data from various source applications across the business functions.
- Ease of creating the Internal objects Such as files, Tables(Objects), Views, Rules, transformations, support of modern data types such as JSON, etc.,
- Easy of giving access to BI tools from the data layer.
- Machine learning enablement’s..

## Key Features
- A cloud-based data warehouse that supports big data projects uses massively parallel processing (MPP) to provide high-performance queries on large data volumes. MPP architectures consist of many servers running in parallel to distribute processing and input/output (I/O) loads.
- The most flexible and economical way to store data for analytics is with columnar data warehouses. As columns store and process data instead of rows, columnar databases make aggregate queries, such as those used for reporting significantly faster.

## Successfull Cloud datawarehousing solutions in the Market
- Amazon Redshift.
- Azure.
- Google Big Query.
- Snowflake.

## Cloud Datawarehouse Architecture

![Snowflake](/images/snowflake_one.png "Snowflake")

## Amazon Redshift: The first widely adopted cloud data warehouse.
- For many years, data warehousing was only available as an on-premise solution. Then in November 2012, Amazon Web Services (AWS) launched Redshift, a fully managed, petabyte-scale data warehouse service in the cloud. Although not the first cloud-based data warehouse, it was the first to gain market share through adoption. Redshift’s SQL dialect is based on PostgreSQL, which is well understood by analysts worldwide, and uses an architecture familiar to many on-premises data warehouses users.
- The first step to creating a Redshift data warehouse is to launch a set of nodes, called an Amazon Redshift cluster. After you provision your cluster, you upload your data set and then perform data analysis queries. Regardless of the size of your data set, Amazon Redshift delivers fast query performance using familiar SQL-based tools and business intelligence applications.

## Microsoft Azure Synapse Analytics: Taking SQL beyond data.
- Azure Synapse Analytics is a newer analytics service that brings together enterprise data warehousing and big data analytics. It gives you the freedom to query data using either serverless on-demand or provisioned resources. Azure Synapse offers a unified experience to ingest, prepare, manage, and serve data for your business intelligence (BI) and machine learning (ML) needs.
- At the heart of Azure Synapse is a cloud-native, distributed SQL processing engine. It’s built on the foundation of SQL Server to drive your most demanding enterprise data warehousing workloads. Similar to other cloud MPP solutions, Azure SQL Data Warehouse (SQL DW) separates storage and compute, billing for each separately. Azure Synapse saves relational tables data with columnar storage and abstracts physical machines by representing compute power in the form of data warehouse units (DWUs). This allows your users to easily and seamlessly scale compute resources at will.

## Google BigQuery: A serverless solution.
- BigQuery is a fully managed, serverless data warehouse that automatically scales to match storage and computing power needs. Google doesn’t expect you to manage your data warehouse infrastructure which is why BigQuery hides many of the underlying hardware, database, nodes, and configuration details. Its elasticity automatically works out of the box. And getting started is simply a matter of creating an account with Google Cloud Platform (GCP), loading a table, and running a query. Google takes care of the rest.
- With BigQuery, you get a columnar and ANSI SQL database that can analyze terabytes to petabytes of data at incredible speeds. BigQuery also lets you do spatial analysis using familiar SQL with BigQuery GIS. In addition, you can quickly build and operationalize ML models on large-scale structured or semi-structured data using simple SQL with BigQuery ML. And you can support real-time interactive dashboarding with BigQuery BI Engine.

## Snowflake Cloud Data Warehouse: The first multi-cloud datawarehouse.
- Snowflake is a fully managed multi cloud-based data warehouse that runs on AWS, GCP, and Azure. Snowflake, unlike the other data warehouses profiled here, is the only solution that doesn’t run on its own cloud. With a common and interchangeable code base, Snowflake features global data replication, which means you can move your data to any cloud, in any region — without having to re-code your applications or learn new skills.
- When you’re a Snowflake user, you can spin up as many virtual warehouses as you need to parallelize and isolate the performance of individual queries. Snowflake enables very high concurrency by separating storage and compute to ensure that many warehouses can simultaneously access the same data source.

## Snowflake, A Market Leader in Datawarehouse as a service.
- Hundreds of millions of data sets globally remain siloed in SaaS applications, cloud data storage, and on-premises data centers. This decades-old issue prevents organizations from getting all the value from all their data.
- The Data Cloud eliminates the barriers created by siloed data. It is an ecosystem of thousands of organizations connecting to their data, and connecting to each other, by seamlessly sharing and consuming data and data services in live, governed, and secure ways. The technology that unites this ecosystem and enables the Data Cloud is Snowflake’s Cloud Data Platform.

## Snowflake Topology. Snowflake can be built either on GCP, AWS, or Azure. As a customer/user, you need to select one cloud offering during the initial setup.

![Snowflake](/images/snowflake_two.png "Snowflake")

## Training
- Snowflake provides one month free trail account to practise cloud services.
- START 30-DAY FREE TRIAL.
	- https://signup.snowflake.com/?utm_source=google&utm_medium=paidsearch&utm_campaign=na-us-en-brand-core-phrase&utm_content=go-eta-evg-ss-free-trial&utm_term=c-g-snowflake-p&_bt=579123129280&_bk=snowflake&_bm=p&_bn=g&_bg=136172943828&&gclsrc=aw.ds&gclid=EAIaIQobChMIloHW37CS9gIVwmtvBB2M0QakEAAYASAAEgKTZfD_BwE&gclsrc=aw.ds
	- Fill the below entrees.
		- First name.
		- Last name.
		- Email.
		- Company.
		- Country.
		- Choose Standard Subscription.
		- Choose AWS, GCP, or Azure.
		- Refer the below screenshot.
			- ![Snowflake](/images/snowflake_three.png "Snowflake") 
			- ![Snowflake](/images/snowflake_four.png "Snowflake") 
			- ![Snowflake](/images/snowflake_five.png "Snowflake") 
	

## References
1. Snowflake documentation - https://docs.snowflake.com/en/
2. Cloud datawarehouse platforms - https://www.altexsoft.com/blog/snowflake-redshift-bigquery-data-warehouse-tools/
3. Snowflake Trial account creation - https://signup.snowflake.com/?utm_source=google&utm_medium=paidsearch&utm_campaign=na-us-en-brand-core-phrase&utm_content=go-eta-evg-ss-free-trial&utm_term=c-g-snowflake-p&_bt=579123129280&_bk=snowflake&_bm=p&_bn=g&_bg=136172943828&&gclsrc=aw.ds&gclid=EAIaIQobChMIloHW37CS9gIVwmtvBB2M0QakEAAYASAAEgKTZfD_BwE&gclsrc=aw.ds
4. Cloud datawarehouse platforms comparisons - https://www.firebolt.io/resources/data-warehouse-comparison-guide
5. Ten best cloud datawarehouses - https://solutionsreview.com/data-management/the-best-cloud-data-warehouse-solutions-2/
