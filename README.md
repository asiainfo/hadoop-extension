# Asiainfo Extensions of Apache Hadoop

All the codes in this project could be found in <http://github.com/asiainfo/hadoop-extension/>

This branch is based on CDH5.1.3
 
## Modification

###YARN-FairScheduler-Enhancement

####Description: 

This patch is aim to add a new feature which make a FSQueue bind to some specific nodes of cluster.

####Background:
	
In some product enviorment, not every nodes had the same network configuration and third-party library installed. 

So in some case of that, user wants to run some job on specific nodes of cluster.

####Design:

This patch create a new property to each pool(queue) which need to bind to specific some nodes of cluster. 

The application could use this queue to schedule their job.


####Example: 

fair-scheduler.xml:

    <resourceGroups>   
      <resourceGroup name="oracleClient">     
        <nodes>slave1,slave2<nodes>      
      </resourceGroup>
      <!-- 
        There would always be a resourceGroup named default, which use the all nodes on cluster. 
      --> 
    </resourceGroups> 
    <pool name="Queue2">   
      <minMaps>10</minMaps>   
      <minReduces>5</minReduces>   
      <resourceGroup>oracleClient</resourceGroup>   
      <maxRunningJobs>5</maxRunningJobs>   
      <weight>1.0</weight> 
    </pool> 
    <pool name="Queue1">   
      <minMaps>10</minMaps>   
      <minReduces>5</minReduces>
      <!-- default resourceGroup is ‘default’ -->   
      <maxRunningJobs>5</maxRunningJobs>   
      <weight>1.0</weight> 
    </pool>


