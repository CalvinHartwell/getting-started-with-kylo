# Chapter 2, Section 1: Installing Kylo, NiFI and HDP

### Running Kylo

The easiest way to use Kylo is through the pre-built virtual appliance (sandbox) which can be downloaded on the Kylo.io website. The sandbox includes an installation of Horton Work's Hadoop platform (HDP) and Kylo on CentOS 7. This can be useful for testing, development and demonstration purposes but does not provide a production environment.

Kylo should usually be installed on an edge node within a big data environment. This means it access things like Hive and Spark without having much of an impact on the system. Different parts of software required by Kylo can be moved to other servers if they prove to be a bottle neck, such as the database it uses.

This section covers the installation of Kylo, NiFI and HDP on a new machine to form an all-in-one machine similar to the sandbox from the ground up. Of course, this machine could be a cluster with hundreds of machines. As long as the machine running Kylo has access to the correct Hadoop services it will work fine.

### Preliminary Requirements

We will be using AWS to build this test setup. In theory, you can use a physical server, another cloud provider, or even Virtual Box/KVM/Xen/etc to build the machine as well. Here are the requirements for the machine:

- At least 8 GB of RAM
- At least 2 cores
- At least 25 Gigabytes of storage
- One Network Interface with a public IP address attached*

Note that the machine can be made to work with less resources but the recommendations here will work well.

* The use of a public IP address is dangerous as it exposes the machine to the whole of the web. If we open up the port to Ambari Depending on your VPC setup, you might not want to do this at all as it could expose your company's internal network to the internet (for example, if you're using AWS Direct Connect). Preferably the use of a VPN would be better: [Amazon VPN Connections](http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/vpn-connections.html).

## Provision the Machine

- First log into AWS (aws.amazon.com), if you don't have an account, create one. Once in, go to Services and find EC2. Once inside EC2 Dashboard, go to Launch Instance.

- Inside Launch Instance, select Red Hat Enterprise Linux 7.3 (specifically Red Hat Enterprise Linux 7.3 (HVM), SSD Volume Type - ami-9c363cf8). If you're reading this in the future, the version has most likely changed, so just pick the latest Red Hat Enterprise Linux (HVM) image.

- On the next screen, select the instance type. I used t2.large, which has two vCPU and 8 GiB of memory. Using the t2.medium instance would also suffice.

- On the next screen we can set some more instance details such as subnet, network and monitoring. The most useful option for us on this screen is to enable protection against accidental termination. We don't need to change any other details at this point so hit next to add storage.

- I recommend changing the default disk size to at least 25 GiB, but you might want to go a little higher, to say, 40 GiB or more if you actually plan to ingest data sets on this machine.

- You can either hit the next tab to add some metadata (called tags) for the instance or you can now hit review and launch.

- The machine will now boot. However, we have not defined any security groups, so we cannot access it yet.

# Defining Security Groups for HDP and Kylo

By default in AWS, all ports are blocked/closed to virtual machines. Security groups must be used to open up connectivity to virtual machines on a port-by-port basis, just like regular firewalls. You can either add all your required ports into a single security or split them into individual groups which can be combined together.

Virtual machines can use multiple security groups at once. For example, I may create a group for ssh (which contains 443) and HTTP (which contains 80 and maybe 8443). If the machine is given the SSH group it will just have 443, but if the other is added, all three ports 443, 80 and 8443 will be opened up.

- First log into AWS (aws.amazon.com), if you don't have an account, create one. Once in, go to Services and find EC2. Once inside EC2 Dashboard, go to Network and Security and then Security Groups.

- You will need to create either a single security group or multiple groups. Give the new group a name and a description, the list of ports we need to open are below:

| Service          | Port |
|------------------|------|
| SSH              | 443  |
| Kylo-UI          | 8400 |
| Ambari GUI       | 8080 |
| Ambari Handshake | 8440 |
| Ambari Heartbeat | 8441 |

- On the Create security group form, you will want to add new in-bound rules for each port, selecting the Type as Custom TCP. You can limit the Source to your own IP address OR set the source to any ip address. As previously mentioned, this is a security risk.

- There are additional Ambari and Kylo ports defined in the manuals which can be opened as required.

# 
