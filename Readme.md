# Healthcare Delta Live Table Pipeline

1. Tech stack - Databricks, Pyspark, Delta Lake, Delta Live Tables.
2. Setup notebook to create raw diagnosis mapping and raw daily patients delta table.
3. Ingest one time static data in raw diagnosis mapping from Databricks volume path, raw daily patients delta table will keep on getting incremental data from mock, Pyspark job.
4. Setup notebook and add SQL declarative logics to create bronze, silver, and gold layer delta tables.
5. Create delta live table pipeline job and add above notebook to create lineage among tasks, validate the delta life table pipeline, run it.

## What does the Data look like?
We have a diagnosis mapping table which is one time ingestion and can be joined to other data for some transformation.  
  
<img width="600" height="600" alt="image" src="https://github.com/user-attachments/assets/7903b386-31d3-4ec6-a22b-a9c3e0e3293d" />  

Then we have some patiests data that is coming in daily and have info like patient id, name, admission date and their diagnosis.  

<img width="700" height="500" alt="image" src="https://github.com/user-attachments/assets/6770faab-9242-4dc2-922d-6a1fcfd1adcd" />  

## DLT Pipeline
The pipeline follows the medallion architecture i.e. it would be having 3 layer consisting of bronze, silver and gold. The following diagram shows the dlt pipeline graph.  

<img width="700" height="389" alt="image" src="https://github.com/user-attachments/assets/34a3f22f-fb44-4e53-a60d-ca402309830e" />  

The first table in bronze layer is diagnostic_mapping which is a materialized view. The second is daily_patients which is a streaming table and it is streaming from raw_daily_patients which is made by mock notebook to increment manually from the volume.  

<img width="685" height="601" alt="image" src="https://github.com/user-attachments/assets/9032f3d3-18a0-4428-bfe1-9d8fcd0e5dc9" />  

Now we have a table called processed_patient_data in silver layer which joins the 2 tables and is also a streaming table.  

<img width="700" height="566" alt="image" src="https://github.com/user-attachments/assets/4f6517fd-d412-4631-bf8d-87fbab30b0c2" />  

In gold layer, we are making two of the tables based on different aggregations. Both are materialized views as it is needed to perform the aggregation on whole dataset.  

<img width="600" height="600" alt="image" src="https://github.com/user-attachments/assets/85f221f7-94af-4124-b990-1a92bec21541" />  

After running the feed raw notebook, we can set up the dlt pipeline and attach the healthcare_dlt_pipeline notebook with it. We can then validate the lineage in development mode and get the above graph.









