# Filesystem

the filesystem is where we actually store the data. at the end of the day, most base data storage techniques are some 
variation of a filesystem.

this will most likely look like a heirarchical filesystem of [.at files](http://liegroups.org/software/documentation/atlasofliegroups-docs/tutorial/video_1A/basics.html#the-basic-at-file)
that represent the underlying definition of the Lie group representation of the given dataset.

realistically, we could allow for variable backends on the storage aspect as well. as much as i hate it, BSV is the most
realistic option, but we could say anything; custom Azure Blob/AWS EFS, bitcoin, eth, twitter. our filesystem is just a 
heirarchical model representation of data. if we maintain that heirarchical model (i.e. maintain it through a symbololic heirarchical tree of the tx hashes [lol]), then there really isn't a difference to us; if we can rebuild the General Lie Group and maintain isomorphism, the system doesn't care how the data is given. 

## Traditional Solutions

**[this](https://github.com/tugwitt/notes/blob/master/wiki/cs/dbms/DMBS-Overview.md) is a good primer on DBMS's**

### SQL Server

SQL Server uses data files as it's core data storage mechanism. [SQL Server Internals](https://www.red-gate.com/simple-talk/sql/database-administration/sql-server-storage-internals-101/)

#### Records

>  A record, also known as a row, is the smallest storage structure in a SQL Server data file. Each row in a table is stored as an individual record on disk. Not only table data is stored as records, but also indexes, metadata, database boot structures and so forth. However, we’ll concentrate on only the most common and important record type, namely the data record, which shares the same format as the index record. 

![SQL Server Record](https://www.red-gate.com/simple-talk/wp-content/uploads/imported/1880-cc374fe5-65c7-449c-86f6-7b481eb256bd.png)

#### Pages

>  Theoretically, SQL Server could just store a billion records side by side in a huge data file, but that would be a mess to manage. Instead, it organizes and stores records in smaller units of data, known as pages. Pages are also the smallest units of data that SQL Server will cache in memory (handled by the buffer manager). 

![SQL Server Page](https://www.red-gate.com/simple-talk/wp-content/uploads/imported/1880-585f878a-dea2-448c-929c-9ea86d2d7ea4.png)

#### Heaps

>  Heaps are the simplest data structures, in that they’re just “a big bunch of pages,” all owned by the same object. A special type of page called an index allocation map (IAM) tracks which pages belong to which object. SQL Server uses IAM pages for heaps and indexes, but they’re especially important for heaps as they’re the only mechanism for finding the pages containing the heap data. 

#### Indexes

>  Structurally, non-clustered and clustered indexes are the same. Both store index pages in a structure known as a b-tree. However, while a non-clustered index stores only the b-tree structure with the index key values and pointers to the data rows, a clustered index stores both the b-tree, with the keys, and the actual row data at the leaf level of the b-tree. As such, each table can have only one clustered index, since the data can only be stored in one location, but many non-clustered indexes that point to the base data. With non-clustered indexes, we can include copies of the data for certain columns, for example so that we can read frequently accessed columns without touching the base data, while either ignoring the remaining columns or following the index pointer to where the rest of the data is stored. 

![SQL Server B Tree](https://www.red-gate.com/simple-talk/wp-content/uploads/imported/1880-d5560ef5-2a99-4a58-ad36-bab3624b1168.png)


