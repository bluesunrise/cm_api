Cloudera Manager RESTful API Clients
====================================

NOTE This is a forked version of Cloudera API to include un-merged pull request, see:

https://github.com/cloudera/cm_api/pull/63/commits/76ef10e0834f67ab5f93169e4c8d56d14eb69993

The original fork is on branch cm5-5.14.0. This branch fixed resolves a newer version of Jackson dependency conflict, and is used by Cloudhub in GW7. The artifact is:

````
branch 5.14.0, artifact version 5.14.0-2018-02-13:

<dependency>
  <groupId>com.cloudera.api</groupId>
  <artifactId>cloudera-manager-api</artifactId>
  <version>5.14.0-2018-02-13</version>
</dependency>

````

The cm5-5.14.0 branch was then forked for Java8/GW8 into branch cm5-5.14.0-java8.

Additional patches were made to model classes to run JAXB on Java8. JAXB in Java8 behaves differently, which broke the unit tests in Cloudera.
IF I understand this, you have to use the variable passed into a list setter, for example:

````
 public void setMaintenanceOwners(List<ApiEntityType> maintenanceOwners) {
     this.maintenanceOwners = (null == maintenanceOwners)
                                ? new ArrayList<ApiEntityType>()
-                               : Lists.newArrayList(maintenanceOwners);
+                               : maintenanceOwners; // DST: Lists.newArrayList(maintenanceOwners);
   }
````

Patched the following files (and pom.xml):

````
branch cm5-5.14.0-java8:

	modified:   java/src/main/java/com/cloudera/api/model/ApiCluster.java
	modified:   java/src/main/java/com/cloudera/api/model/ApiHost.java
	modified:   java/src/main/java/com/cloudera/api/model/ApiRole.java
	modified:   java/src/main/java/com/cloudera/api/model/ApiService.java
	modified:   java/src/main/java/com/cloudera/api/model/ApiUser.java

<dependency>
  <groupId>com.cloudera.api</groupId>
  <artifactId>cloudera-manager-api</artifactId>
  <version>cm5-5.14.0-java8</version>
</dependency>

````

References to JAXB behavior changes from Java7 to Java8 documented here:

https://stackoverflow.com/questions/28536666/jaxb-fails-to-parse-xml-after-moving-to-java-8
https://stackoverflow.com/questions/36361075/difference-in-jaxb-java-7-versus-java-8
http://tonyz93.blogspot.com/2017/02/jaxb-diff-results-in-java7-and-java8.html#further
# seems the behavior changes in 2.3.0
https://mvnrepository.com/artifact/com.sun.xml.bind/jaxb-impl

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
