# ☑️ Limiting your vCores usage

If the number of vCores (vCPU) is less than half of your total RAM, you may receive errors and the node may crash. For instance, a server with 32 vCores and 32 GB of RAM will have issues (the perfect ratio would be 32 vCores and 64 GB of RAM). See [hardware-requirements.md](../../../hardware-requirements.md "mention")

To check your number of vCores you can use `nproc`

{% hint style="info" %}
The number of cores you see on a rental server means that "usually" you will have a double number of vCores, because of hypethreading.
{% endhint %}

## How to limit the number of vCores your node uses

<details>

<summary>Version of the tutorial if you are NOT running as a service</summary>

The below process will limit the use of VCores for your whole system, not just your node process.

Open your `.bashrc` file using a text editor, such as `nano`:

```sh
nano ~/.bashrc
```

Add the following line at the end of your `.bashrc` file. Replace `(cores)` with the desired number of vCores:

```sh
export GOMAXPROCS=(cores)
```

For example, on a server with 32 vCores and 32 GB of RAM, you would set this number to 16, since it needs to be at least half of your RAM. You can also set it lower if you still receive issues after testing.

If you have a server with the correct ratio of vCores to RAM but still face issues, try setting `GOMAXPROCS` to one less than your total system vCores. For example, on a 32 vCore, 64 GB RAM server, you might set: export GOMAXPROCS=31

To save the changes, type CTRL + X, then Y, then ENTER.

**Source your .bashrc for the changes to be effective**

```bash
source ~/.bashrc
```

### **Check your server performance:**

Monitor the node log to ensure everything is functioning correctly:

I also like to use [Hetrixtools](https://iri.quest/hetrixtools) to monitor system resources more closely (free to usen up to 15 servers)

</details>

### **Edit the systemd service file for `ceremonyclient`:**

Open the service file for `ceremonyclient`. This is typically located at `/etc/systemd/system/ceremonyclient.service`. If it’s not there, you might need to locate the correct path.

```sh
sudo nano /etc/systemd/system/ceremonyclient.service
```

### **Set the GOMAXPROCS environment variable:**

Add the following line under the `[Service]` section:

```ini
[Unit]
Description=Ceremony Client Go App Service

[Service]
Type=simple
Restart=always
RestartSec=5s
WorkingDirectory=/root/ceremonyclient/node
ExecStart=/root/ceremonyclient/node/release_autorun.sh
Environment="GOMAXPROCS=(cores)"

[Install]
WantedBy=multi-user.target
```

Replace `(cores)` with the desired number of vCores.&#x20;

To check your number of vCores you can use `nproc`, then simply set a GOMAXPROCS value that is half your RAM value and see how it goes.&#x20;

For example, on a server with 32 vCores and 32 GB of RAM, you would set  GOMAXPROCS=16

If it still doesn't solve the error, diminish the value by 1 and test again, and son on...

{% hint style="info" %}
If you have a server with the correct ratio of vCores to RAM but still face issues, try setting `GOMAXPROCS` to one less than your total system vCores. For example, on a 32 vCore, 64 GB RAM server, you might set GOMAXPROCS=31
{% endhint %}

### **Reload systemd to apply the changes:**

```sh
sudo systemctl daemon-reload
```

### Restart your service

```bash
service ceremonyclient restart
```

### **Check your server performance:**

Monitor the node log to ensure everything is functioning correctly:

```sh
sudo journalctl -u ceremonyclient.service -f --no-hostname -o cat
```

I also like to use [Hetrixtools](https://iri.quest/hetrixtools) to monitor system resources more closely (free to use on up to 15 servers)

***

<table data-card-size="large" data-column-title-hidden data-view="cards" data-full-width="false"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><strong>Want to say thank you?</strong></td><td>CLICK TO DONATE</td><td><a href="../../../want-to-say-thank-you.md">want-to-say-thank-you.md</a></td><td></td><td><a href="../../../.gitbook/assets/donations-banner-text-1-1-B.jpg">donations-banner-text-1-1-B.jpg</a></td></tr></tbody></table>

