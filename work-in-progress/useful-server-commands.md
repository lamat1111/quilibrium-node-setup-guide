# 🔠 Useful server commands

{% hint style="info" %}
If you are looking for commands to transfer QUIL tokens, please [look here](https://app.gitbook.com/o/OarGuxi0cVButvqcFwRt/s/G8xnbuGv4YmbeRKqTig0/)
{% endhint %}

{% hint style="warning" %}
THIS IS  A NEW VERSION OF THE SERVER COMMANDS

If you are looking for the old version, you will fin ti here [old-useful-server-commands.md](../archive/old-useful-server-commands.md "mention")
{% endhint %}

### Check node info&#x20;

After your node has been running for at least 30 minutes, run this command from your root folder to check the node info (Node version, Peer ID, Quil balance).\
For this to work, you need to [setup the gRPC calls](../set-up-the-grpc-calls.md) first.\
To go to the root folder, just type cd .

```bash
cd ~/ceremonyclient/node && GOEXPERIMENT=arenas go run ./... -node-info
```

### Check node version&#x20;

If the "Check node info" command above do not work, you can check the node version by running:

```bash
cat ~/ceremonyclient/node/config/version.go | grep -A 1 'func GetVersion() \[\]byte {' | grep -Eo '0x[0-9a-fA-F]+' | xargs printf '%d.%d.%d'
```

### Check node peer ID&#x20;

If the "Check node info" command above do not work, you can check the node peer ID by running:

```bash
cd ~/ceremonyclient/node && GOEXPERIMENT=arenas go run ./... -peer-id
```

### Console&#x20;

Similar to "Node info", this will show basic info about your node.

```bash
cd ~/ceremonyclient/node && GOEXPERIMENT=arenas go run ./... --db-console
```

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

## Node service commands

Start service

```bash
service ceremonyclient start
```

Stop service

```bash
service ceremonyclient stop
```

Restart service

```bash
service ceremonyclient restart
```

View node log

```bash
sudo journalctl -u ceremonyclient.service -f --no-hostname -o cat
```
