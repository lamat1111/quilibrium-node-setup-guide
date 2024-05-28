# ✔️ Check your node info

{% hint style="warning" %}
For these commands to work, you need to  [set-up-the-grpc-calls.md](set-up-the-grpc-calls.md "mention")
{% endhint %}

`node-1.4.18-linux-amd64` will need to change depending on the node version and architecture. If you run on Ubuntu 22.04, what you find here is usually correct. [How to check your system architecture](https://lamat.gitbook.io/quilibrium-node-setup-guide/updating-your-node#check-your-system-architecture).

**Get your peerID**

```bash
cd ~/ceremonyclient/node && ./node-1.4.18-linux-amd64 -peer-id
```

**See Node Info** \
_this can give an error on nodes that are not fully sync, but you will still see your peerID_

```bash
cd ~/ceremonyclient/node && ./node-1.4.18-linux-amd64 -node-info
```

**Run the DB console**\
_shows your peerID and balance, press Q to detach_

```bash
cd ~/ceremonyclient/node && ./node-1.4.18-linux-amd64 --db-console
```

**Check Balances**

```bash
cd ~/ceremonyclient/node && ./node-1.4.18-linux-amd64 ./... -balance
```

{% hint style="info" %}
Copy your PeerID and store it somewhere. This is the ID of your node and you can share it with others if you need to.
{% endhint %}

***

### **Extract Peer Manifests by Peer ID**

{% hint style="info" %}
_This command retrieves the manifest details for a specific peer identified by its unique peer ID. You will be probably requested to install some app before being able to execute it._

_The peer details contain much relevant info about your peer, included the "difficulty metric" a score telling you how your node is performing in the network._
{% endhint %}

If it's the first time you are trying to retrieve the manifest, run the below script (do the [safety-checks.md](safety-checks.md "mention") first). This will install the necessary apps and output the manifest last.

```
wget --no-cache -O - https://raw.githubusercontent.com/lamat1111/quilibriumscripts/main_new/tools/qnode_peermanifest_checker | bash
```

Next time you want to retrieve the manifest, you can simply run the below command (it will be faster)

```
peer_id_base64=$(grpcurl -plaintext localhost:8337 quilibrium.node.node.pb.NodeService.GetNodeInfo | jq -r .peerId | base58 -d | base64) && grpcurl -plaintext localhost:8337 quilibrium.node.node.pb.NodeService.GetPeerManifests | grep -A 15 -B 1 "$peer_id_base64"
```

***

### Check your QUIL balance and address (after 2.0)

```
cd ~/ceremonyclient/client && ./qclient token balance
```

If you get a "No such file or directory" error, run the command below to try to rebuild the client.

```
cd ceremonyclient/client && GOEXPERIMENT=arenas go build -o qclient main.go
```

All the commands to transfer QUIL tokens are [here](https://github.com/lamat1111/Quilibrium-Node-Auto-Installer/blob/main/tokens-cli-commands.md).

***

[![image-text](https://accademiainfinita.it/extra-contents/quil-best-providers-banner-square.jpg)](https://iri.quest/quil-best-server-providers)
