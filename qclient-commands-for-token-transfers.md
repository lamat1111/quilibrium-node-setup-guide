# 🔀 qclient commands for token transfers

With the release of Quilibrium 2.0, the node application comes with the _/client_ folder for you to have better visibility on your node's conditions, earned rewards and perform transfer transactions.

### How to run the qclient commands

{% hint style="info" %}
For the commands to work you need to be in your "ceremonyclient/client" folder:\
`cd ~/ceremonyclient/client/` for default node installations, or in the folder where your client binary is located.
{% endhint %}

To run the qclient commands, you need to execute your qclient binary, followed by the command and optional flags. One important flag is `--config /path/to/config`, without this flag the command will fail, unless you run it from inside the "node" directory (or whichever directory contains your .confg folder).\
\
Here is an example of a command:

```sh
./qclient-version-os-arch command --config /path/to/config
```

This translates to the following for v2.0.1 on Linux:

{% code overflow="wrap" %}
```bash
./qclient-2.0.1-linux-amd64 token balance --config $HOME/ceremonyclient/node/.config
```
{% endcode %}

Every time you see "qclient" in the commands below, it actually refers to something like `./qclient-version-os-arch`

{% hint style="warning" %}
COMMON ISSUE WITH QCLIENT COMMANDS\
Most Qclient command errors stem from config path problems. \
When using full paths in your commands, like `--config /root/ceremonyclient/node/.config`, you may want to update your config.yml accordingly. \
Change `path: .config/store` to include your full path, e.g. `/root/ceremonyclient/node/.config/store` and try again.
{% endhint %}

### Querying Balance

The command line tool accepts arguments in either decimal (xx.xxxxx) format or raw unit (0x00000) format. Note that raw units are a multiple of QUIL: 1 QUIL = 0x1DCD65000 units

Command:

```
qclient token balance
```

Response:

{% code overflow="wrap" %}
```bash
$ qclient token balance
50.0 QUIL (Account 0x23c0f371e9faa7be4ffedd616361e0c9aeb776ae4d7f3a37605ecbfa40a55a90)
```
{% endcode %}

### Querying Individual Coins

Users may want to view the individual coins:

Command:

```
qclient token coins
```

Response:

{% code overflow="wrap" %}
```bash
$ qclient token coins
25.0 QUIL (Coin 0x1148092cdce78c721835601ef39f9c2cd8b48b7787cbea032dd3913a4106a58d)
25.0 QUIL (Coin 0x2dda9dc9770a1e5a01974fcd5af2a77147d0f19fb4935a1df677ec6050be0a9e)
```
{% endcode %}

### Creating a Pending Transaction

Quilibrium's token application has two modes: a two-stage transfer/accept (or reject), or a single-stage mutual transfer.

#### Commands in Qclient 2.0.x

{% hint style="warning" %}
* In Qclient version 2.0.x it's only possible to send an entire coin, not an amount. The amount feature will be added in version 2.1.x
* In Qclient 2.0.x the transaction will be immediately sent. You will not receive any transation ID and the receiver will not have to approve it.
* In Qclient 2.0.x specifying a refund account is not supported
{% endhint %}

Here is the command you run in qclient 2.0.x

{% code overflow="wrap" %}
```bash
qclient token transfer <ToAccount> <OfCoin>
```
{% endcode %}

#### Commands in Qclient 2.1.x

From Qclient 2.1.x you can send more complex commands and you will receive a more complete response

{% code overflow="wrap" %}
```bash
qclient token transfer <ToAccount> <RefundAccount> <Amount|OfCoin>

<Amount> QUIL (Pending Transaction 0x0382e4da0c7c0133a1b53453b05096272b80c1575c6828d0211c4e371f7c81bb)
```
{% endcode %}

Omitting the RefundAccount will simply provide your own originating account. The option to specify exists so that you can maintain anonymity when sending by creating a fresh account to receive the refund. The RefundAccount cannot be the same as the ToAccount.

The first is a user-friendly version of a transfer, similar to what account-based networks like Ethereum and Solana do, where you operate on a balance. Behind the scenes, the client is actually splitting and/or merging coins as needed to create the required amount to send as a discrete coin. The second is an application-aware version of a transfer, similar to what UTXO-based networks like Bitcoin do, where you operate on the raw coin balance under a specific address. If you have good reason to manage coins separately (yet under the control of the same managing account), you will want to use the second option in conjunction with split/merge operations if needed:

### Splitting and merging commands

{% code overflow="wrap" %}
```sh
$ qclient token split <OfCoin> <LeftAmount> <RightAmount>

<LeftAmount> QUIL (Coin 0x024479f49f03dc53fd702198cd9b548c9e96004e19ef6a4e9c5211a9795ba34d)
<RightAmount> QUIL (Coin 0x0140e01731256793bba03914f3844d645fbece26553acdea8ac4de4d84f91690)
```
{% endcode %}

{% code overflow="wrap" %}
```bash
$ qclient token merge <LeftCoin> <RightCoin>

<Total> QUIL (Coin 0x151f4ae225e20759077e1724e4c5d0feae26c477fd10d728dfea962eec79b83f)
```
{% endcode %}

### Accepting a Pending Transaction

{% hint style="warning" %}
Not available in In Qclient 2.0.x\
Transaction will be recieved without the need for approval.
{% endhint %}

To accept a pending transaction, you simply run:

{% code overflow="wrap" %}
```bash
$ qclient token accept <PendingTransaction>

<Amount> QUIL (Coin 0x2688997f2776ab5993894ed04fcdac05577cf2494ddfedf356ebf8bd3de464ab)
```
{% endcode %}

The same applies for rejecting a pending transaction

{% code overflow="wrap" %}
```bash
$ qclient token reject <PendingTransaction>

<Amount> QUIL (PendingTransaction 0x27fff099dee515ece193d2af09b164864e4bb60c19eb6719b5bc981f92151009)
```
{% endcode %}

This creates a separate pending transaction because if the refund address is specified by the originator, and were they to specify another of your own addresses, it would be no different from accepting.

### Performing a Mutual Transfer

{% hint style="warning" %}
Not available in In Qclient 2.0.x
{% endhint %}

Pending transactions introduce friction, but without that friction, users can be spammed coins they don't want, or sent coins from an address they do not wish to interact with. If both parties agree in advance to transact, they can perform a mutual transfer, where both parties must be online, but can avoid having to deal with the two-phase transaction. This is great for maintaining privacy (each party's account is private) as well as ensuring a timely completion of a transaction:

On the receiver's side:

{% code overflow="wrap" %}
```bash
$ qclient token mutual-receive <ExpectedAmount>
Rendezvous: 0x2ad567e4fc1ac335a8d3d6077de2ee998aff996b51936da04ee1b0f5dc196a4f
Awaiting sender...
```
{% endcode %}

and after the sender connects:

{% code overflow="wrap" %}
```bash
Awaiting sender... OK
<Amount> QUIL (Coin 0x0525c76ecdc6ef21c2eb75df628b52396adcf402ba26a518ac395db8f5874a82)
```
{% endcode %}

On the sender's side:

```bash
$ qclient token mutual-transfer <Rendezvous> <Amount>

Confirming rendezvous... OK
<Amount> QUIL (Coin [private])
```

or if using the raw Coin address:

```bash
$ qclient token mutual-transfer <Rendezvous> <OfCoin>

Confirming rendezvous... OK
<Amount> QUIL (Coin [private])
```

This will likely be the first unique experience Quilibrium provides to users already familiar with other networks, as privacy preservation is an immediately obvious and first class experience here by showing the user what it can (or _cannot_) see.

### Claiming Rewards

Tokens issued after 1.5.0 are issued by nodes providing their proofs to the Mint Authority functionality of the token application. Claiming those rewards can be configured to be performed automatically (default, generates a new Coin every claim and merges them), or in lump sums at intervals, manually. It is recommended for ease of management that the defaults are applied, so that in the event of hardware failure no rewards go unclaimed.

If you wish to do it manually, however, you will need to run:

{% code overflow="wrap" %}
```bash
$ qclient token mint all

<Amount> QUIL (Coin 0x162ad88c319060b4f5ea6dbf9a0c2cd82d3d70dfc22d5fc99ca5371083d68416)
```
{% endcode %}

***

<table data-card-size="large" data-column-title-hidden data-view="cards" data-full-width="false"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><strong>The Best Server Providers for your Nodes</strong></td><td>CLICK TO SEE THEM</td><td><a href="best-server-providers.md">best-server-providers.md</a></td><td></td><td><a href=".gitbook/assets/best-serve-providers-banner-text-1-1-B.jpg">best-serve-providers-banner-text-1-1-B.jpg</a></td></tr><tr><td><strong>Want to say thank you?</strong></td><td>CLICK TO DONATE</td><td><a href="want-to-say-thank-you.md">want-to-say-thank-you.md</a></td><td></td><td><a href=".gitbook/assets/donations-banner-text-1-1-B.jpg">donations-banner-text-1-1-B.jpg</a></td></tr></tbody></table>
