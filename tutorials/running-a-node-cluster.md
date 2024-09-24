---
icon: circle-nodes
---

# Running a node cluster

{% hint style="warning" %}
Setting up and running clusters is for advanced users only.
{% endhint %}

A cluster is a group of machines that acts as a single node. One machine serves as the master, holding the node peerID, while the others function as slaves, providing additional computational power.

If you already possess a peerID in an advantageous prover ring position, clustering is an excellent strategy to scale up your operation.

### How to run a cluster?

Follow [this tutorial ](https://quilibrium.discourse.group/t/how-to-run-nodes-in-a-cluster/687/34)on the forum to learn how to run a cluster.

### **Notes**

* Clusters do not function in Windows WSL, but work effectively on Linux and Mac systems.
* Clusters have a soft cap of 2048 workers; adding more workers beyond this limit won't result in increased rewards.
* All machines in the cluster should have identical specifications. While it's technically possible to cluster different machines together, the slowest core will inevitably bottleneck the entire cluster's performance.
* The connection between machines must be robust. If you're renting machines, it's advisable to select ones within the same datacenter. However, some users report successful clustering of machines in different datacenters, provided the connection between them is strong.

#### PolySize

In plain English, "polySize" is the amount of work your node can do.

* If your cluster has more than 128 workers, to maximize the work you should go as high as 1024. \
  _You can run a number of workers between those 2 values, but the closer to 1024 the better performance you will have._
* If your cluster has more than 1024, you should go as high as 2048. \
  _You can run a number of workers between those 2 values, but the closer to 2048 the better performance you will have._
* If your cluster has more than 2048, adding more workers beyond this limit won't result in increased rewards, unless you do some complex manual configurations.

