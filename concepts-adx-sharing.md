# How in-place sharing works for Azure Data Explorer

This article describes how in-place sharing works for Azure Data Explorer.

## Sharing data from Azure Data Explorer cluster
Azure Data Share supports the ability to share databases from Azure Data Explorer cluster. Data providers can add databases from existing Azure Data Explorer to a share. 

Data shared from SQL-based sources contains schema and data only. Azure Data Share does not preserve any pre-existing constraints defined on a table or view. Data is shared as a snapshot of the table or view at the time that a snapshot is generated. Azure Data Share does not support incremental copy.

Scheduled incremental copies are not supported for SQL-based sharing. If a snapshot is scheduled, a snapshot of the table as it exists on the originators SQL Server is generated at each scheduled or manual trigger. This means that each time a snapshot is triggered, the full contents of the table are brought across rather than just the delta since the last copy. 

### Receiving SQL-based data in Azure Data Lake Store Gen2 or Azure Storage
Data consumers are able to receive SQL-based data into Azure Data Lake Store Gen2 or Azure Storage. By default, Azure Data Share enables customers to specify a storage location into which they will receive data into. Data is copied into a storage location specified by the data consumer when configuring the data share. Note that the contents of the origin table are copied into a format chosen by the data consumer and any previous data copied is overwritten when a new snapshot is generated. Azure Data Share currently supports receiving data in CSV or Parquet format. 

### Receiving SQL-based data in Azure SQL Database or Azure SQL Data Warehouse
Data consumers can choose to receive data shared with them from the data provider directly into an Azure SQL Server table. When a data consumer triggers a snapshot to receive data shared with them, the table is created into the database that was selected at the time of configuration. If the table does not already exist, it will be created with the original schema (no constraints). If the table already exists, and the schema is consistent with the original schema of the table being shared, data will be appended to the existing table. If the table already exists with a different schema, the table will not be overwritten and the trigger will fail. 

The table generated on the data consumers SQL Server will have the same name as the original table name. 

## Next steps

- Learn how to share data from Azure SQL Database or Azure SQL Data Warehouse - [SQL-based sharing](share-your-sql-data.md)
