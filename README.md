# youtube_data_analysis
An end-to-end data engineering project for analyzing YouTube data, encompassing data ingestion, data lake formation, cloud deployment on AWS, ETL design, scalability, and reporting. This repository includes scripts, workflows, and documentation to guide users through each phase of the project, leveraging Python, AWS services, and data engineering best practices.

### Table of content
|||
|:-:|:-:|
|||

### Getting Started**

**Project Overview**

The requirement from `(simulated)` customer:
- Launching new data-driven campaign
- Main advertising channel: `Youtube`
- Initial question to answers:
      1. "How to categorise videos, based on their comments and statistics?"
      2. "What factors affect houw popular a YouTube video `will be`?"
  
**Why Youtube?**

Top three most-visited websites (monthly)
No. 1 - google.com
No. 2 - youtube.com
No. 3 - facebook.com

*source: [Exploding Topics - Most Visited Website in The World (June 2024), by Josh Howarth, published on 1st June 2024](https://explodingtopics.com/blog/most-visited-websites)*

**Goal and Success Criteria**

How my customer will measure success?

`Data Ingestion`: Ingest data, one-offs and incrementally.
`Data Lake`: Design and build a new Data Lake architecture.
`AWS Cloud`: AWS as the Cloud provider.
`ETL Desing`: Extract, transform and load data efficiently.
`Scalability`: The data architecture should scale efficiently.
`Reporting`: Build a Business intelligence tier, include Dashboards.

<!-- 

Note for myself by doing this project

- To build a data lake from scratch in Amazon S3: Joining semi-structure and structure data.
- Lake House architecture design: Best practices --> cost and performance.
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

-->

**Datasets from YouTube**
- Top trending videos
- What is "Trending"?
      1. YouTube uses factors, including users interactions, e.g number of views, shares, comments and likes. Not the most-viewed videos overall for the calendarr year
- Source: Kaggle. Data collected using YouTube API. [Click here](https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqbEhQUy01eWpUSnRpVTRMVkl6Y09RcGkxVEljd3xBQ3Jtc0ttZUZ4a0xaZ0NkVjJtOGpFWHVlRDVjS1d1NDJUaFpaVnQwUGlSemdieW84N29vZUdlT25FOWhpZ0hLbjMwSE10SnF6M3JvbHZ2TkNZM1h0ZHFPdWQ0eVdneXUtM0lKbm4tMERlWGh5NVNfZWlGT1Uxdw&q=https%3A%2F%2Fwww.kaggle.com%2Fdatasnaek%2Fyoutube-new&v=yZKJFKu49Dk) to view & download the datasets getting from Kaggle.

**On-premise Data Centre vs. Cloud Data Centre**

In cost wise, it is efficient to use Cloud Based. In this project we will explore on Amazon Web Services (AWS) which the leading cloud platform next to Microsoft. We can call it one-stop center for cloud services, since many services they offers.

**Log in into your AWS Account under IAM account**




























