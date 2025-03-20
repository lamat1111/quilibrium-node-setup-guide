---
icon: sack-dollar
---

# How to transfer QUIL

{% hint style="info" %}
The [q1-node-manager.md](../../q1-node-manager.md "mention") has now an option to open a "Qclient Actions" submenu with all the Qclient commands for easy of use.
{% endhint %}

**To send QUIL on the Quilibrium network you will need either:**

1. A running 2.0 node with gRPC added in your config.yml file, and Qclient 2.0.x (latest version)
2. Only Qclient 2.0.x (latest version), and using the public RPC

See [set-up-the-grpc-calls.md](../../set-up-the-grpc-calls.md "mention") to understand how to set up a local or public RPC.

See [qclient-commands.md](qclient-commands.md "mention") to understand how to use the Qclient commands

### Important Addresses

Here are the three most important types of addresses you'll encounter when using Quilibrium:

{% hint style="info" %}
**Important**: When using commands, replace the version number (2.0.2.3), OS (linux), and architecture (amd64) with your actual binary version and system specifications.
{% endhint %}

#### 1. Peer ID

* Your node's unique identifier on the Quilibrium network
* Format: Starts with "Qm..." (e.g., "QmNr69420VGcV...")
* Get it by running:

```bash
cd ~/ceremonyclient/node
./node-2.0.2.3-linux-amd64 -node-info
```

{% hint style="danger" %}
Do not send Quil to your Peer ID
{% endhint %}

#### 2. Token Address

* Your main QUIL wallet address
* Holds the total sum of your QUIL tokens
* Format: Starts with "0x..." (e.g., "0x202c3f71...")
* Get it by running:

```bash
cd ~/ceremonyclient/client
./qclient-2.0.2.3-linux-amd64 token balance
```

#### 3. Coin Addresses

* Individual addresses holding specific QUIL assets
* Each coin can hold any amount of QUIL
* Format: Starts with "0x..." (e.g., "0x25fc34h6...")
* Get them by running:

```bash
cd ~/ceremonyclient/client
./qclient-2.0.2.3-linux-amd64 token coins
```

To send QUIL you want to retrieve a Coin address and have the Wallet address of the receiver.&#x20;

In Qclient version 2.0.x it's only possible to send whole coins, starting from version 2.1.x it will be also possible to send a specific amount of QUIL.

For the commands to send QUIL, see [qclient-commands.md](qclient-commands.md "mention")



<table data-card-size="large" data-column-title-hidden data-view="cards" data-full-width="false"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><strong>The Best Server Providers for your Nodes</strong></td><td>CLICK TO SEE THEM</td><td><a href="../../best-server-providers.md">best-server-providers.md</a></td><td></td><td><a href="../../.gitbook/assets/best-serve-providers-banner-text-1-1-B.jpg">best-serve-providers-banner-text-1-1-B.jpg</a></td></tr><tr><td><strong>Want to say thank you?</strong></td><td>CLICK TO DONATE</td><td><a href="../../want-to-say-thank-you.md">want-to-say-thank-you.md</a></td><td></td><td><a href="../../.gitbook/assets/donations-banner-text-1-1-B.jpg">donations-banner-text-1-1-B.jpg</a></td></tr></tbody></table>
