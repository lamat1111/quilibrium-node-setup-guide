# ⬆️ Updating your node

If you are running your node as a service, you can simply run the below script.&#x20;

{% hint style="success" %}
WIth the latest update of this script (29.05.2024) your node service will auto-update for all future releases, so you won't need to run this or manually update anymore :)\


If you are not sure if you have the latest node service update, feel free to run the below script. It will update your service if necessary.
{% endhint %}

{% hint style="warning" %}
Follow the  [safety-checks.md](safety-checks.md "mention") before running this script in your server
{% endhint %}

#### Check if everything is alright

Things change fast, and we may be not fast enough to update the scripts you find from now on in the guide. So, to avoid any issue, I suggest checking [Telegram pinned messages](https://t.me/quilibrium) and [Discord announcements](https://discord.gg/quilibrium) for any last minute issue or update. If there is something you don't understand, ask in the chats.

If everything looks fine, proceed to the next step.

{% hint style="info" %}
Even if you run the script but it doesn't work because there was a last minute update, don't worry. The worst that can happen is that they will give you an error.&#x20;
{% endhint %}

```
wget --no-cache -O - https://raw.githubusercontent.com/lamat1111/QuilibriumScripts/master/qnode_service_update_newsource.sh | bash
```

The script will NOT delete any customizations you made to your service file (e.g. CPUQuota or GOMAXPROX). Still, is better to check your service file after the update just to be on the safe side.

To do so you can run:

```bash
nano /lib/systemd/system/ceremonyclient.service
```

<details>

<summary>OLD script version - do not use</summary>

```
wget -O - https://raw.githubusercontent.com/0xOzgur/QuilibriumTools/v1.4.18/update.sh | bash
```

🙏 _Many tanks to_ [_@OxOzgur_](https://github.com/0xOzgur) _for providing the auto-update script_

</details>

***

<table data-card-size="large" data-column-title-hidden data-view="cards" data-full-width="false"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><strong>The Best Server Providers for your Nodes</strong></td><td>CLICK TO SEE THEM</td><td><a href="best-server-providers.md">best-server-providers.md</a></td><td></td><td><a href=".gitbook/assets/best-serve-providers-banner-text-1-1-B.jpg">best-serve-providers-banner-text-1-1-B.jpg</a></td></tr><tr><td><strong>Want to say thank you?</strong></td><td>CLICK TO DONATE</td><td><a href="want-to-say-thank-you.md">want-to-say-thank-you.md</a></td><td></td><td><a href=".gitbook/assets/donations-banner-text-1-1-B.jpg">donations-banner-text-1-1-B.jpg</a></td></tr></tbody></table>

## Manual method

{% hint style="info" %}
Source: [https://quilibrium.guide/upgrade-1-4-18](https://quilibrium.guide/upgrade-1-4-18) \
_I have only tested and reworked the instructions a bit for clarity_
{% endhint %}

#### Update your node files

Stop your node service

```bash
service ceremonyclient stop
```

Go to ceremonyclient folder.\
Check whether some files are updated in the ceremonyclient git repo.\
If there are files shown that are changed or different from your local copy, merge them.\
Do a `go clean` command to clear all previous build files.&#x20;

```bash
cd ~/ceremonyclient
git fetch origin
git merge origin
cd ~/ceremonyclient/node
GOEXPERIMENT=arenas go clean -v -n -a ./...
```

Remove the compiled go binary file `node`

```bash
rm /root/go/bin/node
ls /root/go/bin
```

Rebuild the qclient

```bash
cd ~/ceremonyclient/client
rm /root/go/bin/qclient
GOEXPERIMENT=arenas go build -o /root/go/bin/qclient main.go
ls /root/go/bin
```

Switch to branch releases of the repo

```bash
cd /root/ceremonyclient/node
git checkout release
```

Now, in order to appropriately adjust the systemd file, it's crucial to pinpoint the suitable executable file from three available options:

1. node-1.4.18-linux-amd64
2. node-1.4.18-linux-arm64
3. node-1.4.18-darwin-arm64

#### Check your system architecture

Begin by determining your server's system architecture type using the command:

```bash
echo $OSTYPE
```

If the output matches "darwin", opt for:

```bash
node-1.4.18-darwin-arm64
```

For "linux-gnu" systems, consider these choices:

1. node-1.4.18-linux-amd64
2. node-1.4.18-linux-arm64
3. node-1.4.18-darwin-arm64

To further narrow down the appropriate binary file, execute:

```bash
echo $arch
```

If "arm" is present in the output, select:

```bash
node-1.4.18-linux-arm64
```

In case of a blank result, opt for:

```bash
node-1.4.18-linux-amd64
```

#### Update the ExecStart directive and start the service

To update the service systemd file, we must adjust the ExecStart directive&#x20;

from `/root/go/bin/node ./...`&#x20;

to `/root/ceremonyclient/node/node-1.4.18-linux-amd64`.

Execute the following command to make the adjustment:

```bash
sed -i 's/ExecStart=\/root\/go\/bin\/node .\/.../ExecStart=\/root\/ceremonyclient\/node\/node-1.4.18-linux-amd64/g' /lib/systemd/system/ceremonyclient.service
```

Don't forget to reload the systemd daemon afterward:

```bash
systemctl daemon-reload
```

{% hint style="info" %}
Replace "node-1.4.18-linux-amd64" with the appropriate binary file based on the prechecks we conducted earlier.
{% endhint %}

Finally, start your node via the service command

```bash
service ceremonyclient start
```
