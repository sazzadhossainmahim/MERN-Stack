Document Database
A record in MongoDB is a document, which is a data structure composed of field and value pairs. MongoDB documents are similar to JSON objects. The values of fields may include other documents, arrays, and arrays of documents.
The advantages of using documents are:
•	Documents (i.e. objects) correspond to native data types in many programming languages.
•	Embedded documents and arrays reduce need for expensive joins.
•	Dynamic schema supports fluent polymorphism.
Collections/Views/On-Demand Materialized Views
MongoDB stores documents in collections. Collections are analogous to tables in relational databases.
Databases and Collections
MongoDB stores data records as documents (specifically BSON documents) which are gathered together in collections. A database stores one or more collections of documents.
document
A record in a MongoDB collection and the basic unit of data in MongoDB. Documents are analogous to JSON objects but exist in the database in a more type-rich format known as BSON. See Documents.
MongoDB stores data records as BSON documents. BSON is a binary representation of JSON documents, though it contains more data types than JSON. For the BSON spec
Key Features
High Performance
MongoDB provides high performance data persistence. In particular,
•	Support for embedded data models reduces I/O activity on database system.
•	Indexes support faster queries and can include keys from embedded documents and arrays.
Rich Query Language
MongoDB supports a rich query language to support read and write operations (CRUD) as well as:
•	Data Aggregation
•	Text Search and Geospatial Queries.
High Availability
MongoDB's replication facility, called replica set, provides:
•	automatic failover
•	data redundancy.
A replica set is a group of MongoDB servers that maintain the same data set, providing redundancy and increasing data availability.
Horizontal Scalability
MongoDB provides horizontal scalability as part of its core functionality:
•	Sharding distributes data across a cluster of machines.
•	Starting in 3.4, MongoDB supports creating zones of data based on the shard key. In a balanced cluster, MongoDB directs reads and writes covered by a zone only to those shards inside the zone. See the Zones manual page for more information.
Support for Multiple Storage Engines
MongoDB supports multiple storage engines:
•	WiredTiger Storage Engine (including support for Encryption at Rest)
•	In-Memory Storage Engine.
In addition, MongoDB provides pluggable storage engine API that allows third parties to develop storage engines for MongoDB.

MongoDB CRUD Operations
CRUD operations create, read, update, and delete documents.
Create Operations
Create or insert operations add new documents to a collection. If the collection does not currently exist, insert operations will create the collection.
Explicit Creation¶
MongoDB provides the db.createCollection() method to explicitly create a collection with various options, such as setting the maximum size or the documentation validation rules. If you are not specifying these options, you do not need to explicitly create the collection since MongoDB creates new collections when you first store data for the collections
Document Validation
By default, a collection does not require its documents to have the same schema; i.e. the documents in a single collection do not need to have the same set of fields and the data type for a field can differ across documents within a collection.
Modifying Document Structure
To change the structure of the documents in a collection, such as add new fields, remove existing fields, or change the field values to a new type, update the documents to the new structure.
Unique Identifiers
Collections are assigned an immutable UUID. The collection UUID remains the same across all members of a replica set and shards in a sharded cluster.
Databases and Collections
MongoDB stores data records as documents (specifically BSON documents) which are gathered together in collections. A database stores one or more collections of documents.
Collections
MongoDB stores documents in collections. Collections are analogous to tables in relational databases.
Views
A MongoDB view is a queryable object whose contents are defined by an aggregation pipeline on other collections or views. MongoDB does not persist the view contents to disk. A view's content is computed on-demand when a client queries the view. MongoDB can require clients to have permission to query the view. MongoDB does not support write operations against views.
	Aggregation Pipeline
The aggregation pipeline is a framework for data aggregation modeled on the concept of data processing pipelines. Documents enter a multi-stage pipeline that transforms the documents into aggregated results
Create View
To create or define a view:
•	Use the db.createCollection() method or the create command
Behavior
Views exhibit the following behavior:
Read Only
Views are read-only; write operations on views will error.
The following read operations can support views:
•	db.collection.find()
•	db.collection.findOne()
•	db.collection.aggregate()
•	db.collection.countDocuments()
•	db.collection.estimatedDocumentCount()
•	db.collection.count()
•	db.collection.distinct()
Index Use and Sort Operations
•	Views use the indexes of the underlying collection.
•	As the indexes are on the underlying collection, you cannot create, drop or re-build indexes on the view directly nor get a list of indexes on the view.
•	Starting in MongoDB 4.4, you can specify a $natural sort when running a find command on a view. Prior versions of MongoDB do not support $natural sort on views.
•	The view's underlying aggregation pipeline is subject to the 100 megabyte memory limit for blocking sort and blocking group operations. Starting in MongoDB 4.4, you can issue a find command with allowDiskUse: true on the view to allow MongoDB to use temporary files for blocking sort and group operations.
Prior to MongoDB 4.4, only the aggregate command accepted the allowDiskUse option.

Database Commands
All command documentation outlined below describes a command and its available parameters and provides a document template or prototype for each command. Some command documentation also includes the relevant mongo shell helpers.
To run a command against the current database, use db.runCommand():
db.runCommand( { <command> } )
To run an administrative command against the admin database, use db.adminCommand():
db.adminCommand( { <command> } )
Note
For details on specific commands, including syntax and examples, click on the specific command to go to its reference page.
User Commands
Aggregation Commands
Name	Description
aggregate
Performs aggregation tasks such as group using the aggregation framework.
count
Counts the number of documents in a collection or a view.
distinct
Displays the distinct values found for a specified key in a collection or a view.
mapReduce
Performs map-reduce aggregation for large data sets.

Geospatial Commands
Name	Description
geoSearch
Performs a geospatial query that uses MongoDB's haystack index functionality.
Query and Write Operation Commands
Name	Description
delete
Deletes one or more documents.
find
Selects documents in a collection or a view.
findAndModify
Returns and modifies a single document.
getLastError
Returns the success status of the last operation.
getMore
Returns batches of documents currently pointed to by the cursor.
insert
Inserts one or more documents.
resetError
Deprecated. Resets the last error status.
update
Updates one or more documents.
Query Plan Cache Commands
Name	Description
planCacheClear
Removes cached query plan(s) for a collection.
planCacheClearFilters
Clears index filter(s) for a collection.
planCacheListFilters
Lists the index filters for a collection.
planCacheSetFilter
Sets an index filter for a collection.
Database Operations
Authentication Commands
Name	Description
authenticate
Starts an authenticated session using a username and password.
getnonce
This is an internal command to generate a one-time password for authentication.
logout
Terminates the current authenticated session.
User Management Commands
Name	Description
createUser
Creates a new user.
dropAllUsersFromDatabase
Deletes all users associated with a database.
dropUser
Removes a single user.
grantRolesToUser
Grants a role and its privileges to a user.
revokeRolesFromUser
Removes a role from a user.
updateUser
Updates a user's data.
usersInfo
Returns information about the specified users.
Role Management Commands
Name	Description
createRole
Creates a role and specifies its privileges.
dropRole
Deletes the user-defined role.
dropAllRolesFromDatabase
Deletes all user-defined roles from a database.
grantPrivilegesToRole
Assigns privileges to a user-defined role.
grantRolesToRole
Specifies roles from which a user-defined role inherits privileges.
invalidateUserCache
Flushes the in-memory cache of user information, including credentials and roles.
revokePrivilegesFromRole
Removes the specified privileges from a user-defined role.
revokeRolesFromRole
Removes specified inherited roles from a user-defined role.
rolesInfo
Returns information for the specified role or roles.
updateRole
Updates a user-defined role.
Replication Commands
Name	Description
applyOps
Internal command that applies oplog entries to the current data set.

hello
Displays information about this member's role in the replica set, including whether it is the primary.
isMaster
Deprecated. Use hello instead.

replSetAbortPrimaryCatchUp
Forces the elected primary to abort sync (catch up) then complete the transition to primary.
replSetFreeze
Prevents the current member from seeking election as primary for a period of time.
replSetGetConfig
Returns the replica set's configuration object.
replSetGetStatus
Returns a document that reports on the status of the replica set.
replSetInitiate
Initializes a new replica set.
replSetMaintenance
Enables or disables a maintenance mode, which puts a secondary node in a RECOVERING state.
replSetReconfig
Applies a new configuration to an existing replica set.
replSetResizeOplog
Dynamically resizes the oplog for a replica set member. Available for WiredTiger storage engine only.
replSetStepDown
Forces the current primary to step down and become a secondary, forcing an election.
replSetSyncFrom
Explicitly override the default logic for selecting a member to replicate from.
Tip
See also: 
Replication for more information regarding replication.
Sharding Commands
Name	Description
addShard
Adds a shard to a sharded cluster.

addShardToZone
Associates a shard with a zone. Supports configuring zones in sharded clusters.
balancerCollectionStatus
Returns information on whether the chunks of a sharded collection are balanced.
New in version 4.4.
balancerStart
Starts a balancer thread.
balancerStatus
Returns information on the balancer status.
balancerStop
Stops the balancer thread.
checkShardingIndex
Internal command that validates index on shard key.
clearJumboFlag
Clears the jumbo flag for a chunk.
cleanupOrphaned
Removes orphaned data with shard key values outside of the ranges of the chunks owned by a shard.
enableSharding
Enables sharding on a specific database.
flushRouterConfig
Forces a mongod/mongos instance to update its cached routing metadata.
getShardMap
Internal command that reports on the state of a sharded cluster.
getShardVersion
Internal command that returns the config server version.

isdbgrid
Verifies that a process is a mongos.

listShards
Returns a list of configured shards.
medianKey
Deprecated internal command. See splitVector.

moveChunk
Internal command that migrates chunks between shards.
movePrimary
Reassigns the primary shard when removing a shard from a sharded cluster.
mergeChunks
Provides the ability to combine chunks on a single shard.
refineCollectionShardKey
Refines a collection's shard key by adding a suffix to the existing key.
New in version 4.4.
removeShard
Starts the process of removing a shard from a sharded cluster.
removeShardFromZone
Removes the association between a shard and a zone. Supports configuring zones in sharded clusters.

setShardVersion
Internal command to sets the config server version.

shardCollection
Enables the sharding functionality for a collection, allowing the collection to be sharded.
shardingState
Reports whether the mongod is a member of a sharded cluster.

split
Creates a new chunk.

splitChunk
Internal command to split chunk. Instead use the methods sh.splitFind() and sh.splitAt().

splitVector
Internal command that determines split points.
unsetSharding
Deprecated. Internal command that affects connections between instances in a MongoDB deployment.
updateZoneKeyRange
Adds or removes the association between a range of sharded data and a zone. Supports configuring zones in sharded clusters.

Tip
See also: 
Sharding for more information about MongoDB's sharding functionality.
Session Commands
Command	Description
abortTransaction
Abort transaction.
New in version 4.0.
commitTransaction
Commit transaction.
New in version 4.0.
endSessions
Expire sessions before the sessions' timeout period.
New in version 3.6.
killAllSessions
Kill all sessions.
New in version 3.6.
killAllSessionsByPattern
Kill all sessions that match the specified pattern
New in version 3.6.
killSessions
Kill specified sessions.
New in version 3.6.
refreshSessions
Refresh idle sessions.
New in version 3.6.
startSession
Starts a new session.
New in version 3.6.
Administration Commands
Name	Description
cloneCollectionAsCapped
Copies a non-capped collection as a new capped collection.

collMod
Add options to a collection or modify a view definition.
compact
Defragments a collection and rebuilds the indexes.
connPoolSync
Internal command to flush connection pool.
convertToCapped
Converts a non-capped collection to a capped collection.
create
Creates a collection or a view.
createIndexes
Builds one or more indexes for a collection.
currentOp
Returns a document that contains information on in-progress operations for the database instance.
drop
Removes the specified collection from the database.
dropDatabase
Removes the current database.
dropConnections
Drops outgoing connections to the specified list of hosts.
dropIndexes
Removes indexes from a collection.
filemd5
Returns the md5 hash for files stored using GridFS.

fsync
Flushes pending writes to the storage layer and locks the database to allow backups.
fsyncUnlock
Unlocks one fsync lock.
getDefaultRWConcern
Retrieves the global default read and write concern options for the deployment.
New in version 4.4.
getParameter
Retrieves configuration options.
killCursors
Kills the specified cursors for a collection.
killOp
Terminates an operation as specified by the operation ID.
listCollections
Returns a list of collections in the current database.
listDatabases
Returns a document that lists all databases and returns basic database statistics.
listIndexes
Lists all indexes for a collection.
logRotate
Rotates the MongoDB logs to prevent a single file from taking too much space.
reIndex
Rebuilds all indexes on a collection.
renameCollection
Changes the name of an existing collection.
setFeatureCompatibilityVersion
Enables or disables features that persist data that are backwards-incompatible.
setIndexCommitQuorum
Changes the minimum number of data-bearing members (i.e commit quorum), including the primary, that must vote to commit an in-progress index build before the primary marks those indexes as ready.
setParameter
Modifies configuration options.
setDefaultRWConcern
Sets the global default read and write concern options for the deployment.
New in version 4.4.
shutdown
Shuts down the mongod or mongos process.

Diagnostic Commands
Name	Description
availableQueryOptions
Internal command that reports on the capabilities of the current MongoDB instance.
buildInfo
Displays statistics about the MongoDB build.
collStats
Reports storage utilization statics for a specified collection.
connPoolStats
Reports statistics on the outgoing connections from this MongoDB instance to other MongoDB instances in the deployment.
connectionStatus
Reports the authentication state for the current connection.
cursorInfo
Removed in MongoDB 3.2. Replaced with metrics.cursor.

dataSize
Returns the data size for a range of data. For internal use.
dbHash
Returns hash value a database and its collections.
dbStats
Reports storage utilization statistics for the specified database.
driverOIDTest
Internal command that converts an ObjectId to a string to support tests.
explain
Returns information on the execution of various operations.
features
Reports on features available in the current MongoDB instance.
getCmdLineOpts
Returns a document with the run-time arguments to the MongoDB instance and their parsed options.
getLog
Returns recent log messages.
hostInfo
Returns data that reflects the underlying host system.
_isSelf
Internal command to support testing.
listCommands
Lists all database commands provided by the current mongod instance.

lockInfo
Internal command that returns information on locks that are currently being held or pending. Only available for mongod instances.

netstat
Internal command that reports on intra-deployment connectivity. Only available for mongos instances.

ping
Internal command that tests intra-deployment connectivity.
profile
Interface for the database profiler.

serverStatus
Returns a collection metrics on instance-wide resource utilization and status.
shardConnPoolStats
Deprecated in 4.4. Use connPoolStats instead.

top
Returns raw usage statistics for each database in the mongod instance.

validate
Internal command that scans for a collection's data and indexes for correctness.
whatsmyuri
Internal command that returns information on the current client.
Free Monitoring Commands
Name	Description
setFreeMonitoring
Enables/disables free monitoring during runtime.
Auditing Commands
Name	Description
logApplicationMessage
Posts a custom message to the audit log.
 

