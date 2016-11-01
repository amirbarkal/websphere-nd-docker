# Websphere Application Server Network Deployment 2-Node Cluster on Docker
# Written by Amir Barkal, inspired by [Dockerfiles for WebSphere Application Server traditional](https://github.com/WASdev/ci.docker.websphere-traditional)
======================================================================================================
## What is this?

This is a bunch of dockerfiles and docker-compose yaml files to get you started quickly with WebSphere Application Server Network Deployment cluster.
The purpose of this project is to easily create a 2 node cluster with a custom WAS profile, running on 3 Docker containers:
* Deployment Manager (dmgr)
* Custom node 1 running an application server (custom1)
* Custom node 2 running an application server (custom2)

NOTE: At the moment the cluster needs to be manually created from ISC, after the
  cell has been initialized.

## What is it good for?
Testing, demonstration, learning and POC. Witnessing the AWESOME power of Docker!

## Prerequisites:
* Git-Bash with Administrator privileges 
* Docker-tools with minimum engine version 1.12.0
* Docker Hub account with access to download the base nd image. (`docker login -u USERNAME -p PASSWORD`). Alternatively, you can build your own nd image [as per described here](https://github.com/WASdev/ci.docker.websphere-traditional/tree/master/network-deployment/install). Make sure you change the image name in the `FROM` block inside dmgr/Dockerfile and custom/Dockerfile to match the one you built. You will also need to update the `docker-compose.yml` file with your image names.

## How do I run it?
1. Clone this repo `https://github.com/amirbarkal/websphere-nd-docker.git`
2. Change to the repo dir `cd websphere-nd-docker`
3. Execute `docker-compose up -d`
4. Wait for it... (Can take up to 20 minutes depending on the speed of your internet connection and CPU)
   You can check containers status with `docker stats`. When CPU activity is around 0% your cluster is ready!

## How do I access it?
Open `http://DOCKER_HOST:9060/admin`
Security is off, so use whatever login name you like.

## How do I create the cluster?
Open ISC and enter random username. (i.e. `wasadmin`)


1. Go to `Servers >> Clusters >> WebSphere application server clusters >> New`
![Create the cluster](images/1.png)
2. Enter cluster name, keep default options and hit `Next`
![](images/2.png)
3. Add the first cluster member to node custom1, again keeping all default options and click `Next`
![](images/3.png)
4. Add the second cluster member to node custom2 and click `Add Member`
![](images/4.png)
5. Review the summary and hit `Finish`
![](images/5.png)
6. Click `Review`
![](images/6.png)
7. Make sure `Synchronize changes with Nodes` is selected and then click `Save`
![](images/7.png)
8. Wait for configuration synchronization to complete before clicking `OK`
![](images/8.png)
9. Start the cluster by selecting it from the list and hit `Start`
![](images/9.png)
10. Wait for the 2 application server JVMs to load. You can check their status in 
`Servers >> Server Types >> WebSphere application servers`
![](images/10.png)


## To Do:
* Automate cluster creation upon cell initialization

## Technical Details:

   + Current version level is:

     * IBM Java 7.1.30
     * Websphere Application Server ND 8.5.5 Fix Pack 9
     * Installation Manager 1.6.2

   + The following IBM part numbers and source files were used to construct the image:

     * 7.1.3.30-WS-IBMWASJAVA-part1.zip
     * 7.1.3.30-WS-IBMWASJAVA-part2.zip
     * (CIK2HML) WASND_v8.5.5_1of3.zip
     * (CIK2IML) WASND_v8.5.5_2of3.zip
     * (CIK2JML) WASND_v8.5.5_3of3.zip
     * (CIK2GML) Install_Mgr_v1.6.2_Lnx_WASv8.5.5.zip
     * 8.5.5-WS-WAS-FP0000009-part1.zip
     * 8.5.5-WS-WAS-FP0000009-part2.zip
