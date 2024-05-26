# ✔️ Check your node info

{% hint style="warning" %}
For these commands to work, you need to  [set-up-the-grpc-calls.md](set-up-the-grpc-calls.md "mention")
{% endhint %}

`node-1.4.18-linux-amd64` will need to change depending on the node version and architecture

See Node Info:

```bash
cd ~/ceremonyclient/node && ./node-1.4.18-linux-amd64 -node-info
```

Run the DB console:

```bash
cd ~/ceremonyclient/node && ./node-1.4.18-linux-amd64 --db-console
```

Check Balances:

```bash
cd ~/ceremonyclient/node && ./node-1.4.18-linux-amd64 ./... -balance
```

{% hint style="info" %}
Copy your PeerID and store it somewhere. This is the ID of your node and you can share it with others if you need to.
{% endhint %}

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
