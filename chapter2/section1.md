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

- First log into AWS (aws.amazon.com), if you don't have an account, create one.

- Once in, go to Services and find EC2. Once inside EC2 Dashboard, go to Launch Instance.

- Inside Launch Instance, select Red Hat Enterprise Linux 7.3 (specifically Red Hat Enterprise Linux 7.3 (HVM), SSD Volume Type - ami-9c363cf8). If you're reading this in the future, the version has most likely changed, so just pick the latest Red Hat Enterprise Linux (HVM) image.

- On the next screen, select the instance type. I used t2.large, which has two vCPU and 8 GiB of memory. Using the t2.medium instance would also suffice.

- 
