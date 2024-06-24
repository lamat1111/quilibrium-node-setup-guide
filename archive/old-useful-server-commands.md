# 🔠 OLD - Useful server commands

{% hint style="info" %}
If you are looking for commands to transfer QUIL tokens, please [look here](broken-reference)
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

### Attach to existing tmux session

```bash
tmux a -t quil
```

To detach from tmux press CTRL+B then release both keys and press D

### Create tmux session + run node + detach from session: 1 step command&#x20;

This is useful to quickly run then node in a session AFTER you have rebooted your server. Only RUN this after a reboot and if you have no tmux session already active.\
The last part `~/scripts/qnode_restart.sh` will only work if you have run the auto-installer in this guide. Otherwise, you have to use `GOEXPERIMENT=arenas go run ./...`

```bash
tmux new-session -d -s quil 'export PATH=$PATH:/usr/local/go/bin && cd ~/ceremonyclient/node && ~/scripts/qnode_restart.sh'
```

### Create cronjob to run the node automatically after a reboot&#x20;

You only have to run this command once. This will set up a cronjob that will create your tmux session and run the node automatically after every reboot of your server. Shoutout to Peter Jameson (Quilibrium Discord community creator) for the script.\
The last part `~/scripts/qnode_restart.sh` will only work if you have run the auto-installer in this guide. Otherwise, you have to use `GOEXPERIMENT=arenas go run ./...`

```bash
echo "@reboot sleep 10 && tmux new-session -d -s quil 'export PATH=\$PATH:/usr/local/go/bin && cd ~/ceremonyclient/node && ~/scripts/qnode_restart.sh'" | crontab -
```

If you need to delete the crontab:\
Open the crontab file for editing with `crontab -e`\
Locate the line corresponding to the cron job you want to delete and delete it. Press CTRL+X, then Y to save, then ENTER

### Kill node process&#x20;

Use this in case you need to stop the node and kill the process

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

