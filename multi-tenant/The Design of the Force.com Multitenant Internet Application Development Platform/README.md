# The Design of the Force.com Multitenant Internet Application Development Platform.pdf
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

