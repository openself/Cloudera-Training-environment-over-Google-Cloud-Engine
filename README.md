# Deploy a Free Cloudera training environment over Google Cloud Engine
Ideal guide for whom who wants to get familiar with Cloudera Hadoop distribution and would like to setup a cluster from scratch using the Google Cloude free subscription. <br/>
This is a study guide I made for the Cloudera Certified Administrator (CCA) that I am preparing. This is for test exam code CCA-131 (https://www.cloudera.com/more/training/certification/cca-admin.html). <br/>
I took the class offered from Cloudera and I used the O'Reilly book "Hadoop The Definitive Guide (4th edition)" to study. 
I also used the Cloudera support website documentation. The Apache Hadoop website is also a great site for even more documentation.
<br/><br/>

The following are the main steps I went through:
1. Open and configure a proper training VM environment on Google Cloud Engine
2. Install and configure Cloudera Manager and CDH
3. Perform basic and advanced configuration needed to effectively administer a Hadoop cluster
4. Maintain and modify the cluster to support day-to-day operations in the enterprise
5. Enable relevant services and configure the cluster to meet goals defined by security policy; demonstrate knowledge of basic security practices
6. Benchmark the cluster operational metrics, test system configuration for operation and efficiency
7. Demonstrate ability to find the root cause of a problem, optimize inefficient execution, and resolve resource contention scenarios
<br/><br/>

# Setup Google Cloud Engine environment
In this course, I will install Cloudera Manager and CDH (Cloudera Distribution including Apache Hadoop) on five virtual machines (VMs) running in the cloud (Google Cloud Engine), exploiting the free trial period (around 1 month). These are referred to as the “cluster VMs”. <br/>
All the VMs use the Centos 7 distribution and they have the following specifications: <br/>
  * lion: n1-standard-2 (2 vCPU, 7 GB memory)
  * elephant: n1-standard-1 (1 vCPU, 3.75 GB memory)
  * tiger: n1-standard-1 (1 vCPU, 3.75 GB memory)
  * horse: n1-standard-1 (1 vCPU, 3.75 GB memory)
  * monkey: n1-standard-1 (1 vCPU, 3.75 GB memory)
  
You should even add two firewall rules that, for simplicity, allows inbound and outbound traffic on all the ports. This can be done form the Google Cloud Engine Dashboard (Left menu -> Compute Engine -> VM instances -> select the VM you'd like -> Network -> default click and then customize your rules)<br/>

Once you get access to your VMs (both by private-public key or password) you should check that: 
  * the user you would like to launch Cloudera Manager Server and Agent is a sudoer user
  * you can use sudo as the user of the previous point without typing password. That users should have unlimited, passwordless sudo privileges
  * OS-level firewall is disabled or allows traffic on the ports Cloudera use
  * it is possible to ping from each machine to the others with the private IP address
  * it is possible to connect via ssh from each machine to the others using the private IP address
  * local DNS file should be properly set with the mapping between private IP and the FQDN (file is located at /etc/hosts)
  
# Install Cloudera Manager, CDH and Managed Services
The following steps illustrates the phases required to install Cloudera Manager and a Cloudera Manager 
deployment for CDH and managed services. Every single phase is required, but you can accomplish each phase in multiple ways. 
  1. *Install JDK: * JDK required by the Server, Management Services and CDH services. There exists two ways for installing it. The first is to install the oracle JDK during the Cloudera Manager installation wizard, the second is to manually install the same supported version of JDK on each host 
  2. *Set up DBs: * Database required by the Serverm Management Services and CDH services. However it is possible to install and configure PostreSQL packages by following the Cloudera Manager wizard (please take care that this solution can be done only in non-production environments)
  3. *Python installation: *it is requirement for Hue.
  4. Once all the three previous points have been satisfied it's time to install Cloudera Manager. I followed the instllation Path A (not recommended in a production environment), therefore I used a self-executing Cloudera Manager installation program to install Cloudera Manager Server and other packages. 
