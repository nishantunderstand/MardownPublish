# Consumer Lag Growing to Millions 

Partition Skew (One Partition Become Hot Partition)
Consumer Process is Heavy Computational Logic
Consumer Poll is longer , Rebalancing Happen
Kafka Configuration is the Issue



# Messages Produced but Consumer Receives Nothing 

Wrong Offset 
Wrong Consumer Name
Longer Poll Time, Rebalancing 
No Partiton Assigned
Serialization / Deserialization Error


# Why Does Consumer Reprocess Old Messages After Restart?

OffSet Issue 

Autocommit Offset is Disable, Manual Commit is misisng 
OffSet Crashed Before Commit (Large Window Size)
LargeBatchSize + Commit at the end
Offset Commit is Inside try block and Exception Happen
Consumer Group Is Deleted



# Why One Consumer Is Overloaded While Others Are Idle?

Uneven key Distribution
One Partition is Hot Partition
We have more consumer than partition
Sticky Partition, Load keep coming to the same partition.


> One partition can be consumed by only one consumer at a time 👈👈👈👈👈
