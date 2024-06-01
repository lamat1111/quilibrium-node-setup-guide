# ☑️ Limiting your CPU usage

Quilibrium will use 90-100% of your CPU power all the time. Take precautions to avoid being banned by your provider (or damaging your machine).

{% hint style="success" %}
_If you use the default `release_autorun.sh` script  to run your node, or if you install it via the_ [node-auto-installer.md](../../node-auto-installer.md "mention") _script in this guide, your CPU usage will be automatically limited to 50%._
{% endhint %}

### Steps to follow

Get your number of vCores by running `nproc`

#### Open your service file

```bash
nano /lib/systemd/system/ceremonyclient.service
```

#### Add this line in the \[Service] section (adjust the percentage as needed)

```bash
CPUQuota=1120% # Adjust the percentage as needed
```

{% hint style="info" %}
**How do you calculate your CPUQuota?**\
CPUQuota= your vCores count \* assigned quota\
_(e.g. 16 vCores at 70% => CPUQuota=1120%)_\


To calculate your CPUQuota, consider that in systems like Linux, CPU usage is typically measured as a percentage of a single CPU core's capacity, not the total capacity of all cores combined.

To clarify, the total CPU usage on an 16 vCores system, if all cores were fully utilized, would be 1600%. Therefore, when setting a CPUQuota, you're expressing the percentage of total CPU capacity you want your service to utilize. In this case, 1120% indicates that your service should use 70% of the total CPU capacity available on the VPS.



If you have limited the vCores used by your node using GOMAXPROCS (see [limiting-the-ram-assigned-to-each-vcore.md](limiting-the-ram-assigned-to-each-vcore.md "mention")), then you should count only the vCores you are actually using.\

{% endhint %}

#### Here is how the file should look like

```bash
[Unit]
Description=Ceremony Client Go App Service

[Service]
Type=simple
Restart=always
RestartSec=5s
WorkingDirectory=/root/ceremonyclient/node
ExecStart=/root/ceremonyclient/node/release_autorun.sh #this line may be different for some of you
CPUQuota=1120%  # Adjust the percentage as needed

[Install]
WantedBy=multi-user.target

```

To save press CTRL + X, then Y, then ENTER

#### Reload your systemd manager configuration

```bash
systemctl daemon-reload
```

Done!

#### **Check your server performance:**

Monitor the node log to ensure everything is functioning correctly:

```sh
sudo journalctl -u ceremonyclient.service -f --no-hostname -o cat
```

I also like to use [Hetrixtools](https://iri.quest/hetrixtools) to monitor system resources more closely (free to use on up to 15 servers)

***

<table data-card-size="large" data-column-title-hidden data-view="cards" data-full-width="false"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><strong>The Best Server Providers for your Nodes</strong></td><td>CLICK TO SEE THEM</td><td><a href="../../best-server-providers.md">best-server-providers.md</a></td><td></td><td><a href="../../.gitbook/assets/best-serve-providers-banner-text-1-1-B.jpg">best-serve-providers-banner-text-1-1-B.jpg</a></td></tr><tr><td><strong>Want to say thank you?</strong></td><td>CLICK TO DONATE</td><td><a href="../../want-to-say-thank-you.md">want-to-say-thank-you.md</a></td><td></td><td><a href="../../.gitbook/assets/donations-banner-text-1-1-B.jpg">donations-banner-text-1-1-B.jpg</a></td></tr></tbody></table>
