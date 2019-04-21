



#Deployment of On-Demand Cluster 







##Create and Configure Azure Data Factory 

In this lab, you will learn how to create on-demand Azure Databricks cluster and run jobs using Azure Data Factory.
Setup 

###Setting up Azure blob Storage 

1.In the Azure portal tab in your browser and click  Create a resource.

2. In the Storage category, click Storage account.

3. Create a new storage account with the following settings:
• Name: Specify a unique name (and make a note of it)
• Deployment model: Resource manager
• Account kind: Storage (general purpose v1)
• Location: Choose the same location as your Databricks workspace
• Replication: Locally-redundant storage (LRS)
• Performance: Standard
• Secure transfer required: Disabled
• Subscription: Choose your Azure subscription
• Resource group: Choose the existing resource group for your Databricks workspace
• Virtual networks: Disabled

4. Wait for the resource to be deployed. Then view the newly deployed storage account.

5. In the blade for your storage account, click Blobs.

6. In the Browse blobs blade, click  Container, and create a new container with the following
settings:
• Name: spark
• Public access level:  Anonymous 

7. In the Settings section of the blade for your blob store, click Access keys and note the Storage
account name and key1 values on this blade – you will need these in the next procedure.

8. Go to Storage explorer ( preview)  and then create a folder data  inside the container spark

9.  Upload the file IISlog.txt

###Task 1

####Import the Notebook 
1.	Go to the Azure Databricks workspace

2.	Click import and import ProcessLog.py

3.	Go to the Account        

4.	Go to user settings and click Generate new token 

5.	Note down the token 

###Task 2 

####Create an Azure data factory 

•	Go to Create a Resource | Analytics | Data Factory 

•	Provide the details 
a.	Unique name 
b.	Select the resource group already used in the lab 
c.	Use location as west Europe 


###Task 3 

Use Edge \Chrome 
####Create a Linked Service 

•	Go to the newly created resource and click on author and monitoring 

•	 A new window will open in the browser. Wait for few minutes to open 

•	Click on Author 

•	Click on Connections and under linked services , click new 

•	Select the compute tab and choose Azure Databricks and then select continue 

•	Provide the following details 
a.	Unique name 
b.	Provide the ADB access token
c.	Rest as follows 
 

•	Go to advance and under spark conf settings , add two name value pair
i.	Name: fs.azure.account.key.databrickshacks.blob.core.windows.net  
Value : <XXX Storage account Key>
ii.	Name : spark.hadoop.fs.azure.account.key.databrickshacks.blob.core.windows.net 
Value :  <XXX storage account key >

d.	Click Finish
###Task 4 

####Create a Pipeline 
1.	Go to authoring page and click on pipeline and select Add Pipeline

2.	Select DataBricks and Drag Notebook

3.	Give a unique notebook name 

4.	Under Azure Databricks, select the newly created ADB linked service

5.	Go to Settings and click browse.

6.	To add  notebook , traverse and add Processlog

7.	Click Publish All

###Task 5 
####Run and monitor 
1.	Once published Successfully , add trigger and trigger now.

2.	Click finish

3.	Go to Monitor  
 
4.	Monitor the pipeline and observe to the pipeline

5.	Go to the blob\spark\data and find a part_ file that got created.

6.	Download and view the data 




