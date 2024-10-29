---
icon: coin
---

# How to retrieve your coin address

Usually, you can retrieve your coin address with the qclient token coins command. See [qclient-commands-for-token-transfers.md](../qclient-commands-for-token-transfers.md "mention")

But in some cases, after a failed bridging operation, that command won't be able to query your coin address anymore.

If you can't query your coin address directly (when `qclient token coins` doesn't work), you can decode it from the cross-mint hex data.&#x20;

Here are 4 methods to find your address:

### Method 1: First Format Decoding

This format has your coin address embedded between static strings.

#### Structure

```
0x7472616e73666572[your_coin_address_without_0x]1ac3290d57e064bdb5a57e874b59290226a9f9730d69f1d963600883789d6ee2
```

#### Example

```
Original string:
0x7472616e73666572230f39c8656f7914f9ae86de19ab04f2377d651786eb145646209d40423573a21ac3290d57e064bdb5a57e874b59290226a9f9730d69f1d963600883789d6ee2

Your coin address:
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

```
Original string:
0xc0ffee254729296a45a3885639AC7E10F9d54979230f39c8656f7914f9ae86de19ab04f2377d651786eb145646209d40423573a2

Breakdown:
Ethereum address: 0xc0ffee254729296a45a3885639AC7E10F9d54979
Coin address: 0x230f39c8656f7914f9ae86de19ab04f2377d651786eb145646209d40423573a2
```

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

