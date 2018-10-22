## zk配置参数

参数  | 说明
------------- | -------------
clientPort  | the port to listen for client connections; that is, the port that clients attempt to connect to.
 dataDir | the location where ZooKeeper will store the in-memory database snapshots and, unless specified otherwise, the transaction log of updates to the database.
 tickTime | the length of a single tick, which is the basic time unit used by ZooKeeper, as measured in milliseconds. It is used to regulate heartbeats, and timeouts. For example, the minimum session timeout will be two ticks.
dataLogDir | This option will direct the machine to write the transaction log to the dataLogDir rather than the dataDir. This allows a dedicated log device to be used, and helps avoid competition between logging and snaphots.
 
 