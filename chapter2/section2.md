# Installing Hadoop

## Installing Horton Works Dataplatform (HDP)

Kylo supports both the Horton Works and Cloudera distributions of Hadoop. Horton work's distribution of Hadoop is called Horton Works Dataplatform, known as HDP. The quickest way to spin up the cluster is to use a piece of software called Ambari.

Ambari is an open source management platform for provisioning, managing, monitoring and securing Apache Hadoop Clusters. The software provides a simple web GUI for performing all these auctions. To use the product, we need to setup an Ambari server with a database and install the Ambari agents on the various servers in our cluster.

As we are using only a single server this is a very simple process as everything will be on one machine. If we wanted to add more machines to our cluster, we just need to add additional servers which have the Ambari agent configured.

### Installing Ambari Server

First we need to setup the Ambari repository to install the Ambari server package. SSH back to your machine and run the following command:

```
  wget http://public-repo-1.hortonworks.com/ambari/centos7/2.x/updates/2.5.1.0/ambari.repo -P /etc/yum.repos.d/
```

Now lets install The Ambari-server and the Ambari-agent:

```
  yum install ambari-server ambari-agent -y
```

After Ambari is installed, we need to configure it, so we will run the command ambari-server setup to start the wizard:

```
  ambari-server setup
```

This in execute the ambari-server setup wizard. My answers to the wizard were yes (disable Selinux temporarily), :

![Local Image](/images/ambari-server-setup-complete.png)

### Configure Ambari Agent

Once the Ambari agent RPM has been installed, the Ambari agent needs to be configured to point to the Ambari server. Edit the configuration file /etc/ambari-agent/conf/ambari-agent.ini and change the server hostname and port to match

```
[server]
hostname=localhost
url_port=8440
secured_url_port=8441
connect_retry_delay=10
max_reconnect_retry_delay=30
```

If your Ambari server is running on another machine (I.E your Kylo machine is an edge node), you will need to modify the hostname here or maybe your port if you changed it. Lets start the Ambari agent and enable it so it becomes active on boot:

```

```

### Install Hadoop Services
