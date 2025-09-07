# Reflection Memo

Working through this exercise gave me valuable insights into Azure’s data analytics.
The biggest surprise about Azure tooling was how easily with few clicks different services integrate. With just a few clicks, I was able to connect Data Factory pipelines, Databricks notebooks, and Synapse serverless SQL, all backed by the same Azure Data Lake storage account. The auto-generated SQL in Synapse Studio  particularly seamlessly allowed me to query parquet files on-demand without spinning up dedicated infrastructure.

As major challenge I encountered was - authentication and file formats. Initially, I struggled with container-level SAS tokens because Spark allows only one token per storage account configuration. This caused read/write failures across `rawdata` and `curated` containers. The fix was generating an account-level SAS token with `rlcw` permissions, which immediately simplified access and resolved the issue. Another challenge was duplicate-looking rows in Synapse; the fix was cleaning the Region field in Spark with `trim()` and `upper()` before aggregation.

From this project, I learned that Data Factory is best suited for **orchestrating ETL workflows**—moving and scheduling data pipelines across sources. In contrast, Databricks notebooks are ideal for **data transformation, advanced analytics, and iterative exploration**. Using them together combines the reliability of orchestration with the flexibility of distributed compute.

