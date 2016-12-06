# DAX: A Widely Distributed Multi-tenant Storage Service for DBMS Hosting

## ABSTRACT
　　Many applications hosted on the cloud have sophisticated
data management needs that are best served by a SQL-based
relational DBMS. It is not dificult to run a DBMS in the
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
exploit exible consistency.

## INTRODUCTION
　　In this paper we present a storage service that is intended
to support cloud-hosted, data-centric applications. There is
a wide variety of cloud data management systems that such
applications can use to manage their persistent data. At
one extreme are so-called NoSQL database systems, such as
BigTable [7] and Cassandra [20]. These systems are scalable
and highly available, but their functionality is limited. They
typically provide simple key-based, record-level, read/write interfaces and limited (or no) support for application-dened transactions. Applications that use such systems directly
must either tolerate or work around these limitations.  
　　At the other extreme, applications can store their data
using cloud-hosted relational database management systems
(DBMS). For example, clients of infrastructure-as-a-service
providers, such as Amazon, can deploy DBMS in virtual
machines and use these to provide database management
services for their applications. Alternatively, applications
can use services such as Amazon's RDS or Microsoft SQL
Azure [4] in a similar way. This approach is best suited
to applications that can be supported by a single DBMS
instance, or that can be sharded across multiple independent
DBMS instances. High availability is also an issue, as
the DBMS represents a single point of failure { a problem
typically addressed using DBMS-level high availability techniques.
Despite these limitations, this approach is widely
used because it puts all of the well-understood benets of
relational DBMS, such as SQL query processing and transaction
support, in service of the application. This is the
approach we focus on in this paper.  
　　A cloud-hosted DBMS must have some means of persistently
storing its database. One approach is to use a persistent
storage service provided within the cloud and accessed
over the network by the DBMS. An example of this is Amazon's
Elastic Block Service (EBS), which provides networkaccessible
persistent storage volumes that can be attached
to virtual machines.  
　　In this paper, we present a back-end storage service
called DAX, for Distributed Application-controlled Consistent
Store, that is intended to provide network-accessible
persistent storage for hosted DBMS tenants. Each DBMS
tenant, in turn, supports one or more applications. This
architecture is illustrated in Figure 1. We have several objectives for DAX's design that set it apart from other distributed
storage services:  
　　scalable tenancy: DAX must accommodate the aggregate
storage demand (space and bandwidth) of all of
its DBMS tenants, and it should be able to scale out to accommodate
additional tenants or to meet growing demand
from existing tenants. Our focus is on scaling out the
storage tier to accommodate more tenants, not on scaling
out individual DBMS tenants. A substantial amount
of previous research has considered techniques for scaling
out DBMS [12, 14, 22] and techniques like sharding [15]
are widely used in practice. These techniques can also be
used to scale individual hosted DBMS running on DAX.
Furthermore, while DBMS scale-out is clearly an important
issue, current trends in server hardware and software
are making it more likely that an application can be supported
by a single DBMS instance, with no need for scale
out. For example, it is possible at the time of this writing
to rent a virtual machine in Amazon's EC2 with 68 GB of
main memory and 8 CPU cores, and physical servers with
1 TB of main memory and 32 or more cores are becoming
commonplace. While such powerful servers reduce the
need for elastic DBMS scale-out, we still need a scalable
and resilient storage tier, which we provide with DAX.  
 high availability and disaster tolerance: We expect
the storage service provided by DAX to remain available
despite failures of DAX servers (high availability),
and even in the face of the loss of entire data centers
(disaster tolerance). To achieve this, DAX replicates data
across multiple geographically distributed data centers. If
a DBMS tenant fails, DAX ensures that the DBMS can be
restarted either in the same data center or in a dierent
data center. The tenant may be unavailable to its applications
while it recovers, but DAX will ensure that no
durable updates are lost. Thus, DAX ooads part of the
work of protecting a tenant DBMS from the eects of failures.
It provides highly available and widely distributed
access to the stored database, but leaves the task of ensuring
that the database service remains available to the
hosted DBMS.  
 consistency: DAX should be able to host legacy
DBMS tenants, which expect to be provided with a consistent
view of the underlying stored database. Thus, DAX
must provide suciently strong consistency guarantees to
its tenants.  
 DBMS specialization: DAX assumes that its clients
have DBMS-like properties. We discuss these assumptions
further in Section 2.  
　　A common way to build strongly consistent highly available
data stores is through the use of synchronous masterslave
replication. However, such systems are dicult to distribute
over wide areas. Therefore, we have instead based
DAX on multi-master replication and Dynamo-style 
exible consistency [16]. Flexible consistency means that clients
(in our case, the DBMS tenants) can perform either fast
read operations for which the storage system can provide
only weak consistency guarantees or slower read operations
with strong consistency guarantees. Similarly, clients can
perform fast writes with weak durability guarantees, or relatively
slow writes with stronger guarantees. As we show
in Section 3, these performance/consistency and performance/
durability tradeos can be substantial, especially in
widely distributed systems. DAX controls these trade-os
automatically on behalf of its DBMS tenants. Its goal is
to approach the performance of the fast weakly consistent
(or weakly durable) operations, while still providing strong
guarantees to the tenants. It does this in part by taking advantage
of the specic nature of the workload for which it is
targeted, e.g., the fact that each piece of stored data is used
by only one tenant.  
　　This paper makes several research contributions. First,
we present a technique called optimistic I/O, which controls
the consistency of the storage operations issued by the
DBMS tenants. Optimistic I/O aims to achieve performance
approaching that of fast weakly consistent operations while
ensuring that the DBMS tenant sees a suciently consistent
view of storage.  
　　Second, we describe DAX's use of client-controlled syn-
chronization. Client-controlled synchronization allows DAX
to defer making guarantees about the durability of updates
until the DBMS tenant indicates that a guarantee is required.
This allows DAX to hide some of the latency associated
with updating replicated data. While client-controlled
synchronization could potentially be used by other types
of tenants, it is a natural t with DBMS tenants, which
carefully control update durability in order to implement
database transactions.    
　　Third, we dene a consistency model for DAX that accounts
for the presence of explicit, DBMS-controlled synchronization
points. The model denes the consistency
requirements that a storage system needs to guarantee to
ensure correct operation when a DBMS fails and is restarted
after the failure (possible in a dierent data center).  
Finally, we present an evaluation of the performance of
DAX running in Amazon's EC2 cloud. We demonstrate its
scalability and availability using TPC-C workloads, and we
also measure the eectiveness of optimistic I/O and clientcontrolled
synchronization.

[源文件](http://pan.baidu.com/s/1eRQ2tyi)