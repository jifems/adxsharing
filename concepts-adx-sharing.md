# How Azure Data Explorer in-place sharing works

Azure Data Share supports the ability to share databases in-place from ADX clusters. Data provider can share at the database or cluster level. When shared at database level, data consumer will only be able to access the specific database(s) shared by the data provider. When shared at cluster level, data consumer can access all the databases from the provider's cluster, including any future databases created by the data provider. To access shared databases, data consumer needs to have its own ADX cluster. When sharing relationship is established, Azure Data Share creates a symbolic link between the  provider and consumer's ADX cluster. 

<img src="./media/adx-sharing-architecture.png" width="60%">

When data consumer accesses the data, data is cached in the consumer's cluster for performance. It is not written to the blob storage account powering the consumer's cluster. Data consumer can only read or query the data, but not write to the database. When data provider revokes access, symbolic link is deleted, and the shared database(s) are no longer available to the data consumer.

Both the provider and consumer's ADX clusters must be in the same Azure Data Center. Cross Azure Data Center sharing is not supported.

Azure Data Explorer supports two modes of data ingestion: batch and streaming. Data received from batch in the shared database will appear between a few seconds to a few minutes on the consumer side. Data received from streaming could take up to 24 hours to appear on the consumer side depending on the volume of the streamed data (the higher the volume, the faster it will appear).

In case of conflicts between databases of leader/follower clusters, when all databases are followed by the follower cluster, they are resolved as follows:
** A database named DB created on the follower cluster takes precedence over a database with the same name created on the leader cluster
** Thus, database DB in the follower cluster needs to be removed (or renamed) in order for the follower cluster to have the leader's database DB.
** A database named DB followed from 2 or more leader clusters will be arbitrarily chosen from one of the leader clusters, and will not be followed more than once.

Commands for showing cluster activity log and history run on a follower cluster will show the activity and history on the follower cluster, and their result sets will not include those of leader cluster(s). For example: a .show queries command run on the follower cluster will only show queries run on databases followed by follower cluster, and not queries run against the same database in the leader cluster.

It is not possible to follow entities in levels lower than a Database (e.g. one cannot follow a specific table or function, nor have a table-level policy overrides which aren't specified above).


## Next steps

- Learn how to [share data from Azure Data Explorer](share-your-adx-data.md)
