---
description: >-
  Fun fact: ~50 mil QUIL have been lost forever because people forgot to back up
  their keys :-o
---

# 🔑 Backup your private keys

After 30 minutes that then node has been running, it should have generated your keys and config files correctly. Use [WinSCP](https://winscp.net/eng/index.php) or [Termius SFTP feature](https://support.termius.com/hc/en-us/articles/4402367330201-SFTP) to navigate to the `root/ceremonyclient/node/.config` folder.&#x20;

_You may have to enable visibility for hidden files in WinSCP if you don't see the .config folder._&#x20;

Download locally your `keys.yml` and `config.yml` files. Keep them safe and do not share them with anyone! It is a good idea to put them in an encrypted folder using a free tool such as [Encrypto](https://macpaw.com/encrypto)

If you need to migrate the node elsewhere, after installing the node from scratch you just need to put these 2 files in the `root/ceremonyclient/node/.config` folder (changing the ones automatically created by the node). Here is a quick way to do this.

<details>

<summary>What does a correct "keys.yml" file look like?</summary>

```
"":
 id: ""
 type: 0
 privateKey: ""
 publicKey: ""
default-proving-key:
 id: default-proving-key
 type: 0
 privateKey: ////long-key-here///
 publicKey: ////long-key-here///
q-ratchet-idk:
 id: q-ratchet-idk
 type: 1
 privateKey: ////long-key-here///
 publicKey: ////long-key-here///
q-ratchet-spk:
 id: q-ratchet-spk
 type: 1
 privateKey: 
```

</details>

<details>

<summary>What does a correct "config.yml" file look like?</summary>

```
key:
 keyManagerType: file
 keyManagerFile:
   path: .config/keys.yml
   createIfMissing: false
   encryptionKey: ////long-key-here///
p2p:
 d: 0
 dLo: 0
 dHi: 0
 dScore: 0
 dOut: 0
 historyLength: 0
 historyGossip: 0
 dLazy: 0
 gossipFactor: 0
 gossipRetransmission: 0
 heartbeatInitialDelay: 0s
 heartbeatInterval: 0s
 fanoutTTL: 0s
 prunePeers: 0
 pruneBackoff: 0s
 unsubscribeBackoff: 0s
 connectors: 0
 maxPendingConnections: 0
 connectionTimeout: 0s
 directConnectTicks: 0
 directConnectInitialDelay: 0s
 opportunisticGraftTicks: 0
 opportunisticGraftPeers: 0
 graftFloodThreshold: 0s
 maxIHaveLength: 0
 maxIHaveMessages: 0
 iWantFollowupTime: 0s
 bootstrapPeers:
 ////list-of-bootstrap-peers-here///
 listenMultiaddr: /ip4/0.0.0.0/udp/8336/quic
 peerPrivKey: ////long-key-here///
 traceLogFile: ""
 minPeers: 0
engine:
 provingKeyId: default-proving-key
 filter: ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff
 genesisSeed: ////very-long-seed-here///
 maxFrames: -1
 pendingCommitWorkers: 4
 minimumPeersRequired: 0
 statsMultiaddr: ""
 difficulty: 0
db:
 path: .config/store
listenGrpcMultiaddr: ""
listenRESTMultiaddr: ""
logFile: ""
```

</details>
