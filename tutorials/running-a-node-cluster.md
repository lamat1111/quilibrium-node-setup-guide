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
* All machines in the cluster should have identical specifications. While it's technically possible to cluster different machines together, the slowest core will inevitably bottleneck the entire cluster's performance.
* The connection between machines must be robust. If you're renting machines, it's advisable to select ones within the same datacenter. However, some users report successful clustering of machines in different datacenters, provided the connection between them is strong.

#### PolySize

PolySize refers to the amount of work your node can perform.&#x20;

To optimize your cluster's performance, aim for a number of workers that is at least 128 or a power of two up to 2048. This means ideal worker counts are 128, 256, 512, 1024, or 2048.&#x20;

While your node will function with any number of workers, performance is enhanced when you approach these values.  It's important to note that if your cluster exceeds 2048 workers, increasing the count beyond this threshold won't lead to higher rewards unless you implement complex manual configurations.

<table data-card-size="large" data-column-title-hidden data-view="cards" data-full-width="false"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><strong>The Best Server Providers for your Nodes</strong></td><td>CLICK TO SEE THEM</td><td><a href="../best-server-providers.md">best-server-providers.md</a></td><td></td><td><a href="../.gitbook/assets/best-serve-providers-banner-text-1-1-B.jpg">best-serve-providers-banner-text-1-1-B.jpg</a></td></tr><tr><td><strong>Want to say thank you?</strong></td><td>CLICK TO DONATE</td><td><a href="../want-to-say-thank-you.md">want-to-say-thank-you.md</a></td><td></td><td><a href="../.gitbook/assets/donations-banner-text-1-1-B.jpg">donations-banner-text-1-1-B.jpg</a></td></tr></tbody></table>

