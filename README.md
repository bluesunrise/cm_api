Cloudera Manager RESTful API Clients
====================================
see branch: cm5-5.14.0
that branch contains patch for

ApiObjectMapper.java to use newer version 2.7.2 of Jackson to be compatible with Azure dependencies. There is an outstanding pull request unprocessed 

 https://github.com/cloudera/cm_api/pull/63/commits/76ef10e0834f67ab5f93169e4c8d56d14eb69993"


> [Cloudera Manager](http://www.cloudera.com/products-services/tools/) is the market-leading management platform 
> for [CDH](http://www.cloudera.com/hadoop/). As the industry’s first end-to-end 
> management application for Apache Hadoop, Cloudera Manager sets the standard for enterprise deployment by 
> delivering granular visibility into and control over every part of CDH – empowering operators to improve 
> cluster performance, enhance quality of service, increase compliance and reduce administrative costs.

This project contains all the source, examples and documentation 
you need to easily build a [Cloudera Manager](http://www.cloudera.com/products-services/tools/) client in 
[Java](java) or [Python](python).

All source in this repository is [Apache-Licensed](LICENSE.txt).

This client code allows you to interact with Cloudera Manager to:
* Manage multiple clusters
* Start and stop all or individual services or roles
* Upgrade services running on your cluster
* Access time-series data on resource utilitization for any activity in the system
* Read logs for all processes in the system as well as stdout and stderr
* Programmatically configure all aspects of your deployment
* Collect diagnostic data to aid in debugging issues
* Run distributed commands to manage auto-failover, host decommissioning and more
* View all events and alerts that have occurred in the system
* Add and remove users from the system
