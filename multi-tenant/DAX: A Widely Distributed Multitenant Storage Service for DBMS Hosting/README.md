#DAX: A Widely Distributed Multi-tenant Storage Service for DBMS Hosting

## ABSTRACT
Many applications hosted on the cloud have sophisticated
data management needs that are best served by a SQL-based
relational DBMS. It is not dicult to run a DBMS in the
cloud, and in many cases one DBMS instance is enough to
support an application's workload. However, a DBMS running
in the cloud (or even on a local server) still needs a
way to persistently store its data and protect it against failures.
One way to achieve this is to provide a scalable and
reliable storage service that the DBMS can access over a
network. This paper describes such a service, which we call
DAX. DAX relies on multi-master replication and Dynamostyle

exible consistency, which enables it to run in multiple
data centers and hence be disaster tolerant. Flexible
consistency allows DAX to control the consistency level of
each read or write operation, choosing between strong consistency
at the cost of high latency or weak consistency with
low latency. DAX makes this choice for each read or write
operation by applying protocols that we designed based on
the storage tier usage characteristics of database systems.
With these protocols, DAX provides a storage service that
can host multiple DBMS tenants, scaling with the number
of tenants and the required storage capacity and bandwidth.
DAX also provides high availability and disaster tolerance
for the DBMS storage tier. Experiments using the TPC-C
benchmark show that DAX provides up to a factor of 4 performance
improvement over baseline solutions that do not
exploit 
exible consistency.

## INTRODUCTION
　　In this paper we present a storage service that is intended
to support cloud-hosted, data-centric applications. There is
a wide variety of cloud data management systems that such
applications can use to manage their persistent data. At
one extreme are so-called NoSQL database systems, such as
BigTable [7] and Cassandra [20]. These systems are scalable
and highly available, but their functionality is limited. They
typically provide simple key-based, record-level, read/write