# MonetDB/SQL Meets SkyServer: the Challenges of a Scientific Database

## Abstract
This paper presents our experiences in porting the
Sloan Digital Sky Survey(SDSS)/ SkyServer to the stateof-
the-art open source database system MonetDB/SQL.
SDSS acts as a well-documented benchmark for scientific
database management. We have achieved a fully
functional prototype for the personal SkyServer, to be
downloaded from our site. The lessons learned are 1)
the column store approach of MonetDB demonstrates
a great potential in the world of scientific databases.
However, the application also challenged the functionality
of our implementation and revealed that a fully
operational SQL environment is needed, e.g. including
persistent stored modules; 2) the initial performance is
competitive to the reference platform, MS SQL Server
2005, and 3) the analysis of SDSS query traces hints
at several techniques to boost performance by utilizing
repetitive behavior and zoom-in/zoom-out access patterns,
that are currently not captured by the system.

[原文](http://pan.baidu.com/s/1pKDsWn5)