---
toc: true
layout: post
description: Why Data Scientist Should Acquire Data Engineering Skills.
categories: [markdown]
title: "Building Models Vs Building Data Pipelines"
---



### Introduction
![](/images/circle.png)
*source*: Lewis Gavin's What is Data Engineering Report.

I have always been a firm proponent of the Oracle of Delphi philosophy, which in essence
admonished humanity thus: 'Know Thyself, For an unexamined Life is not worth living. Between my last post and now, quite a lot has happened, which essentially have allowed me a critical look at my trajectory in the world of Data Science.
Without boring you with the details of these experience, I recently had the opportunity to apply for a data science role in one of the prominent non-profit organization Data organization doing excellent work in the areas of Data Democratization, i.e. making the power of data available to all and sundry irrespective of the level of skills and knowledge.

As part of the application process, the prospective employer gave me a small data problem to solve. On seeing the challenge, I was pleased initially because I assumed it was relatively 'easy' and 'straight forward. I was not required to build any machine learning model, but rather the expectation was to use my python skills to `Extract`, `Transformed` and `Load` data from one state or form to another. I answered and submitted the challenge to the best of my understanding, but it appeared my effort was not good enough as my solution failed to meet my examiners' expectations.

Naturally, I was disappointed initially, but on second thought, I decided to *examine* my performance visa vis my knowledge as a growing Data Scientist. This examination saw me perusing through different sources and seeking the opinion of seasoned professionals in the field. However, I started observing a pattern from my research, and quite frankly, it was pointing towards a gap in skills and exposure. This revelation from my research was quite instructive. Over the years, I have trained myself in the art and craft of building machine learning models from the comfort of my Jupyter notebook. Most of the time, the data used for these machine learning projects were often in flat CSV files. In other words, I was oblivious of any extraction and possibly transformation the data had undergone before taking the form of a CSV flat file.

In technical terms, I lacked Data-pipeline-building Skills, which is a critical aspect of Data Engineering. Is Data Science an endangered career path, Will Data Science be subsumed under Data Engineering? Should Data Scientist acquire Data Engineering skills? If so, how should they go about this? Here are some of the questions begging for answers, some of which we shall attempt to answer in this post.



### How is Data Engineering Different From Data Science?
Data science is an interdisciplinary field and sit at the intersection of statistics/Mathematics, Computer Science and Domain Knowledge. Data Science concerns itself with building machine learning models from algorithms. As a Data Scientist, the bulk of my work centred around manipulating and extracting value from data to aid business decision making. The core of Data science is data cleaning, Exploratory Data Analysis, feature engineering and building Models.
On the other hand, Data engineering tends to lean more on software engineering, especially concerning technology involving data integration, capture and processing. Data engineers concern themselves with building data pipelines via the ETL or ELT paradigm in the data life circle. Data Engineer could be said to provide or build the conduit through which data is made available to the data scientist.

### Data Engineering in Data Life Circle
From the preceding paragraph, it is obvious we used some terms and concepts in our attempt to explain data engineering. Some of these concepts need some unpacking for comprehension to take root. Typically a data life circle involves data extraction, data transformation and data loading. Thus we can say that data engineering essentially consists of the management of the data life circle.

#### Extraction
Data extraction is one of the typical data engineering tasks. As the name implies, data extraction involves:
Collect data from different sources, e.g. databases.
Third-party data providers via API.
Scrap data from the web, e.t.c.
These difference sources are critical to data enrichment. Real-world data don't always come in CSV flat files; instead, they come in different data silos. It is the data engineer's job to extract them into a single form necessary for the subsequent analysis process.

#### Transformation and Loading
 Data cleaning is an aspect of data transformation. According to a Forbes survey, data scientists spend about 80% of their time doing data cleaning. Thus, data scientist, therefore, carries out some data transformation; however, data transformation from the data engineering perspective typically involves building a pipeline that automates and perpetually updates the processes of extraction, transformation, and loading.

 ### Required Skills, Knowledge and Tools as Data Engineers.
 Data engineering is part of the extensive data ecosystem and accounts for the three Vs of big data: Volume, Variety and velocity. Therefore presupposes some levels of skills, knowledge and tools.
 Data engineers are expected to have deep knowledge of the following:

 **Programming Language and Libraries**
 - Python
 - SQL
 - Java
 - Scala
 - Pandas
 - Numpy
 - Scikit-learn
 - Tensorflow e.t.c


 **Databases**
 - Relational Databases e.g MyQSL, Postgres e.t.c.
 - NoSQL
 - Data warehousing
   - Amazon Redshift
   - Google BigQuery
   - Apache Cassandra
   - Elasticsearch e.t.c.

**Data Processing Engines**
- Apache Spark
- Apache Nifi
- Apache Airflow
- Apache Kafka


### ETL in Action

To give us a taste of what the data engineer does in terms of typical code, I decided to share a project I worked on recently.
We would display how to typically extract data from a relational database and load same to Amazon s3
```Python
#import necessary package and libraries
import pymysql
import csv
import boto3
import configparser

# connect to  MySQL database via python mysql package
parser = configparser.ConfigParser()
parser.read("pipeline.conf")
hostname = parser.get("mysql_config", "hostname")
port = parser.get("mysql_config", "port")
username = parser.get("mysql_config", "username")
dbname = parser.get("mysql_config", "database")
password = parser.get("mysql_config", "password")

conn = pymysql.connect(host=hostname,
                       user=username,
                       password=password,
                       db=dbname,
                       port=int(port))


if conn is None:
    print("Error connecting to MySql Database")

else:
    print("MySQL connection established!")

# run a full extraction of the customer table

m_query = "SELECT * FROM customer;"
local_filename = "customer_extract.csv"

m_cursor = conn.cursor()
m_cursor.execute(m_query)
results = m_cursor.fetchall()

# write data unto csv file
with open(local_filename, 'w') as fp:
    csv_w = csv.writer(fp, delimiter='|')
    csv_w.writerows(results)


fp.close()
m_cursor.close()
conn.close()


# upload local csv file to amazon s3

# load the aws_boto_credentials values

parser = configparser.ConfigParser()
parser.read("pipeline.conf")
access_key = parser.get("aws_boto_credentials", "access_key")
secret_key = parser.get("aws_boto_credentials", "secret_key")
bucket_name = parser.get("aws_boto_credentials", "bucket_name")

s3 = boto3.client('s3', aws_access_key_id=access_key, aws_secret_access_key=secret_key)

s3_file = local_filename

s3.upload_file(local_filename, bucket_name, s3_file)
```


The above lines of code would extract all the columns in the customer's table,
save them unto a CSV file format to aid subsequent uploads to the final destination, the Amazon S3 cloud storage facility.

### Conclusion

Data engineering activities share a lot of similarities with data Science activities. And we can say that they complement each other. However, Data engineering over the years has eaten into the job market share of data science as they have become the darlings of start-up firms who, for an apparent reason, would instead employ a data engineer than a sole data scientists. Another reason why data engineering is gaining more grounds than data science could be due to the advent of AutoML. Consequently, I would strongly encourage anyone to acquire data engineering skills, especially practising data scientist or data science enthusiasts. I hope you learn something from today's post.
Bye!
