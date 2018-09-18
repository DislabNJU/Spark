Introduction
===
What is Cobra?
---
Cobra is semi-clairvoyant scheduling strategy deployed in Spark on YARN system. Jobs employing this strategy have competitive performance compared to the clairvoyant schedulers, and have substantial performance improvement (job response time) compared to the built-in algorithms in the online average setting. 
The blew figure is an one-slide overview. See the detailed introduction via the [paper](https://github.com/DislabNJU/Spark/blob/branch-2.0/INFOCOM%20final%20version.pdf).
<img width="650" src="https://github.com/DislabNJU/Spark/blob/branch-2.0/oneslide.png"/>
### What is semi-clairvoyance?
Semi-clairvoyance means the the task scheduler in the job only has partitial knowledge of future characteristics, as contrary to the complete prior knowledge of the job structure. The semi-clairvoyance assumption is more practical, and it captures the key universally useful information of all-kind applications. Specifially, the only available information includes resource requirements and processing times of tasks in available stages.

How Cobra works?
===
As shown in the green rectangle in the above figure, three cases are classified where the job could request more resources, or maintain current resources, or release some resources. The decision is made according to the resource utilization and the presence of waiting tasks.
By how much a job's resources fluctuating depends on the parameter $\rho$.

As mentioned, current implementation is carried in Spark on YARN system. The purple rectangle parts in the above figure is new. In Spark, we implement the Af and Pdelay algorithms. The detailed components and how they interact with the original ones can be shown in the below figure. The primary code of our changes is in [this](https://github.com/DislabNJU/Spark/blob/branch-2.0/core/src/main/scala/org/apache/spark/ExecutorAllocationManager.scala).

<img width="550" src="https://github.com/DislabNJU/Spark/blob/branch-2.0/architecture-detail.png"/>

While in YARN, we implement the monitor component which keeps watching on the container's utilization and reporting to its task scheduler. The primary code of our changes is in [this](https://github.com/DislabNJU/Hadoop/blob/master/hadoop-yarn-project/hadoop-yarn/hadoop-yarn-server/hadoop-yarn-server-nodemanager/src/main/java/org/apache/hadoop/yarn/server/nodemanager/containermanager/monitor/ContainersMonitorImpl.java) and its associated APIs. 
