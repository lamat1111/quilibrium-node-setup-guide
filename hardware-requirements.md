---
description: Better Specs = More Rewards :-)
---

# 💻 Hardware requirements

* **4 vCores/vCPUs\***
* **8 GB of RAM**
* **250 GB of storage (better SSD or NVMe)**
* **400 Mbit/s symmetric bandwidth (or 50 MB/s)**

{% hint style="info" %}
_Outbound traffic after v1.4.18 should be up to 5 TB per month (raw approximation), depending on how you set the node._
{% endhint %}

You can also refer to the [Quilibrium official docs](https://quilibrium.com/docs/noderunning).

Keep in mind that nodes with better specs will earn more rewards. If you really want to maximize your rewards and are ready to delve into some technical stuff, you should definitely read this article: [What are the most important factors in a node performance?](https://docs.quilibrium.one/start/v/wiki/technical/what-are-the-most-important-factors-in-a-node-performance)

### Optimal specs ratio

The ratio for optimal rewards theoretically is  1:2:4 (core:ram in GB:disk in GB). \
For instance, 8 vCores - 16 GB RAM - 32 GB storage (see table below). Your bandwidth will also matter.

### Dedicated VS shared servers

**Bare Metal (Physical dedicated Servers) and VDS (Virtual Dedicated Servers) are your best choice.** Using a VPS (Virtual Private Server) may give you issues, as often the providers oversell the resources.

***

### What you can expect after v2.0:

* CPU usage will be 90% > 100% all the time.
* RAM usage, if you have you have 2X the ratio of your vCores (eg. 4vCores, 8 GB RAM) will also be very high (70 > 90 %).
* Bandwidth consumption is still unclear, but current tests show a very high bandwidth usage (300 Mbps on average). This will diminish as the code gets optimized. Check on the social channels for most update average usage.
* HDD usage is still unclear. Have at least 250 GB of free space.  Check on the social channels for most update average usage.

If you want to limit your CPU usage, follow the guide  [limiting-your-cpu-usage.md](tutorials/node/managing-your-system-resources/limiting-your-cpu-usage.md "mention") .

### Choosing the right resources' ratio

Remember, when you rent an 8 cores server, it will usually have 16 vCores/vCPUs, so you need at least 32 GB of RAM (2X the number of vCores).&#x20;

Examples:

| Cores | vCores | RAM | HDD |
| ----- | ------ | --- | --- |
| 4     | 8      | 16  | 32  |
| 8     | 16     | 32  | 64  |
| 12    | 24     | 48  | 96  |

***

_If your resources' ratio is not right and your node keeps crashing, you may try to_[limiting-your-vcores-usage.md](tutorials/node/managing-your-system-resources/limiting-your-vcores-usage.md "mention")

***

_\*vCores (aka vCPUs) = when you rent a server, the number of cores usually equals 2X the vCores of that server, because of hyperthreading. Eg. an 8 cores server will "usually" have 16 vCores._

***

<table data-card-size="large" data-column-title-hidden data-view="cards" data-full-width="false"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><strong>The Best Server Providers for your Nodes</strong></td><td>CLICK TO SEE THEM</td><td><a href="best-server-providers.md">best-server-providers.md</a></td><td></td><td><a href=".gitbook/assets/best-serve-providers-banner-text-1-1-B.jpg">best-serve-providers-banner-text-1-1-B.jpg</a></td></tr><tr><td><strong>Want to say thank you?</strong></td><td>CLICK TO DONATE</td><td><a href="want-to-say-thank-you.md">want-to-say-thank-you.md</a></td><td></td><td><a href=".gitbook/assets/donations-banner-text-1-1-B.jpg">donations-banner-text-1-1-B.jpg</a></td></tr></tbody></table>
