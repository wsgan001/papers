# The Design of the Force.com Multitenant Internet Application Development Platform
## ABSTRACT
Force.com is the preeminent on-demand application development platform in use today, supporting some 55,000+ organizations. Individual enterprises and commercial software-as-a-service (SaaS)
vendors trust the platform to deliver robust, reliable, Internet-scale applications. To meet the extreme demands of its large user population, Force.com’s foundation is a metadata-driven software

architecture that enables multitenant applications.   
The focus of this paper is multitenancy, a fundamental design approach that can dramatically improve SaaS application management. This paper defines multitenancy, explains its benefits, and demonstrates why metadata-driven architectures are the premier choice for implementing multitenancy.

------
这篇论文的核心是多租户机制，多租户是一种可以显著地提高SaaS应用管理功能的方法。这篇论文详述了多租户，解释了它的优点并证明了为什么元数据驱动的架构是实现多租户机制优先选择。

## INTRODUCTION
History has shown that every so often, incremental advances in technology and changes in business models create major paradigm shifts in the way software applications are designed, built, and
delivered to end users. Today, reliable broadband Internet access, service-oriented architectures (SOAs), and the cost inefficiencies of managing dedicated on-premise applications are driving a transition toward the delivery of managed, shared, Web-based services called software as a service (SaaS).

## CONCLUSION
Platform as a service (PaaS) and software as a service (SaaS) are
contemporary software application development and delivery
models that an increasing number of organizations are using to
improve their time to market, reduce capital expenditures, and
improve overall competitiveness in a challenging global economy.
Internet-based, shared computing platforms are attractive because
they let businesses quickly access hosted, managed software assets
on demand and avoid the costs and complexity associated with the
purchase, installation, configuration, and ongoing maintenance of an
on-premises data center.   

The most successful on-demand SaaS/PaaS company is
salesforce.com. The company developed the Force.com platform
whose metadata-driven architecture enables anyone to efficiently
build and deliver sophisticated, customizable, mission-critical,
Internet-scale multitenant applications. Using standards-based Web
service APIs and native platform development tools, Force.com
developers can easily build all components of a Web-based
application, including the data model, user interface, business logic,
integrations with other applications, and more.

Over the past 10 years, salesforce.com engineers have optimized all
layers of the Force.com platform for multitenancy, with features that
let the platform deliver unprecedented Internet scalability to the
height of 170 million transactions daily. Platform features such as
the bulk data processing API, the Apex programming language, an
external full-text search engine, and its unique query optimizer help
make multitenant platform applications highly efficient and scalable
with little or no thought from developers.

Salesforce.com’s managed approach for the deployment of
production applications ensures top-notch performance, scalability,
and reliability for all dependent applications. Additionally,
salesforce.com continually monitors and gathers operational
information from Force.com applications to help drive incremental
improvements and new platform features that immediately benefit
existing and new applications.

