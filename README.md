Introduction
===
What is Cobra?
---
Cobra is semi-clairvoyant scheduling strategy deployed in Spark on YARN system. Jobs employing this strategy have competitive performance compared to the clairvoyant schedulers, and have substantial performance improvement (job response time) compared to the built-in algorithms.
![image](https://github.com/DislabNJU/Spark/blob/branch-2.0/oneslide.png)
Spark part in Cobra

The primary code of our changes is in ./core/src/main/scala/org/apache/spark/ExecutorAllocationManager.scala 

See the introduction of this work via [the papaer](https://github.com/DislabNJU/Spark/blob/branch-2.0/INFOCOM%20final%20version.pdf)
