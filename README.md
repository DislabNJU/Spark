Introduction
===
What is Cobra?
---
Cobra is semi-clairvoyant scheduling strategy deployed in Spark on YARN system. Jobs employing this strategy have competitive performance compared to the clairvoyant schedulers, and have substantial performance improvement (job response time) compared to the built-in algorithms in the online average setting. 
The blew figure is an one-slide overview. See the detailed introduction via the [paper](https://github.com/DislabNJU/Spark/blob/branch-2.0/INFOCOM%20final%20version.pdf).
![Architecture](https://github.com/DislabNJU/Spark/blob/branch-2.0/oneslide.png)

### What is semi-clairvoyance?
Semi-clairvoyance means the the task scheduler in the job only has partitial knowledge of future characteristics, as contrary to the complete prior knowledge of the job structure. The semi-clairvoyance assumption is more practical, and it captures the key universally useful information of all-kind applications. Specifially, the only available information includes resource requirements and processing times of tasks in available stages.

How Cobra works?
===
As shown in the green rectangle in the above figure, three cases are classified where the job could request more resources, or maintain current resources, or release some resources. The decision is made according to the resource utilization and the presence of waiting tasks.
By how much a job's resources fluctuating depends on the parameter $\rho$.

The primary code of our changes is in ./core/src/main/scala/org/apache/spark/ExecutorAllocationManager.scala 
