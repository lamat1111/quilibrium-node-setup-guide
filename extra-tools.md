---
description: Manage your node like a PRO
---

# 🔧 Extra tools

### External tools

* To manage your nodes, use [Termius](https://termius.com/), the coolest SSH client and terminal around :)
* To track your server uptime and resources usage use [Hetrixtools.com](https://hetrix.tools/u-862828), you can track up to 15 servers for free and the setup is very easy

### Internal tools&#x20;

<details>

<summary>vnstat - monitor bandwidth and data flow</summary>

```bash
sudo apt update && sudo apt install vnstat
```

To check the current bandwidth usage use `vnstat`.\
To check hourly stats e use `vnstat -h`.\
Daily: `vnstat -d`. Monthly: `vnstat -m`. Top 10 traffic days: `vnstat -t`.

</details>

<details>

<summary>speedtest - monitor bandwidth speed</summary>

```bash
sudo apt-get install curl
curl -s https://packagecloud.io/install/repositories/ookla/speedtest-cli/script.deb.sh | sudo bash
sudo apt-get install speedtest
```

</details>

<details>

<summary>htop - monitor all processes and resources' consumption</summary>

```bash
sudo apt update && sudo apt install htop
```

To use it just type `htop`

</details>

***

<table data-card-size="large" data-column-title-hidden data-view="cards" data-full-width="false"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><strong>The Best Server Providers for your Nodes</strong></td><td>CLICK TO SEE THEM</td><td><a href="best-server-providers.md">best-server-providers.md</a></td><td></td><td><a href=".gitbook/assets/best-serve-providers-banner-text-1-1-B.jpg">best-serve-providers-banner-text-1-1-B.jpg</a></td></tr><tr><td><strong>Want to say thank you?</strong></td><td>CLICK TO DONATE</td><td><a href="want-to-say-thank-you.md">want-to-say-thank-you.md</a></td><td></td><td><a href=".gitbook/assets/donations-banner-text-1-1-B.jpg">donations-banner-text-1-1-B.jpg</a></td></tr></tbody></table>
