# 🔠 Useful server commands

{% hint style="warning" %}
THIS IS  A NEW VERSION OF THE SERVER COMMANDS

If you are looking for the old version, you will find it here [old-useful-server-commands.md](archive/old-useful-server-commands.md "mention")
{% endhint %}

### Node service commands

Please look in [Node Service Commands](https://lamat.gitbook.io/quilibrium-node-setup-guide/node-auto-installer#node-service-commands)

### Node info (peerID, balance, frame number...)

Please look in [check-your-node-info.md](check-your-node-info.md "mention")

### Kill node process&#x20;

Use this in case you need to stop the node and kill the process.&#x20;

If you are running the node as a service, the service will restart the node immediately, so use the command `service ceremonyclient stop` instead.

```bash
pkill node && pkill -f "go run ./..."
```

### Empty "store" folder&#x20;

CAREFUL: this will empty your "store" folder, only use it if you know what you are doing. Sometimes when you receive errors that you cannot debug, you can solve by killing the node process, emptying the store folder and starting the node again from scratch.

```bash
sudo rm -r ~/ceremonyclient/node/.config/store
```

### Backup keys.yml and config.yml to a root/backup folder&#x20;

This may be useful if you have to clean up your ceremonyclient folder and don't want to download locally your config.yml and keys.yml. You can just back up them remotely on a root/backup folder and copy them again in the node folder later on.

Copy the files from your node folder to the root/backup folder

```bash
mkdir -p /root/backup && cp /root/ceremonyclient/node/.config/config.yml /root/backup && cp /root/ceremonyclient/node/.config/keys.yml /root/backup
```

Copy the files back from root/backup to your node folder (a copy will also remain in the root/backup folder)

```bash
cp /root/backup/{config.yml,keys.yml} /root/ceremonyclient/node/.config/
```

### Check total nodes connected to the network&#x20;

Install grpcURL

```bash
go install github.com/fullstorydev/grpcurl/cmd/grpcurl@latest
```

Run

```bash
/root/go/bin/grpcurl -plaintext -max-msg-sz 5000000 localhost:8337 quilibrium.node.node.pb.NodeService.GetPeerInfo | grep peerId | wc -l
```

***

<table data-card-size="large" data-column-title-hidden data-view="cards" data-full-width="false"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><strong>The Best Server Providers for your Nodes</strong></td><td>CLICK TO SEE THEM</td><td><a href="best-server-providers.md">best-server-providers.md</a></td><td></td><td><a href=".gitbook/assets/best-serve-providers-banner-text-1-1-B.jpg">best-serve-providers-banner-text-1-1-B.jpg</a></td></tr><tr><td><strong>Want to say thank you?</strong></td><td>CLICK TO DONATE</td><td><a href="want-to-say-thank-you.md">want-to-say-thank-you.md</a></td><td></td><td><a href=".gitbook/assets/donations-banner-text-1-1-B.jpg">donations-banner-text-1-1-B.jpg</a></td></tr></tbody></table>
