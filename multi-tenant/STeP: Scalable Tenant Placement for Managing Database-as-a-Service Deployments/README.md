#STeP: Scalable Tenant Placement for Managing Database-as-a-Service Deployments

##Abstract
　　Public cloud providers with Database-as-a-Service offerings
must efficiently allocate computing resources to each of their
customers. An effective assignment of tenants both reduces
the number of physical servers in use and meets customer
expectations at a price point that is competitive in the cloud
market. For public cloud vendors like Microsoft and Amazon,
this means packing millions of users’ databases onto
hundreds or thousands of servers.  
　　This paper studies tenant placement by examining a publicly
released dataset of anonymized customer resource usage
statistics from Microsoft’s Azure SQL Database production
system over a three-month period. We implemented the
STeP framework to ingest and analyze this large dataset.
STeP allowed us to use this production dataset to evaluate
several new algorithms for packing database tenants onto
servers. These techniques produce highly efficient packings
by collocating tenants with compatible resource usage patterns.
The evaluation shows that under a production-sourced
customer workload, these techniques are robust to variations
in the number of nodes, keeping performance objective violations
to a minimum even for high-density tenant packings.
In comparison to the algorithm used in production at the time
of data collection, our algorithms produce up to 90% fewer
performance objective violations and save up to 32% of total
operational costs for the cloud provider.

[源文件](http://pan.baidu.com/s/1csuN2A)