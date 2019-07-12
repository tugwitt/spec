# Filesystem

the filesystem is where we actually store the data. at the end of the day, most base data storage techniques are some 
variation of a filesystem.

this will most likely look like a heirarchical filesystem of [.at files](http://liegroups.org/software/documentation/atlasofliegroups-docs/tutorial/video_1A/basics.html#the-basic-at-file)
that represent the underlying definition of the Lie group representation of the given dataset.

## Traditional Solutions

**[this](https://github.com/tugwitt/notes/blob/master/wiki/cs/dbms/DMBS-Overview.md) is a good primer on DBMS's**

### SQL Server

SQL Server uses data files as it's core data storage mechanism. [SQL Server Internals](https://www.red-gate.com/simple-talk/sql/database-administration/sql-server-storage-internals-101/)

>  A record, also known as a row, is the smallest storage structure in a SQL Server data file. Each row in a table is stored as an individual record on disk. Not only table data is stored as records, but also indexes, metadata, database boot structures and so forth. However, we’ll concentrate on only the most common and important record type, namely the data record, which shares the same format as the index record. 
