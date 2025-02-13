# Formula-1-Data-Engineering-Project-Using-Azure-Databricks
<h3>Project Overview:</h3>
This project focuses on developing a data analysis solution for Formula 1 race results using Azure Databricks. It involves building an ETL pipeline to ingest, transform, and load Formula 1 racing data into a data warehouse for reporting and analysis. The data, sourced from Ergast.com a platform dedicated to Formula 1 statistics is stored in Azure Data Lake Gen2. Data transformation and analysis are carried out using Azure Databricks, with the entire workflow orchestrated through Azure Data Factory.


#### Execution Overview:
- Azure Data Factory (ADF) is responsible for the execution of Azure Datarbicks notebooks as well as monitoring them. We import data from Ergast API to Azure Data Lake Storage Gen2 (ADLS). The raw data is stored in the container at **Bronze zone** (landing zone).
- Data in the Bronze zone is ingested using Azure Databricks notebook. The data is transformed into delta tables using upsert functionality. ADF then uploads the data to ADLS **Silver zone** (standardization zone). 
- Ingested data in **Silver zone** is transformed using Azure Databricks SQL notebook. Tables are joined and aggregated for analytical and visualization purposes. The output is loaded to the **Gold zone** (analytical zone).

#### ETL Workflow:
ETL flow comprises two parts:
1. Ingestion: Process data from **Bronze zone** to **Silver zone**
2. Transformation: Process data from **Silver zone** to **Gold zone**

In the first pipeline, data stored in JSON and CSV format is read using Apache Spark with minimal transformation saved into a delta table. The transformation includes dropping columns, renaming headers, applying schema, and adding audited columns (```ingestion_date``` and ```file_source```) and ```file_date``` as the notebook parameter. This serves as a dynamic expression in ADF.

In the second pipeline, Databricks SQL reads preprocessed delta files and transforms them into the final dimensional model tables in delta format. Transformations performed include dropping duplicates, joining tables using join, and aggregating using a window.

ADF is scheduled to run every Sunday at 10 PM and is designed to skip the execution if there is no race that week. We have another pipeline to execute the ingestion pipeline and transformation pipeline using file_date as the parameter for the tumbling window trigger.


## Resources Used for this Project:
* Azure Data Lake Storage
* Azure Data Factory
* Azure Databricks
* Azure Key Vault

## Tasks performed:

•	Built a solution architecture for a data engineering solution using Azure Databricks, Azure Data Lake Gen2, Azure Data Factory, and Power BI.

•	Created and used Azure Databricks service and the architecture of Databricks within Azure.

•	Worked with Databricks notebooks and used Databricks utilities, magic commands, etc.

•	Passed parameters between notebooks as well as created notebook workflows.

•	Created, configured, and monitored Databricks clusters, cluster pools, and jobs.

•	Mounted Azure Storage in Databricks using secrets stored in Azure Key Vault.

•	Worked with Databricks Tables, Databricks File System (DBFS), etc.

•	Used Delta Lake to implement a solution using Lakehouse architecture.

•	Created dashboards to visualize the outputs.

•	Connected to the Azure Databricks tables from PowerBI.


<h3>Technologies/Tools Used:</h3>
<ul>
  <li>Pyspark</li> 
  <li>Spark SQL</li> 
  <li>Delta Lake</li> 
  <li>Azure Databricks </li> 
  <li>Azure Data Factory</li> 
  <li>Azure Date Lake Storage Gen2</li> 
  <li>Azure Key Fault</li> 
  <li>Power BI</li> 
</ul>  
