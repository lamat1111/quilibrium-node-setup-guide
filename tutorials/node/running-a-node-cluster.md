---
icon: circle-nodes
---

# Running a node cluster

{% hint style="warning" %}
Setting up and running clusters is for advanced users only.
{% endhint %}

A cluster is a group of machines that acts as a single node. One machine serves as the master, holding the node peerID, while the others function as slaves, providing additional computational power.

If you already possess a peerID in an advantageous prover ring position, clustering is an excellent strategy to scale up your operation.

<table data-card-size="large" data-column-title-hidden data-view="cards" data-full-width="false"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><strong>The Best Server Providers for your Nodes</strong></td><td>CLICK TO SEE THEM</td><td><a href="../../best-server-providers.md">best-server-providers.md</a></td><td></td><td><a href="../../.gitbook/assets/best-serve-providers-banner-text-1-1-B.jpg">best-serve-providers-banner-text-1-1-B.jpg</a></td></tr><tr><td><strong>Want to say thank you?</strong></td><td>CLICK TO DONATE</td><td><a href="../../want-to-say-thank-you.md">want-to-say-thank-you.md</a></td><td></td><td><a href="../../.gitbook/assets/donations-banner-text-1-1-B.jpg">donations-banner-text-1-1-B.jpg</a></td></tr></tbody></table>

## How to run nodes in a cluster

{% hint style="info" %}
Tutorial by Tyga. You can find it on the [forum](https://quilibrium.discourse.group/t/how-to-run-nodes-in-a-cluster/687), along with several FAQs
{% endhint %}

#### Terminology

* **Default:** the default way to run a node-- not manually setting data workers
* **Cluster:** a grouped set of servers that utilize the a central peerId/config, or in other words control process, by manually defining and running data workers across each server defined in that config file
* **Control Process:** the process that controls the data worker processes
* **Data Worker Process:** a process in which does all the heavy lifting for proving and computation

#### Notes

* Clusters do not function in Windows WSL, but work effectively on Linux and Mac systems.
* All machines in the cluster should have identical specifications. While it's technically possible to cluster different machines together, the slowest core will inevitably bottleneck the entire cluster's performance.
* The connection between machines must be robust. If you're renting machines, it's advisable to select ones within the same datacenter. However, some users report successful clustering of machines in different datacenters, provided the connection between them is strong.

#### PolySize

PolySize refers to the amount of work your node can perform.&#x20;

To optimize your cluster's performance, aim for a number of workers that is close to these values 128, 1024, 2048.

While your node will function with any number of workers, performance is enhanced when you approach these values, and it will be reduced if you have a value that is closer to the lower count (e.g. 127 workers should perform better than 129). \
Above 2048 workers, the performance will lower drastically.

### Assuming 2 Machines/Servers in a Cluster <a href="#p-1297-assuming-2-machinesservers-in-a-cluster-2" id="p-1297-assuming-2-machinesservers-in-a-cluster-2"></a>

You have at least 2 machines that are on the same network:

* Machine A
  * Internal IP address: 192.168.0.200
  * 4 cores
* Machine B
  * Internal IP address: 192.168.0.201
  * 4 cores

You want to run as many cores as possible using PeerId Qmabc123.

You will need a dedicated core for for controlling the data workers, so this means that you only have 7 available cores for data workers.

### Set-up on each machine for Config <a href="#p-1297-set-up-on-each-machine-for-config-3" id="p-1297-set-up-on-each-machine-for-config-3"></a>

You don’t need to copy your keys or store, but you will need to have a .config directory with at least the config.yml file for getting the data worker process running.

* For the machine with the control process: you need the whole .config directory per usual, with keys.yml, store directory, etc.
* For the machines with only data workers: you **ONLY** need the .config directory with **only** the config.yml file in it.

#### .config Directory placement <a href="#p-1297-config-directory-placement-4" id="p-1297-config-directory-placement-4"></a>

You can either place the `.config` directory in the default place (ceremonyclient/node/.config) or you can place it anywhere and when starting your processes to use the `--config /location/of/.config/dir` parameter.

#### Reasoning for this <a href="#p-1297-reasoning-for-this-5" id="p-1297-reasoning-for-this-5"></a>

As noted below in the “Further Thoughts” section, Cassie mentions:

> … the \[data worker ports] are not inherently secured by any authorization, so if you leave a data worker open, anyone can send it prover tasks (and thus earn rewards from it).

This would imply you don’t need the keys or store file on the data worker-only machines, just networked that only you can connect to the data workers with your control process.

As far as I can tell, the reasons the config is required is because the startup process will generate one if not found to use the defaults found there after it loads it into the application, as well as for defining the RPC Multiaddr for the data worker for this core.

### Modifying the .config/config.yml file <a href="#p-1297-modifying-the-configconfigyml-file-6" id="p-1297-modifying-the-configconfigyml-file-6"></a>

So find the ./config/config.yml file for that Peer ID and modify the `.engine.dataWorkerMultiaddrs` array to include workers from each machine.

#### Relevant YAML syntax notation <a href="#p-1297-relevant-yaml-syntax-notation-7" id="p-1297-relevant-yaml-syntax-notation-7"></a>

The config files are written in YAML, so learning a bit of YAML to be able to modify your config files yourself would be recommended. For the tutorials sake, as there are a lot of beginners, I will cover the relevant syntax to get you through this tutorial.

**YML array syntax**

There are a couple options, single-line or multi-line.

For those interested to read more, [here is a SO link 6](https://stackoverflow.com/questions/23657086/yaml-multi-line-arrays).

#### Single-line arrays <a href="#p-1297-single-line-arrays-9" id="p-1297-single-line-arrays-9"></a>

```yaml
# Single-line notation
# Each element is comma-separated inside the array closures. 
# May have new lines.
engine:
  dataWorkersMultiaddrs: [
      "/ip4/127.0.0.1/tcp/40000",
      ....
]

# or 

engine:
  dataWorkersMultiaddrs: [ "/ip4/127.0.0.1/tcp/40000", "/ip4/127.0.0.1/tcp/40001", # can all be on one line
    "/ip4/127.0.0.1/tcp/40003", # or on multiple lines
    "/ip4/127.0.0.1/tcp/40004", # or on multiple lines
      ....
]
```

#### Multi-line arrays <a href="#p-1297-multi-line-arrays-10" id="p-1297-multi-line-arrays-10"></a>

```yaml
# one element per line, uses dash to indicate individual array elements
# no commas between entries
engine:
  dataWorkersMultiaddrs: 
      - "/ip4/127.0.0.1/tcp/40000"
      ....

```

#### Writing the data-worker elements <a href="#p-1297-writing-the-data-worker-elements-11" id="p-1297-writing-the-data-worker-elements-11"></a>

Data-workers will be mapped as follows:

* Base port (by default) 40000
* –core starts at 1

What this maps out to is:

**Command:**

```bash
node-1.4.21.1-linux-amd64 --core 1
# start a node on port 40000 on the machine it runs on.
```

**Config Mapping:**

The index in your `engine.dataWorkerMultiaddrs` array of 0 (core index - 1) must be `/ip4/<ip4-address>/tcp/40000` where `<ip4-address>` is the internal/private IP address of the machine the above command will be ran on.

#### Full Example <a href="#p-1297-full-example-14" id="p-1297-full-example-14"></a>

Assuming machine A will have the control process, then that means Machine A will only have 3 definitions, and Machine B will have 4.

**Config**

```yaml
engine:
  ...
  dataWorkerMultiaddrs: 
    # Machine A data workers
    - /ip4/192.168.0.200/tcp/40000
    - /ip4/192.168.0.200/tcp/40001
    - /ip4/192.168.0.200/tcp/40002
    # Machine B data workers
    - /ip4/192.168.0.201/tcp/40003
    - /ip4/192.168.0.201/tcp/40004
    - /ip4/192.168.0.201/tcp/40005
    - /ip4/192.168.0.201/tcp/40006
  difficulty: 0
...
```

Now copy this config to both Machine A and Machine B.

{% hint style="warning" %}
The master node `keys.yml` and `config.yml` must be also placed in your workers nodes for the cluster to work correctly.
{% endhint %}



**Commands**

On the servers run the following:

**Machine A**

```bash
~/ceremonyclient/node/node-1.4.21.1-linux-amd64 // this will start up the parent process, but not any worker nodes because the .engine.dataWorkerMultiaddrs array is not empty
~/ceremonyclient/node/node-1.4.21.1-linux-amd64 --core 1
~/ceremonyclient/node/node-1.4.21.1-linux-amd64 --core 2
~/ceremonyclient/node/node-1.4.21.1-linux-amd64 --core 3
```

**Machine B**

```bash
~/ceremonyclient/node/node-1.4.21.1-linux-amd64 --core 4
~/ceremonyclient/node/node-1.4.21.1-linux-amd64 --core 5
~/ceremonyclient/node/node-1.4.21.1-linux-amd64 --core 6
~/ceremonyclient/node/node-1.4.21.1-linux-amd64 --core 7
```

You must use the incrementing core id or it will not find the right index in the `.engine.dataWorkerMultiaddr` array.

**Technical Note:**

I started with `--core 1` because it’s the core param cannot be 0 (it would result in a out of bounds array index error. For those curious for the technical reason: `node/main.go:389` in the source repo works as follows:

if you define --core it will pass in the value and attempt to find the appropriate rpcMultiaddr:

```go
if len(nodeConfig.Engine.DataWorkerMultiaddrs) != 0 {
    rpcMultiaddr = nodeConfig.Engine.DataWorkerMultiaddrs[*core-1]
}
```

### Firewall Rules for Clusters <a href="#p-1297-firewall-rules-for-clusters-20" id="p-1297-firewall-rules-for-clusters-20"></a>

You could run Machine B without any firewalls, just connected to Machine A, which would/should have a firewall.

However if Machine B is a cloud device with an IP address you will want the firewall anyways.

If you have these firewalls active, you need to add local network exceptions to the firewall on servers that do not have a control process. Doing so will allow your control process to communicate to your data workers. This would look something like this:

```bash
# On Machine B
sudo ufw allow from 192.168.0.201 to any port 40003:4006 proto tcp 
# On Machine C
sudo ufw allow from 192.168.0.201 to any port 40007:40016 proto tcp
...
```

### Scaling this out further <a href="#p-1297-scaling-this-out-further-21" id="p-1297-scaling-this-out-further-21"></a>

Now, introduce a new server, Machine C (internal IP address of 192.168.0.203 with 10 workers)., then the config needs to be updated on A and B (as well as copied to C) and the commands for each of the machines would look as follows:

#### Config.yml (not all content is shown, and comments are just for clarity’s sake, not for any config function) <a href="#p-1297-configyml-not-all-content-is-shown-and-comments-are-just-for-claritys-sake-not-for-any-config" id="p-1297-configyml-not-all-content-is-shown-and-comments-are-just-for-claritys-sake-not-for-any-config"></a>

```yaml
engine:
  ...
  dataWorkerMultiaddrs: 
    # Machine A data workers
    - /ip4/192.168.0.200/tcp/40000
    - /ip4/192.168.0.200/tcp/40001
    - /ip4/192.168.0.200/tcp/40002
    # Machine B data workers
    - /ip4/192.168.0.201/tcp/40003
    - /ip4/192.168.0.201/tcp/40004
    - /ip4/192.168.0.201/tcp/40005
    - /ip4/192.168.0.201/tcp/40006
    # Machine C data workers
    - /ip4/192.168.0.203/tcp/40007
    - /ip4/192.168.0.203/tcp/40008
    - /ip4/192.168.0.203/tcp/40009
    - /ip4/192.168.0.203/tcp/40010
    - /ip4/192.168.0.203/tcp/40011
    - /ip4/192.168.0.203/tcp/40012
    - /ip4/192.168.0.203/tcp/40013
    - /ip4/192.168.0.203/tcp/40014
    - /ip4/192.168.0.203/tcp/40015
    - /ip4/192.168.0.203/tcp/40016
  difficulty: 0
```

#### Machine A <a href="#p-1297-machine-a-23" id="p-1297-machine-a-23"></a>

```bash
~/ceremonyclient/node/node-1.4.21.1-linux-amd64 // this will start up the parent process, but not any worker nodes because the .engine.dataWorkerMultiaddrs array is not empty
~/ceremonyclient/node/node-1.4.21.1-linux-amd64 --core 1
~/ceremonyclient/node/node-1.4.21.1-linux-amd64 --core 2
~/ceremonyclient/node/node-1.4.21.1-linux-amd64 --core 3
```

#### Machine B <a href="#p-1297-machine-b-24" id="p-1297-machine-b-24"></a>

```bash
~/ceremonyclient/node/node-1.4.21.1-linux-amd64 --core 4
~/ceremonyclient/node/node-1.4.21.1-linux-amd64 --core 5
~/ceremonyclient/node/node-1.4.21.1-linux-amd64 --core 6
~/ceremonyclient/node/node-1.4.21.1-linux-amd64 --core 7
```

#### Machine C <a href="#p-1297-machine-c-25" id="p-1297-machine-c-25"></a>

```bash
~/ceremonyclient/node/node-1.4.21.1-linux-amd64 --core 8
~/ceremonyclient/node/node-1.4.21.1-linux-amd64 --core 9
~/ceremonyclient/node/node-1.4.21.1-linux-amd64 --core 10
~/ceremonyclient/node/node-1.4.21.1-linux-amd64 --core 11
~/ceremonyclient/node/node-1.4.21.1-linux-amd64 --core 12
~/ceremonyclient/node/node-1.4.21.1-linux-amd64 --core 13
~/ceremonyclient/node/node-1.4.21.1-linux-amd64 --core 14
~/ceremonyclient/node/node-1.4.21.1-linux-amd64 --core 15
~/ceremonyclient/node/node-1.4.21.1-linux-amd64 --core 16
~/ceremonyclient/node/node-1.4.21.1-linux-amd64 --core 17
```

And same for any further servers you add to this cluster.

#### Restarting the Nodes <a href="#p-1297-restarting-the-nodes-26" id="p-1297-restarting-the-nodes-26"></a>

You will need to restart the nodes for each config change, so as the cluster gets bigger, scripts become more useful in automating the above commands.

#### Adding “Breathing Room” <a href="#p-1297-adding-breathing-room-27" id="p-1297-adding-breathing-room-27"></a>

It may be worth not running your machines at fully capacity, especially the machine with the control process as to allow it sufficient CPU capacity.

You could technically run multiple control processes on one CPU, but I don’t see the benefit unless running a pool of other peoples where your CPU isn’t running any data workers for yourself at all. In such case you are just managing 100% control processes on a smaller core server and editing config files to connect to other people’s data workers.

### Further thoughts <a href="#p-1297-further-thoughts-28" id="p-1297-further-thoughts-28"></a>

Here are some additional thoughts in regards to this topic.

#### Adding Automation <a href="#p-1297-adding-automation-29" id="p-1297-adding-automation-29"></a>

You could script this out relatively easily, as well as making that script a service that maintains these individual processes, but may not be worth the effort for small-time operators. Ideally, the service would be able to monitor each core thread rather than the script that generates them as a whole, unless your script monitors for inactive cores.

#### Efficiency of clustering <a href="#p-1297-efficiency-of-clustering-30" id="p-1297-efficiency-of-clustering-30"></a>

**Processing Power**

The benefits of clustering become more obvious the more machines/servers you operate.

For instance, if a Node Runner has 8 Mac Minis with 8 CPU cores and ran them all separately on their own PeerIds, they’d use 1/8 of their cores for the control process. Scale that up to 8 more and that is leaving a whole Mac Mini’s worth of data workers/processing power on the table.

**Leveraging PeerId Seniority**

One of the bigger upsides to this if a Node Runner wants to scale, they would not have to start over from scratch, rather they could cluster it and from day one gain the advantages of the more senior PeerId with more processing power.

I am not sure exactly how this will play out in 2.0 with the addition to prover rings, but I imagine having faster proving times means more times in queue for another task.

#### Downsides <a href="#p-1297-downsides-33" id="p-1297-downsides-33"></a>

The downsides are more about that you aren’t running as many configs, which may be useful for splitting your node’s proving across different sectors/applications.

This is my speculation, anyways, for 2.0. For all I know, there are ways to split your data workers across different areas while clustered.

#### Running a mining pool <a href="#p-1297-running-a-mining-pool-34" id="p-1297-running-a-mining-pool-34"></a>

I was musing about this since it has been brought up, but I’m not sure exactly how this would work in splitting rewards, as I am not aware of a way to figure out how much each QUIL a data worker brings to the table. This may be a reason I suspect mining pools will have limited core counts and perhaps white-listed machines, as 1000 cores with a hodge-podge of cores may not bring as much benefit than 500 vs how much rewards are split.

There may be cases where 1000 cores would actually produce more rewards, say in the case where you are in the inner prover rings, than say if you were just starting.

### Pausing individual workers

{% hint style="warning" %}
This feature will be avilable from v 2.1.0\
For now, when issuuing the `qclient config prover pause` command, you are pausing the entire cluster.
{% endhint %}

When running Q nodes in a cluster, you can manage individual data workers within the cluster. If a data worker goes down due to an outage, you can temporarily remove it from the cluster without affecting the entire system.&#x20;

The fastest way to handle this is to issue a manual stop command from qclient specifically for that ring (or worker). This pause message essentially tells the system to skip that particular worker for now. This approach is preferable to stopping the whole cluster, especially when only a few data workers are affected. There is a limit to how long a worker can be paused, but it's better than missing demanded intervals. This flexibility means that clusters aren't at a disadvantage compared to standalone nodes when it comes to managing individual worker outages.\


***

<table data-card-size="large" data-column-title-hidden data-view="cards" data-full-width="false"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><strong>The Best Server Providers for your Nodes</strong></td><td>CLICK TO SEE THEM</td><td><a href="../../best-server-providers.md">best-server-providers.md</a></td><td></td><td><a href="../../.gitbook/assets/best-serve-providers-banner-text-1-1-B.jpg">best-serve-providers-banner-text-1-1-B.jpg</a></td></tr><tr><td><strong>Want to say thank you?</strong></td><td>CLICK TO DONATE</td><td><a href="../../want-to-say-thank-you.md">want-to-say-thank-you.md</a></td><td></td><td><a href="../../.gitbook/assets/donations-banner-text-1-1-B.jpg">donations-banner-text-1-1-B.jpg</a></td></tr></tbody></table>

