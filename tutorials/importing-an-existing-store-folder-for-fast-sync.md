# ⚡ Importing an existing store folder for fast sync

For syncing faster your new node it is possible to import the ceremonyclient/node/.config/store folder from an already synced node.

If you don't have one, try to ask in the Telegram or Discord and maybe someone will help you. If someone gives you a zipped store folder, always scan it for viruses and malware.

Once you have your store.zip proceed like this (this procedure assumes that you are using Termius SFTP feature or WinSCP to navigate the folders.

1. Scan the .zip for viruses, then open it and check that it contains a "store" folder and that the folder contains a long list of .sst files
2. Stop your node&#x20;
3. Backup your existing store folder (just change its name)
4. Upload the new store folder and extract the archive in ceremonyclient/node/.config/
5. Check that your new ceremonyclient/node/.config/store folder contains a list of .sst files
6. Restart your node and wait. \
   It's normal for the node process to crash 1 or 2 times, but after 15 minutes it should start to sync normally.
7. _OPTIONAL. Sometimes this can solve the issue if your node keeps crashing after you imported an existing store folder._ \
   Import the ceremonyclient/node/.config/REPAIR file from an existing synced node (backup your existing REPAIR file). If you don't have a REPAIR file you can use the one linked below.

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

## Importing your store folder from an existing node

#### On the source node (existing store folder)

zip the store folder

```bash
nohup tar -czvf /root/ceremonyclient/node/.config/store_kickstart.tar.gz -C /root/ceremonyclient/node/.config/store .
```

download locally and upload to your new server in /root/ceremonyclient/node/.config/&#x20;

_alternative: use Termius SFTP to drag/drop the store\_kickstart.tar.gz between the 2 servers_

#### **On the target server**

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