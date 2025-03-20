---
icon: coin
---

# How to retrieve your coin address after a failed bridging operation

Usually, you can retrieve your coin address with the qclient token coins command. See [qclient-commands.md](qclient-commands.md "mention")

But in most cases, after a failed bridging operation, that command won't be able to query your coin address anymore.

This is because your coin has been taken out of the Quilibrium network and reserved for minting on Ethereum, but because you did not finish the bridge successfully, the coin has remained in a sort of "limbo".

This is why you should ALWAYS take note of your coin address before attempting to bridge.

So, if you can't query your coin address directly anymore (when `qclient token coins` doesn't work), here are 4 alternative methods to find your coin address.

### Method 1: First Format Decoding

This format has your coin address embedded between static strings.

#### Structure

```sh
0x7472616e73666572[your_coin_address_without_0x]1ac3290d57e064bdb5a57e874b59290226a9f9730d69f1d963600883789d6ee2
```

#### Example

```bash
# Original string:
0x7472616e73666572230f39c8656f7914f9ae86de19ab04f2377d651786eb145646209d40423573a21ac3290d57e064bdb5a57e874b59290226a9f9730d69f1d963600883789d6ee2

# Your coin address:
0x230f39c8656f7914f9ae86de19ab04f2377d651786eb145646209d40423573a2
```

> **Note**: The `0x` prefix is omitted in the cross-mint string.

### Method 2: Second Format Decoding

This format combines your Ethereum address and coin address.

#### Structure

```
[your_ethereum_address][your_coin_address_without_0x]
```

#### Example

<pre class="language-bash"><code class="lang-bash"># Original string:
0xc0ffee254729296a45a3885639AC7E10F9d54979230f39c8656f7914f9ae86de19ab04f2377d651786eb145646209d40423573a2

<strong># Breakdown:
</strong>Ethereum address: 0xc0ffee254729296a45a3885639AC7E10F9d54979
Coin address: 0x230f39c8656f7914f9ae86de19ab04f2377d651786eb145646209d40423573a2
</code></pre>

### Where to find these Strings in your terminal after a failed bridging operation

You can find the cross-mint hex strings in either:

* Your `.bash_history` file
* By using the up arrow key in your terminal to browse command history

***

### Method 3: Using Etherscan

If you have a failed transaction:

1. Go to Etherscan
2. Find your transaction
3. Click on "+ Click to show more"
4. Select "Decode Input Data"
5. Look for the `uid` value in the decoded data

***

### Method 4: Using a fresh node

{% hint style="info" %}
I have not tested this method, but it's been suggested by other that it coudl work
{% endhint %}

Spin up a fresh node, install the qclient and import the .config folder for the keys that you want to query for your coin address.

After your node begin syncing, try using the `qclient token coins` command again.

Because your node is not fully synced, it should in theory be able to "look into the past" and find your coin address even if, when querying that info from a fully synced node, you cannot see it.

***

### The bridge "Advanced" mode shows "Unknown Amount" when I paste my coin address.

If you have retrieved your coin address and are trying to finish the bridging process by pasting it directly via the "Advanced" bridge mode, you will see an "Unknown Amount" message.

This is normal, as the bridge doesn't know the amount in QUIL for that coin, since it no longer exists on the Quilibrium network but is already reserved for minting on Ethereum.

You can proceed with finishing the bridge, even if the amount is unknown, and your coin should be bridged successfully.



<table data-card-size="large" data-column-title-hidden data-view="cards" data-full-width="false"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><strong>Want to say thank you?</strong></td><td>CLICK TO DONATE</td><td><a href="../../want-to-say-thank-you.md">want-to-say-thank-you.md</a></td><td></td><td><a href="../../.gitbook/assets/donations-banner-text-1-1-B.jpg">donations-banner-text-1-1-B.jpg</a></td></tr></tbody></table>

