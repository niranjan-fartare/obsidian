- Volume
- Velocity
- Variety
- Value
- Veracity

# Hadoop

- Solution for storing and processing data

## HDFS

- Hadoop Distributed File System
- Name / Primary Node -> Stores metadata of data
- Data / Core Node -> Stores data
- Follows, WORN -> Write Once Read N Times
### 7th Dec

## HDFS Commands

- hadoop fs -ls / -> Shows files from the cluster
- hadoop fs -mkdir /folder -> Create folder on Data Nodes
- hadoop fs -put file location -> Upload / Copy file in the Cluster
	- hadoop fs -put -f file location -> Overwrite file with same name
- hadoop fs -cat file -> Prints file contents 
- hadoop fs -copyFromLocal -> Copy from Local to Cluster
- hadoop fs -moveFromLocal -> Move from Local to Cluster
- hadoop fs -get hdfspath localpath -> Copy from Cluster to Local
	- hadoop fs -copyToLocal hdfspath localpath -> Copy from Cluster to Local
- hadoop  fs -getmerge hdfsfolder/* localpath -> Copy files from Cluster to Local and merge files
- hadoop fs -cp -> Copy files within Cluster
- hadoop fs -mv -> Move files within Cluster
- hadoop fs -rm -> Remove files
- hadoop fs -chmod -> Change permissions
- hadoop fs -rm -r -> Delete directory
- hadoop fs -du -> Disk Usage
- hadoop fs -df -> Disk Free
- hadoop fs -df -appendToFile -> Appends local file to a file in Cluster
- hadoop fs -expunge -> Deleted trashed files
- hadoop dfsadmin -report -> Cluster status

- Name Node Safe Mode -> Read Only mode 
	- Checks health of the nodes
	- hdfs dfsadmin -safemode get -> Current safe mode status
	- hdfs dfsadmin -safemode enter -> Turn on safe mode
	- hdfs dfsadmin -safemode leave -> Turn off safe mode
- hdfs dfs -touchz file -> Create empty file in the Cluster
- hadoop fs jar jar_file input output_folder(Create Automatically) -> Run Jar file which contains map reduce logic.

