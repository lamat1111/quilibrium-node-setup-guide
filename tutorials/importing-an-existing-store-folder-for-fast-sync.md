# ⚡ Importing an existing store folder for fast sync

{% hint style="warning" %}
There is no need to do this. Your node starts earning rewards as soon as it's online, even if it's still syncing.
{% endhint %}

For syncing faster your new node it is possible to import the ceremonyclient/node/.config/store folder from an already synced node.

If you are running your node as a service,  you can use a script to do this automatically. Just run the command below in your terminal. You can inspect the code [here](https://github.com/lamat1111/Quilibrium-Node-Auto-Installer/blob/main/store\_kickstart).

{% hint style="warning" %}
_Follow the_  [safety-checks.md](../safety-checks.md "mention")before running this script in your server
{% endhint %}

```
wget --no-cache -O - https://raw.githubusercontent.com/lamat1111/quilibriumscripts/master/tools/store_kickstart | bash
```

***

[![image-text](https://accademiainfinita.it/extra-contents/quil-best-providers-banner-square.jpg)](https://iri.quest/quil-best-server-providers)

***

## Manual process

If you don't have a store folder to use, [you can download one here](https://snapshots.cherryservers.com/quilibrium/store.zip) (this is hosted by [CherryServers](https://iri.quest/cherryservers) and safe to use). In any case, if someone gives you a zipped store folder, always scan it for viruses and malware.

Once you have your store.zip proceed like this (this procedure assumes that you are using Termius SFTP feature or WinSCP to navigate the folders.

1. Scan the .zip for viruses, then open it and check that it contains a "store" folder and that the folder contains a long list of .sst files
2. Stop your node&#x20;
3. Backup your existing store folder (just change its name)
4. Upload the new store folder and extract the archive in ceremonyclient/node/.config/
5. Restart your node and wait. \
   It's normal for the node process to crash 1 or 2 times, but after 15 minutes it should start to sync normally.

{% hint style="info" %}
If you place an existing store folder (from an alerady synced node) in a new node .config folder, without running this new node for some minutes first, the `store` folder to be removed because it will be treated as test data.

To avoid this, you need to place a `REPAIR` file in `.config` alongside the`store` folder you imported. Then, when you start the new node, the `store` folder will be used as-is. You can download a REPAIR file below.

Or, as an alternative, let the new node run for some minutes (it will create its own store folder and REPAIR file), and only then import your own store folder.
{% endhint %}

{% file src="../.gitbook/assets/REPAIR" %}
import in your ceremonyclient/node/.config/ folder
{% endfile %}

If the node keeps crashing, and you keep getting an error similar to this one

```
panic: get parent data clock frame: item not found

goroutine 1 [running]: source.quilibrium.com/quilibrium/monorepo/node/app.
(*Node).RunRepair(0xc0030f47d0) /opt/ceremonyclient/node/app/node.go:87 
+0x5da main.repair({0xc0002c33c8, 0x7}, 0xc000098eb0?) 
/opt/ceremonyclient/node/main.go:488 +0xa5 main.main() 
/opt/ceremonyclient/node/main.go:220 +0x4d5
```

then unfortunately the process did not work, the store folder is corrupted and cannot be repaired.&#x20;

Stop the node, delete the store folder with the command `rm -r root/ceremonyclient/node/.config/store` and restore your backup. If you do not have a backup, just remove the store folder and restart the node. It will create  a new one and start to sync from 0 again.

***

## Importing your store folder from an existing node (that you own)

### On the source node (existing store folder)

zip the store folder

```bash
nohup tar -czvf /root/ceremonyclient/node/.config/store_kickstart.tar.gz -C /root/ceremonyclient/node/.config/store .
```

download locally and upload to your new server in /root/ceremonyclient/node/.config/&#x20;

_alternative: use Termius SFTP to drag/drop the store\_kickstart.tar.gz between the 2 servers_

### **On the target server**

Stop the node

Rename the existing store to store-original

```bash
mv /root/ceremonyclient/node/.config/store /root/ceremonyclient/node/.config/store-original
```

Create a new store folder

```bash
mkdir -p /root/ceremonyclient/node/.config/store
```

Extract the archive in the store folder

```bash
cd /root/ceremonyclient/node/.config && tar -xvf store_kickstart.tar.gz -C store
```

Restart the node
