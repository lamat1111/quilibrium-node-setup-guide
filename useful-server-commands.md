# 🔠 Useful server commands

{% hint style="warning" %}
THIS IS  A NEW VERSION OF THE SERVER COMMANDS

If you are looking for the old version, you will find it here [old-useful-server-commands.md](archive/old-useful-server-commands.md "mention")
{% endhint %}

{% hint style="warning" %}
With v1.4.18 some of these commands like node-info do not work anymore. Hang on while I gather intel to understand the new working commands.
{% endhint %}

### #&#x20;

## &#x20;[check-your-node-info.md](check-your-node-info.md "mention")

## #node&#x20;

### Check QUIL balance

```bash
cd ~/ceremonyclient/node && GOEXPERIMENT=arenas go run ./... -balance
```

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

***

[![image-text](https://accademiainfinita.it/extra-contents/quil-best-providers-banner-square.jpg)](https://iri.quest/quil-best-server-providers)
