# Healthcare Delta Live Table Pipeline

1. Tech stack - Databricks, Pyspark, Delta Lake, Delta Live Tables.
2. Setup notebook to create raw diagnosis mapping and raw daily patients delta table.
3. Ingest one time static data in raw diagnosis mapping from Databricks volume path, raw daily patients delta table will keep on getting incremental data from mock, Pyspark job.
4. Setup notebook and add SQL declarative logics to create bronze, silver, and gold layer delta tables.
5. Create delta live table pipeline job and add above notebook to create lineage among tasks, validate the delta life table pipeline, run it.
