# Working with Big Data & Tables on GCP using Hadoop & Apache Hive

Analyzing data of over a billion rows using Hadoop with Apache Hive on Google Cloud Platform (GCP)

## Creating Dataproc Cluster
I'll be using **GCP's Dataproc** which makes it easy to run Apache Hadoop, Spark, Hive, and Pig jobs on a fully managed cluster. With Dataproc, we can create a cluster of virtual machines that are pre-configured with Hadoop, Spark, and other big data tools & it allows to easily scale up or down the cluster to match our processing needs, and only pay for the resources we use.

So first I create a dataproc cluster with 2 worker nodes. Each worker node contains a YARN NodeManager and a HDFS DataNode.
<img width="942" alt="1_dataproc_cluster" src="https://user-images.githubusercontent.com/71979171/228705724-9398d649-c71e-4487-956b-9aedc268961c.PNG">



Now, let's connect to the Master node VM via SSH. By default, the Master node is created with a public IP address and is accessible via Secure Shell (SSH) for remote access and management. -

## The Data 
In this repository, I have the dataset that I'll be using for this project. It's about consumers and their details like age, gender, country, salaries etc. (At a later point, I'll perform a transformation that finds average salary figure for each country) 
<img width="261" alt="0_data" src="https://user-images.githubusercontent.com/71979171/228745950-a1ee2d24-ae5a-4d5f-b52c-1775fb683716.PNG">

The dataset has over 5 Million records (rows) & is stored in a zip file. I'll use the url of this data on the SSH with the command **wget** to load it into HDFS.


<img width="945" alt="2_ssh" src="https://user-images.githubusercontent.com/71979171/228710704-2a6bb08d-624e-44e3-9c8a-d8b4b7b45f5c.PNG">


I'll unzip the file & copy the data (with 5 million rows x) 200 times to generate a combined data of **over 1 billion records**.
Then, I'll put all the 200 files into the Hadoop Distributed File System (HDFS) and proceed to Hive.
Using Hive, let's create a database & a table for our data -

![image](https://user-images.githubusercontent.com/71979171/228740994-e617cd8e-30d5-44a0-863a-251a5ef6f34c.png)


Now, I'll perform a simple aggregation transformation of taking salary of each consumer from this table, finding out average salary for each country, ans storing the result in a new table. 

It can be seen that 40 Mappers & over 1000 Reducers have been assigned to process this operation. Naturally, over 95% of elapsed time is consumed during the Map task!
<img width="936" alt="4_Mapper" src="https://user-images.githubusercontent.com/71979171/228743964-69028835-17ea-4585-b6f6-6341a1af5d22.PNG">

<img width="956" alt="4_Reducer" src="https://user-images.githubusercontent.com/71979171/228743979-5476c94c-9163-4a9b-a76b-5fcf85f50740.PNG">

Finally, we have a CountrySalaries Table which has average salary for each country -

<img width="649" alt="5_Result" src="https://user-images.githubusercontent.com/71979171/228745390-a6e1dec1-0e32-4334-aef5-102c7142c2f1.PNG">


This table can be later used for reporting, analytics through BI tools.
