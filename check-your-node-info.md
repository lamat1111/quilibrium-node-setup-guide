# ✔️ Check your node info

{% hint style="warning" %}
With v1.4.18 some of these commands like node-info do not work anymore. Hang on while I gather intel to understand the new working commands.
{% endhint %}

After your node has been running for at least 30 minutes, run this command from your root folder to check the node info (Node version, Peer ID, QUIL balance).

```
cd ~/ceremonyclient/node && GOEXPERIMENT=arenas go run ./... -node-info
```

For this to work, you need to [set-up-the-grpc-calls.md](set-up-the-grpc-calls.md "mention")first.

If you have enabled the gRPC calls, but you still get an error, it usually just means that your node needs to run some more in order to correctly connect to the network. Retry later or use the alternative command.

#### **Alternative command to check your PeerID**

```
cd ~/ceremonyclient/node && GOEXPERIMENT=arenas go run ./... -peer-id
```

_Copy your PeerID and store it somewhere. This is the ID of your node and you can share it with others if you need to._

***

## Check your QUIL balance and address (after 2.0)

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
