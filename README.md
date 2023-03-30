# GCP_Hive_BigData

## Creating Dataproc Cluster
I'll be using **GCP's Dataproc** which makes it easy to run Apache Hadoop, Spark, Hive, and Pig jobs on a fully managed cluster. With Dataproc, we can create a cluster of virtual machines that are pre-configured with Hadoop, Spark, and other big data tools & it allows to easily scale up or down the cluster to match our processing needs, and only pay for the resources we use.

So first I create a dataproc cluster with 2 worker nodes. Each worker node contains a YARN NodeManager and a HDFS DataNode.
<img width="942" alt="1_dataproc_cluster" src="https://user-images.githubusercontent.com/71979171/228705724-9398d649-c71e-4487-956b-9aedc268961c.PNG">



Now, let's connect to the Master node VM via SSH. By default, the Master node is created with a public IP address and is accessible via Secure Shell (SSH) for remote access and management. -


<img width="942" alt="2_ssh" src="https://user-images.githubusercontent.com/71979171/228708281-ba241b28-33ed-48e4-9cd3-aafcdad5dfcb.PNG">




## The Data 
In this repository, I have the dataset that I'll be using for this project. The dataset has over 5 Million records (rows) & is stored in a zip file. I'll use the url of this data on the SSH with the command **wget** to load it into HDFS.
