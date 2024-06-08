# youtube_data_engineering
An end-to-end data engineering project for analyzing YouTube data, encompassing data ingestion, data lake formation, cloud deployment on AWS, ETL design, scalability, and reporting. This repository includes scripts, workflows, and documentation to guide users through each phase of the project, leveraging Python, AWS services, and data engineering best practices.

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

### On-premise Data Centre vs. Cloud Data Centre

In cost wise, it is efficient to use Cloud Based. In this project we will explore on Amazon Web Services (AWS) which the leading cloud platform next to Microsoft. We can call it one-stop center for cloud services, since many services they offers.

### Data Engineering Process

1. `CREATE AN AWS ACCOUNT`: Click [here](https://portal.aws.amazon.com/billing/signup#/start/email). If, this is your first time login into AWS Dashboard Account, to access the services, you need to activate, by inserting payment method then follow the verification steps. If you already have an account, just sign in into your IAM role account, if you don't have, follow next instruction.
2. `CREATE AWS IAM ROLE ACCOUNT`: Again if you already have an IAM role account you can skip this step. to create and IAM role account, search and click `IAM`, then click  `Users`, then click `add users`. during IAM account setup, here are some component keys that you need to focus on; username, IAM role (programmatic access), passwords, attached existing policies (select AdministratorAccess), download the csv (and save it at secure location). Once IAM role account created, and create new access key and download the csv file once you completed creating access key ( access key, allowing us to pair with other tools to use with the account). Now, you have successfully created the IAM role account together with the secret key, login the IAM account via link given in the csv. that you download earlier.
3. `SETTING UP AWS CLI ON YOUR DEVICE`: You can link your device to install [AWS CLI](https://aws.amazon.com/cli/) either MAC, Windows or Linux. Setting this up will help you fasten up the process. Then, configure your CMD (if using Windows) or Terminal (if using MAC) by inserting command `aws configure` then the system will prompt question like access key, secret access key, region.
4. `SETTING UP AWS S3 BUCKET`: Next, you can go to AWS console (under IAM role account), then create new S3 Bucket. you can name it whatever you want, in this project, I've named my bucket `my-yt-data-analysis-bucket`. <p align="center"><img src="img/aws-s3-ls.png"></p>
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
8. `AWS GLUE FOR DATA INTEGRATION`: When you done uploading the files into S3 Bucket, now, go to `AWS GLUE` then click at `CRAWLER` at the left navigation pane. Create `new crawler` and name it whatever you want,  in this project I've named it as `de-yt-glue-catalog-1`,and for my case, I kept everything in default. Ensure you are using correct S3 Bucket (which contain json file, in this context the directory s3://my-yt-data-analysis-bucket/youtube/raw_statistics_reference_data/, then create new IAM role for this AWS GLUE section. Now, take closer attention for this, open new tab, and go to AWS IAM, click `role` section. Create new role, the choose AWS Service and choose `Glue` for `use cases for other AWS services:`. For permission policies, select `AmazonS3FullAccess` & `AWSGlueServiceRole` then name the role. In this project I've named it as de-on-yt-glue-s3-role. Now get back to the prev tab `AWS Glue - crawler` that we left just now. refresh the `Choose the IAM role` and the select the `de-on-yt-glue-s3-role` that we just create earlier. then Create new database for this, in my case i've create `de_youtuber_raw` databases, then select the database you just created, then click next until you complete setting up the crawlers. Then select the crawler that we just created, then select `RUN Crawler`. Then once it's complete it will fetch data and create and table analysis on what the json file is all about.


















