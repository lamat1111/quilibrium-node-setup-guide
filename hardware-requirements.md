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

Keep in mind that nodes with better specs will earn more rewards.&#x20;

The ratio for optimal rewards theoretically is be 1:2:4 (core:ram in GB:disk in GB). \
For instance 8 vCores - 16 GB RAM - 32 GB storage (see table below). Your bandwidth will also matter.

**VDS (Virtual Dedicated Servers) and Bare Metal (Physical dedicated Servers) are your best choice.** Using a VPS (Virtual Private Server) may give you issues, as often the providers oversell the resources.\
That being said, using a VPS or a home machine may work just fine if you don't care about absolutely maximizing your rewards (but you probably will have to limit your CPU usage).

### What you can expect after v1.4.18:

* Your CPU usage will be 80% > 100% all the time.
* Your RAM usage, if you have you have 2X the ratio of your vCores (eg. 4vCores, 8 GB RAM) will also be very high (80 > 90 %) all the time.
* Your bandwidth and HDD at this stage will not be used much.

### If you use a VPS or your local machine

If you choose to use a VPS; you will probably need to follow the guide  [limiting-your-vps-cpu-usage.md](tutorials/limiting-your-vps-cpu-usage.md "mention") in order to not be banned/throttled, since you will be on shared resources.&#x20;

### Choosing the right resources' ratio

Remember, when you rent an 8 cores server, it will usually have 16 vCores/vCPUs, so you need at least 32 GB of RAM (2X the number of vCores).&#x20;

Examples:

| Cores | vCores | RAM | HDD |
| ----- | ------ | --- | --- |
| 4     | 8      | 16  | 32  |
| 8     | 16     | 32  | 64  |
| 12    | 24     | 48  | 96  |

***

_If your resources' ratio is not right and your node keeps crashing, you may try t_ [solving-server-crashes-with-gomaxprocs.md](tutorials/solving-server-crashes-with-gomaxprocs.md "mention")

_\*vCores (aka vCPUs) = when you rent a server, the number of cores usually equals 2X the vCores of that server, because of hyperthreading. Eg. an 8 cores server will "usually" have 16 vCores._

***

<table data-card-size="large" data-column-title-hidden data-view="cards" data-full-width="false"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><strong>The Best Server Providers for your Nodes</strong></td><td>CLICK TO SEE THEM</td><td><a href="best-server-providers.md">best-server-providers.md</a></td><td></td><td><a href=".gitbook/assets/best-serve-providers-banner-text-1-1-B.jpg">best-serve-providers-banner-text-1-1-B.jpg</a></td></tr><tr><td><strong>Want to say thank you?</strong></td><td>CLICK TO DONATE</td><td><a href="want-to-say-thank-you.md">want-to-say-thank-you.md</a></td><td></td><td><a href=".gitbook/assets/donations-banner-text-1-1-B.jpg">donations-banner-text-1-1-B.jpg</a></td></tr></tbody></table>
