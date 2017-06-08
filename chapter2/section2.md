# Installing Hadoop

## Installing Horton Works Dataplatform (HDP)

Kylo supports both the Horton Works and Cloudera distributions of Hadoop. Horton work's distribution of Hadoop is called Horton Works Dataplatform, known as HDP. The quickest way to spin up the cluster is to use a piece of software called Ambari.

Ambari is an open source management platform for provisioning, managing, monitoring and securing Apache Hadoop Clusters. The software provides a simple web GUI for performing all these auctions. To use the product, we need to setup an Ambari server with a database and install the Ambari agents on the various servers in our cluster.

As we are using only a single server this is a very simple process as everything will be on one machine. If we wanted to add more machines to our cluster, we just need to add additional servers which have the Ambari agent configured.

### Installing Ambari

First we need to setup the Ambari repository to install the Ambari server package. SSH back to your machine and run the following command:

```
  wget http://public-repo-1.hortonworks.com/ambari/centos7/2.x/updates/2.5.1.0/ambari.repo -P /etc/yum.repos.d/
```

Now lets install The Ambari-server:

```
  yum install ambari-server
```
