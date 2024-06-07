# youtube_data_engineering
An end-to-end data engineering project for analyzing YouTube data, encompassing data ingestion, data lake formation, cloud deployment on AWS, ETL design, scalability, and reporting. This repository includes scripts, workflows, and documentation to guide users through each phase of the project, leveraging Python, AWS services, and data engineering best practices.

<!--
### Table of content
|||
|:-:|:-:|
|||
-->

### Data Management Strategy

**Data Ingestion**: Develop a mechanism to efficiently ingest data from various sources.

**ETL System**: Implement an ETL (Extract, Transform, Load) process to convert raw data into a usable format.

**Data Lake**: Establish a centralized repository to store data from multiple sources, ensuring easy access and management.

**Scalability**: Design the system to scale seamlessly as data volume increases.

**Cloud Integration**: Utilize cloud services, specifically AWS, to handle the processing of large datasets that exceed local computing capabilities.

**Reporting**: Create a dashboard to provide insights and answers to the predefined questions.

### Amazon Web Services (AWS) Overview
`Amazon S3`: Amazon Simple Storage Service (S3) is an object storage service offering industry-leading scalability, data availability, security, and performance.

`AWS IAM`: AWS Identity and Access Management (IAM) enables secure management of access to AWS services and resources. It allows for the creation and control of AWS users and permissions.

`Amazon QuickSight`: QuickSight is a scalable, serverless, and embeddable business intelligence (BI) service powered by machine learning. It is designed to provide fast and actionable insights from your data.

`AWS Glue`: Glue is a serverless data integration service that simplifies the process of discovering, preparing, and combining data for analytics, machine learning, and application development.

`AWS Lambda`: Lambda is a serverless computing service that lets developers run code without provisioning or managing servers. It automatically scales and manages the compute resources needed to run your code.

`AWS Athena`: Athena is an interactive query service that makes it easy to analyze data directly in Amazon S3 using standard SQL. There is no need to move your data; it remains in S3.

### Dataset Used

The dataset utilized is from Kaggle and contains comprehensive statistics on daily popular YouTube videos over an extended period. It includes up to 200 trending videos published daily across various regions, with each region's data stored in its own CSV file. The dataset encompasses several attributes such as video title, channel title, publication time, tags, views, likes, dislikes, description, and comment count. Additionally, it features a `category_id` field specific to each region, which is detailed in the accompanying JSON file.

You can access the dataset [here](https://www.kaggle.com/datasets/datasnaek/youtube-new).


### Architecture Diagram

<p align="center"><img src="img/architecture.jpeg"></p>

### Lake House Architecture Diagram

<p align="center"><img src="img/LakeHouseArchitecture.png"></p>

### AWS Glue Catalog Diagram

<p align="center"><img src="img/AWSGlueCatalog.png"></p>

<p align="center"><img src="img/AWSGlueCatalogExplanation.png"></p>

### Project Overview

The requirement from `(simulated)` customer:
- Launching new data-driven campaign
- Main advertising channel: `Youtube`
- Initial question to answers:

1. "How to categorise videos, based on their comments and statistics?"
2. "What factors affect houw popular a YouTube video `will be`?"
  
**Why Youtube, as leading platform for advertisement usage?**

YouTube is on of the top three most-visited websites (monthly) after google.com

*source: [Exploding Topics - Most Visited Website in The World (June 2024), by Josh Howarth, published on 1st June 2024](https://explodingtopics.com/blog/most-visited-websites)*

<!--
**Goal and Success Criteria**

How my customer will measure success?

`Data Ingestion`: Ingest data, one-offs and incrementally.

`Data Lake`: Design and build a new Data Lake architecture.

`AWS Cloud`: AWS as the Cloud provider.

`ETL Desing`: Extract, transform and load data efficiently.

`Scalability`: The data architecture should scale efficiently.

`Reporting`: Build a Business intelligence tier, include Dashboards.

Note for myself by doing this project
- To build a data lake from scratch in Amazon S3: Joining semi-structure and structure data.
- Lake House architecture design: Best practices > cost and performance.
- Data Lake vs. Data Warehouse.
- Data Lake design in layers, partitioned for cost performance: e.g landing, cleansed as SSOT, reporting for BI users. And, WORM model/write Once Read Many.
- AWS Data Catalogue.
- ETL in AWS Glue Spark jobs: Amazon Sagemaker Jupyter Notebooks.
- Amazon SNS for alerting.
- SQL using Amazon Athena and Spark SQL: i.e impact of querying the optimized data layers.
- Ingest changes incrementally and schema evolution.
- BI Dashboards in Amazon QuickSight.
  
**What is Big Data**
- massive data sets, with varied and complex structure
- with the difficulties of storing and analysing
- visualizing for further processes or results

**Timely decision require new data in minutes**
Data loses value quickly over time, below is the data being valued into decision-making:
-------Time-critical decisions-------
Real-time: Preventive/Predictive
Seconds: Actionable
-------Traditional "batch" business intelligence-------
Minutes ~ Hour: Reactive
Days ~ Month: Historical

**Datasets from YouTube taken from Kaggle by Mitchell J.**
- Top trending videos
- What is "Trending"?

1. YouTube uses factors, including users interactions, e.g number of views, shares, comments and likes. Not the most-viewed videos overall for the calendar year

- Source: Kaggle. Data collected using YouTube API. [Click here](https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqbEhQUy01eWpUSnRpVTRMVkl6Y09RcGkxVEljd3xBQ3Jtc0ttZUZ4a0xaZ0NkVjJtOGpFWHVlRDVjS1d1NDJUaFpaVnQwUGlSemdieW84N29vZUdlT25FOWhpZ0hLbjMwSE10SnF6M3JvbHZ2TkNZM1h0ZHFPdWQ0eVdneXUtM0lKbm4tMERlWGh5NVNfZWlGT1Uxdw&q=https%3A%2F%2Fwww.kaggle.com%2Fdatasnaek%2Fyoutube-new&v=yZKJFKu49Dk) to view & download the datasets getting from Kaggle.
-->

### On-premise Data Centre vs. Cloud Data Centre

In cost wise, it is efficient to use Cloud Based. In this project we will explore on Amazon Web Services (AWS) which the leading cloud platform next to Microsoft. We can call it one-stop center for cloud services, since many services they offers.

### Data Engineering Process

1. `CREATE AN AWS ACCOUNT`: Click [here](https://portal.aws.amazon.com/billing/signup#/start/email). If, this is your first time login into AWS Dashboard Account, to access the services, you need to activate, by inserting payment method then follow the verification steps. If you already have an account, just sign in into your IAM role account, if you don't have, follow next instruction.
2. `CREATE AWS IAM ROLE ACCOUNT`: Again if you already have an IAM role account you can skip this step. to create and IAM role account, search and click `IAM`, then click  `Users`, then click `add users`. during IAM account setup, here are some component keys that you need to focus on; username, IAM role (programmatic access), passwords, attached existing policies (select AdministratorAccess), download the csv (and save it at secure location). Once IAM role account created, and create new access key and download the csv file once you completed creating access key ( access key, allowing us to pair with other tools to use with the account). Now, you have successfully created the IAM role account together with the secret key, login the IAM account via link given in the csv. that you download earlier.
3. `SETTING UP AWS CLI ON YOUR DEVICE`: You can link your device to install [AWS CLI](https://aws.amazon.com/cli/) either MAC, Windows or Linux. Setting this up will help you fasten up the process. Then, configure your CMD (if using Windows) or Terminal (if using MAC) by inserting command `aws configure` then the system will prompt question like access key, secret access key, region.
4. `SETTING UP AWS S3 BUCKET`: Next, you can go to AWS console (under IAM role account), then create new S3 Bucket. you can name it whatever you want, in this project, I've named my bucket `my-yt-data-analysis-bucket`.
5. `DOWNLOAD FROM KAGGLE`: Now, we can proceed to download the applicable data from kaggle, what I've mentioned earlier, download [here](https://www.kaggle.com/datasets/datasnaek/youtube-new). Save it at proper designated folder. Then, direct your `terminal` or `cmd` to the designated folder that you've just save ealier. using `cd` command to change your directory.
6. `UPLOAD FILE FROM YOUR DEVICE TO S3 BUCKET`: Now, as your command line interface in the at correct directory to upload the files. use the command below to start upload json & csv files. Copy the command below and paste on the command line interface.

```shell
aws s3 cp . s3://my-yt-data-analysis-bucket/youtube/raw_statistics_reference_data/ --recursive --exclude "*" --include "*.json"
```

Next, since the csv files information is from differents region, so each file is design to go onto diferrent directory.

```shell
aws s3 cp CAvideos.csv s3://my-yt-data-analysis-bucket/youtube/raw_statistics/region=ca/
aws s3 cp DEvideos.csv s3://my-yt-data-analysis-bucket/youtube/raw_statistics/region=de/
aws s3 cp FRvideos.csv s3://my-yt-data-analysis-bucket/youtube/raw_statistics/region=fr/
aws s3 cp GBvideos.csv s3://my-yt-data-analysis-bucket/youtube/raw_statistics/region=gb/
aws s3 cp INvideos.csv s3://my-yt-data-analysis-bucket/youtube/raw_statistics/region=in/
aws s3 cp JPvideos.csv s3://my-yt-data-analysis-bucket/youtube/raw_statistics/region=jp/
aws s3 cp KRvideos.csv s3://my-yt-data-analysis-bucket/youtube/raw_statistics/region=kr/
aws s3 cp MXvideos.csv s3://my-yt-data-analysis-bucket/youtube/raw_statistics/region=mx/
aws s3 cp RUvideos.csv s3://my-yt-data-analysis-bucket/youtube/raw_statistics/region=ru/
aws s3 cp USvideos.csv s3://my-yt-data-analysis-bucket/youtube/raw_statistics/region=us/
```

*additional notes: as for linux or mac we can use `ls` command on the CLI to list the files, but in windows use this command `dir /s /b /o:gn`. You're welcome.

7. `IMPLEMENTING LAKE HOUSE ARCHITECTURE`: Before we go deep, we need to understand the key elements of the lake house architecture. Scalable Data Lakes, Purpose-built Data Services, Seamless Data Movement, Unified Governance & Performance and Cost-effective. Next, we will setup AWS GLUE.
8. `AWS GLUE FOR DATA INTEGRATION`: When you done uploading the files into S3 Bucket, now, go to `AWS GLUE` then click at `CRAWLER` at the left navigation pane. Create `new crawler` and name it whatever you want,  in this project I've named it as `de-yt-glue-catalog-1`,and for my case, I kept everything in default. Ensure you are using correct S3 Bucket, then create new IAM role for this AWS GLUE section.


















