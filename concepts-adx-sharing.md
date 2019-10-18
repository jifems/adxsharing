# How Azure Data Explorer in-place sharing works

Azure Data Share supports the ability to share databases in-place from ADX clusters. Data provider can share at the database or cluster level. When shared at database level, data consumer will only able able to access the specific database(s) shared by the data provider. When shared at cluster level, data consumer can access all the databases from the provider's cluster, including any future databases created by the data provider. To access shared databases, data consumer needs to have its own ADX cluster. When sharing relationship is established, Azure Data Share creates a symbolic link between the  provider and consumer's ADX cluster. 

<img src="./media/adx-sharing-architecture.png" width="60%">

When data consumer accesses the data, data is cached in the consumer's cluster for performance. It is not written to the blob storage account powering the consumer's cluster. Data consumer can only read or query the data, but not write to the database. When data provider revokes access, symbolic link is deleted, and the shared database(s) are no longer available to the data consumer.

Azure Data Explorer supports two modes of data ingestion: micro-batch and streaming. Data received from micro-batch in the shared database will appear immediately on the consumer side. Data received from streaming could take a few seconds up to 24 hours to appear on the consumer side depending on the volume of the streamed data (the higher the volume, the faster it will appear).

## Next steps

- Learn how to [share your data from Azure Data Explorer](share-your-adx-data.md)
