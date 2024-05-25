# ♨️ Limiting your VPS CPU usage

If you are running the node an a VPS, sometimes you may need to limit your CPU usage to avoid your provider throttling your bandwidth or blocking you (since you are on shared resources).

Please note that this will also reduce the rewards you earn, but if you really need to do it, and you are running the node as a service, here is how.

Open your service file

```bash
nano /lib/systemd/system/ceremonyclient.servic
```

Add this line in the \[Service] section (adjust the percentage as needed)

```
CPUQuota=400%
```

{% hint style="info" %}
**How do you calculate your CPUQuota?**\
To calculate your CPUQuota, consider that in systems like Linux, CPU usage is typically measured as a percentage of a single CPU core's capacity, not the total capacity of all cores combined.

For example, if you have an 8-core VPS and you wish your service to utilize only half of all CPU cores when necessary, you would set the CPUQuota to 400%. This might seem counterintuitive, but it aligns with how CPU usage is calculated in these systems.

To clarify, the total CPU usage on an 8-core system, if all cores were fully utilized, would be 800%. Therefore, when setting a CPUQuota, you're expressing the percentage of total CPU capacity you want your service to utilize. In this case, 400% indicates that your service should use half of the total CPU capacity available on the VPS.
{% endhint %}

Here is how the file should look like

```bash
[Unit]
Description=Ceremony Client Go App Service

[Service]
Type=simple
Restart=always
RestartSec=5s
WorkingDirectory=/root/ceremonyclient/node
ExecStart=/root/ceremonyclient/node/node-1.4.18-linux-amd64
CPUQuota=400%  # Adjust the percentage as needed

[Install]
WantedBy=multi-user.target

```

To save press CTRL + X, then Y, then ENTER

Now stop the service

```
service ceremonyclient stop
```

Delete your SELF\_TEST file (this is very important, if you don't do this your node may be disqualified for cheating)

```bash
rm ~/root/ceremonyclient/node/.config/SELF_TEST
```

Restart the service

```bash
service ceremonyclient start
```

{% hint style="warning" %}
If you need to change the CPU % again, or to remove the limit, always delete your SELF\_TEST file after and restart the service.
{% endhint %}

***

[![image-text](https://accademiainfinita.it/extra-contents/quil-best-providers-banner-square.jpg)](https://iri.quest/quil-best-server-providers)
