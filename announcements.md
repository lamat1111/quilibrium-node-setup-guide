---
description: Important updates if you have used this guide auto-installer
---

# 📣 Announcements

**From Quilibrium 2.0 it is important to stop your node gracefully to avoid being penalized.**

{% hint style="warning" %}
Only follow this guide if you are on Linux/Ubuntu and are NOT running a cluster.
{% endhint %}

If you installed your node via the scripts in this guide or the QONE menu, please continue reading.\
\
Your service file should run your node directly via its binary, and have some special settings to stop the node gracefully. A correct service file will look like similar to the one below. \
\
&#xNAN;_&#x4E;ode version and system architecture may change, and if you have CPUQUOTA, GOMAXPROCS settings, that is not an issue._

```sh
[Unit]
Description=Ceremony Client Go App Service

[Service]
Type=simple
Restart=always
RestartSec=5s
WorkingDirectory=/root/ceremonyclient/node
ExecStart=/root/ceremonyclient/node/node-1.4.21.1-linux-amd64
KillSignal=SIGINT
TimeoutStopSec=30s

[Install]
WantedBy=multi-user.target
```

Check your current service file:

```sh
nano /lib/systemd/system/ceremonyclient.service
```

And if it is still running the node via release\_autorun.sh, make the necessary changes. These are the important lines to add (&#x6E;_&#x6F;de version and system architecture may be different for you)._

```sh
ExecStart=/root/ceremonyclient/node/node-1.4.21.1-linux-amd64
KillSignal=SIGINT
TimeoutStopSec=30s
```

Finally, run

{% code overflow="wrap" %}
```sh

sudo systemctl daemon-reload && sudo systemctl restart ceremonyclient

```
{% endcode %}

### To do all this automatically, you can also simply use the below script

{% code overflow="wrap" %}
```sh
mkdir -p ~/scripts && \
wget -O ~/scripts/qnode_service_change_autorun_to_bin.sh "https://raw.githubusercontent.com/lamat1111/QuilibriumScripts/main/tools/qnode_service_change_autorun_to_bin.sh" && \
chmod +x ~/scripts/qnode_service_change_autorun_to_bin.sh && \
~/scripts/qnode_service_change_autorun_to_bin.sh
```
{% endcode %}

The script will show you the new service file at the end and ask for your manual confirmation. If something is not right, you can then manually edit the file yourself to make corrections.

***

After these changes, your node won't be able to auto-update anymore, you will have to update manually. But when stopping or restarting it, you should not be penalized.





***

Please also look in [Discord](https://discord.gg/quilibrium) and [Telegram](https://t.me/quilibrium) for the latest updates.

***

<table data-card-size="large" data-column-title-hidden data-view="cards" data-full-width="false"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><strong>The Best Server Providers for your Nodes</strong></td><td>CLICK TO SEE THEM</td><td><a href="best-server-providers.md">best-server-providers.md</a></td><td></td><td><a href=".gitbook/assets/best-serve-providers-banner-text-1-1-B.jpg">best-serve-providers-banner-text-1-1-B.jpg</a></td></tr><tr><td><strong>Want to say thank you?</strong></td><td>CLICK TO DONATE</td><td><a href="want-to-say-thank-you.md">want-to-say-thank-you.md</a></td><td></td><td><a href=".gitbook/assets/donations-banner-text-1-1-B.jpg">donations-banner-text-1-1-B.jpg</a></td></tr></tbody></table>

