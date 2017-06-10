# Installing Kylo

Kylo is distributed as a Virtual Appliance and in RPM format. There is also a .deb Debian package release for those using a Debian based unix distribution. There are also plans for a .tar release if for some reason you don't want to use the package manager.

In this section we cover the basic installation of Kylo using the Kylo RPM and then cover how to build the Kylo RPM from source. Building the Kylo RPM can be useful for development, debugging and testing Kylo.

## Installing Kylo from RPM

The Kylo RPM can be obtained from the Kylo.io website. Generally the latest RPM can be found through the release notes here: (https://kylo.readthedocs.io/en/latest/release-notes/ReleaseNotes.html#latest)[https://kylo.readthedocs.io/en/latest/release-notes/ReleaseNotes.html#latest].

* Hopefully in the future these packages will served through an official yum repository with signed GPG keys for added security.

Finally,

## Building Kylo from Source

The Kylo package can be built from source using Maven. It is also possible to build Kylo using Maven with an IDE such as Intellij or Eclipse. For the purposes of this short book, we will build the RPM using Maven based on the job schedule run by Jenkins.

First we must install git and clone the Kylo repository:

```
  # Install git
  yum install -y git
```

Next, clone the Kylo repository in some location we can build from (like root home or ec2-user home):

```
  # Clone the kylo repo in ec2-user home, root home or some other dir.
  cd /home/ec2-user/
  git clone https://github.com/Teradata/kylo.git
```

Once the repo is closed we need to install and configure maven. Thankfully for us, Red Hat provides a supported maven package in the optional repository, so lets install it:

```
  # On CentOS, this might be available in EPEL, run yum install epel-release -y first
  yum install -y maven
```

Once installed, maven can be executed using the mvn command. Red Hat's package will most likely be older than the upstream maven release, which can be used instead.

Next we will attempt to build the kylo project. This is pretty easy:

```
  # cd into kylo directory, export options for maven, run the build command
  cd /home/ec2-user/kylo
  export MAVEN_OPTS="-Xms2g -Xmx4g"
  mvn clean install -DskipTests
```

Eventually you will end up with a message like this:

![Local Image](/images/mvn-build.PNG)
