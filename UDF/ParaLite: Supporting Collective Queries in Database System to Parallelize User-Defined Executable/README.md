# ParaLite: Supporting Collective Queries in Database System to Parallelize User-Defined Executable

## Abstract
This paper proposes extensions to parallel database
systems called collective queries and User-Defined eXecutables
(UDX). A collective query is an SQL query whose results are
distributed to multiple clients and then processed by them in
parallel, using arbitrary external programs (user-defined executables).
The intended applications are data intensive workflows,
typically built out of various independently developed
executables and scripts. Collective queries facilitate description
of such workflows by making data parallel execution of external
programs on big data easy and streamlined. It also provides
the workflow developers with a familiar and powerful language
SQL, for flexible data filtering and stereotypical data processing
tasks. We implement this concept in a system “ParaLite”, a
parallel database system based on a popular lightweight database
SQLite. It equips with data transfer optimization algorithms
that distribute query results to multiple clients, taking both
communication cost and compute loads into account. We verified
the correctness and performance of ParaLite and the experimental
results show that ParaLite has good performance on SQL
processing and achieves good scalability for the parallelization
of UDX.

[原文](http://pan.baidu.com/s/1eSp4ZKm)