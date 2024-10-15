# ✔️ Check your node info

{% hint style="warning" %}
It is better to use the [q1-node-quickstart-menu.md](q1-node-quickstart-menu.md "mention"), where all these commands are just one click away.
{% endhint %}

{% hint style="info" %}
For these commands to work, you need to  [set-up-the-grpc-calls.md](set-up-the-grpc-calls.md "mention")\
Change the "NODE\_DIR" variable according to your needs.
{% endhint %}

**Get your peerID**

```sh
NODE_DIR="$HOME/ceremonyclient/node"
NODE_BINARY=$(find "$NODE_DIR" -type f -executable -name "node-*" ! -name "*.dgst*" ! -name "*.sig*" | sort -V | tail -n 1 | xargs basename)
cd "$HOME/ceremonyclient/node" && ./$NODE_BINARY -peer-id
```

**See node info** \
PeerID - Version - Max frame - Balance\
_This can give an error on nodes that are not fully sync, but you will still see your peerID_

```bash
NODE_DIR="$HOME/ceremonyclient/node"
NODE_BINARY=$(find "$NODE_DIR" -type f -executable -name "node-*" ! -name "*.dgst*" ! -name "*.sig*" | sort -V | tail -n 1 | xargs basename)
cd "$HOME/ceremonyclient/node" && ./$NODE_BINARY -node-info
```

**Check balance**

```bash
NODE_DIR="$HOME/ceremonyclient/node"
NODE_BINARY=$(find "$NODE_DIR" -type f -executable -name "node-*" ! -name "*.dgst*" ! -name "*.sig*" | sort -V | tail -n 1 | xargs basename)
cd "$HOME/ceremonyclient/node" && ./$NODE_BINARY -balance
```

**Check node version**

```bash
journalctl -u ceremonyclient -r --no-hostname  -n 1 -g "Quilibrium Node" -o cat
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

{% code overflow="wrap" %}
```bash
wget --no-cache -O - https://raw.githubusercontent.com/lamat1111/quilibriumscripts/main/tools/qnode_peermanifest_checker.sh | bash
```
{% endcode %}

Next time you want to retrieve the manifest, you can simply run the below command (it will be faster). This command temporarily exports some variables, this may be redundant, but it solves the gRPCurl not found error on some systems.

{% code overflow="wrap" %}
```bash
export GOROOT=/usr/local/go && export GOPATH=$HOME/go && export PATH=$GOPATH/bin:$GOROOT/bin:$PATH && peer_id_base64=$(grpcurl -plaintext localhost:8337 quilibrium.node.node.pb.NodeService.GetNodeInfo | jq -r .peerId | base58 -d | base64) && grpcurl -plaintext localhost:8337 quilibrium.node.node.pb.NodeService.GetPeerManifests | grep -A 15 -B 1 "$peer_id_base64"
```
{% endcode %}

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

<table data-card-size="large" data-column-title-hidden data-view="cards" data-full-width="false"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><strong>The Best Server Providers for your Nodes</strong></td><td>CLICK TO SEE THEM</td><td><a href="best-server-providers.md">best-server-providers.md</a></td><td></td><td><a href=".gitbook/assets/best-serve-providers-banner-text-1-1-B.jpg">best-serve-providers-banner-text-1-1-B.jpg</a></td></tr><tr><td><strong>Want to say thank you?</strong></td><td>CLICK TO DONATE</td><td><a href="want-to-say-thank-you.md">want-to-say-thank-you.md</a></td><td></td><td><a href=".gitbook/assets/donations-banner-text-1-1-B.jpg">donations-banner-text-1-1-B.jpg</a></td></tr></tbody></table>
