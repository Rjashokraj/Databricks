The objective of the project is to build a etl pipeline using databricks.
Here we have used s3 as our data lake
In data bricks we have created an external location which leads to our s3 source bucket
from there we are extracting the data and writing it as delta table
we follow medallion architecture of bronze->silver->gold
bronze layer contains raw data, all data are appended in bronze layer
while writing in bronze layer we partition the table based on date
silver layer contains cleansed data
while reading from bronze layer we read only latest table based on filtering date.
After cleaning we write save the data in silver table
we perform incremental load in silver layer by using merge/insert strategy so only the new / modified data is ingested.
gold contains only business insights and KPI
From silver we read the table and perform required aggregation and transfomation.
all the table are written in delta format.
For each layer we have used different notebooks
Then we create job, integrating notes in 3 different tasks based on layers.
Each task will be dependent on downstream tasks, so if anyone task fails job will not proceed.
Then we orchestrate the job by scheduling.
