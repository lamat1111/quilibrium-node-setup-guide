# 🔠 Useful commands

{% hint style="warning" %}
THIS IS  A NEW VERSION OF THE SERVER COMMANDS

If you are looking for the old version, you will find it here [old-useful-server-commands.md](archive/old-useful-server-commands.md "mention")
{% endhint %}

### Node service commands

Please look in [Node Service Commands](https://lamat.gitbook.io/quilibrium-node-setup-guide/node-auto-installer#node-service-commands)

***

### Node info (peerID, balance, frame number...)

Please look in [check-your-node-info.md](check-your-node-info.md "mention")

***

### Config prover pause

To avoid being penalized, use this command to send a "pause" message to the network, if your node has crashed because of hardware failure and cannot recover. Change `version-os-arch` according to your needs.

{% code overflow="wrap" %}
```sh
cd $HOME/ceremonyclient/client && ./qclient-version-os-arch config prover pause --config $HOME/ceremonyclient/node/.config
```
{% endcode %}

{% hint style="info" %}
Your qclient full binary name can be checked with\
`ls $HOME/ceremonyclient/client`
{% endhint %}

***

### Kill node process&#x20;

Use this in case you need to kill duplicated node processes that cause your node to crash.

```bash
pkill -SIGINT node
```

If this doesn't work, use `pkill -SIGKILL node` as  a last resource.

***

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

***

### Check total nodes connected to the network&#x20;

Install grpcURL

```bash
go install github.com/fullstorydev/grpcurl/cmd/grpcurl@latest
```

Run

```bash
/root/go/bin/grpcurl -plaintext -max-msg-sz 5000000 localhost:8337 quilibrium.node.node.pb.NodeService.GetPeerInfo | grep peerId | wc -l
```

***

### Node flags

You can append these flags to your node binary to execute various functions

<table><thead><tr><th width="223">Flag</th><th width="344">Description</th><th>Default</th></tr></thead><tbody><tr><td><code>-balance</code></td><td>Print the node's confirmed token balance to stdout and exit</td><td>-</td></tr><tr><td><code>-config</code></td><td>The configuration directory</td><td><code>.config</code></td></tr><tr><td><code>-core</code></td><td>Specifies the core of the process</td><td><code>0</code> (initial launcher)</td></tr><tr><td><code>-cpuprofile</code></td><td>Write CPU profile to file</td><td>-</td></tr><tr><td><code>-db-console</code></td><td>Starts the node in database console mode</td><td><code>false</code></td></tr><tr><td><code>-debug</code></td><td>Sets log output to debug (verbose)</td><td><code>false</code></td></tr><tr><td><code>-dht-only</code></td><td>Sets a node to run strictly as a DHT bootstrap peer (not full node)</td><td><code>false</code></td></tr><tr><td><code>-import-priv-key</code></td><td>Creates a new config using a specific key from the phase one ceremony</td><td>-</td></tr><tr><td><code>-integrity-check</code></td><td>Runs an integrity check on the store, helpful for confirming backups are not corrupted</td><td><code>false</code></td></tr><tr><td><code>-memprofile</code></td><td>Write memory profile after 20m to this file</td><td>-</td></tr><tr><td><code>-network</code></td><td>Sets the active network for the node (mainnet = 0, primary testnet = 1)</td><td>-</td></tr><tr><td><code>-node-info</code></td><td>Print node related information</td><td><code>false</code></td></tr><tr><td><code>-parent-process</code></td><td>Specifies the parent process pid for a data worker</td><td>-</td></tr><tr><td><code>-peer-id</code></td><td>Print the peer id to stdout from the config and exit</td><td><code>false</code></td></tr><tr><td><code>-pprof-server</code></td><td>Enable pprof server on specified address (e.g. localhost:6060)</td><td>-</td></tr><tr><td><code>-signature-check</code></td><td>Enables or disables signature validation</td><td><code>true</code> (or value of QUILIBRIUM_SIGNATURE_CHECK env var)</td></tr></tbody></table>

***

### Clean folders from repo files

{% hint style="danger" %}
Be careful! The below commands will delete some node files with no possibility of recovery
{% endhint %}

If you run your node and qclient via binary files, you don't need all the repo files, but if you installed your node a long time ago, you may still have those files there.

#### Which files do you actually require?

```
/root/ceremonyclient/
├── client/
│   ├── qclient-version-os-arch
│   ├── qclient-version-os-arch.dgst
│   ├── qclient-version-os-arch.dgst.sig.1
│   └── qclient-version-os-arch.dgst.sig... (other signatures files)
│
└── node/
    ├── .config/
    │   ├── keys.yml    (Keys)
    │   ├── config.yml  (Keys and configs)
    │   ├── store       (Proofs archive)
    │   │
    │   ├── MIGRATIONS        
    │   ├── RELEASE_VERSION
    │   ├── REPAIR  
    │   └── SELF_TEST
    │
    ├── node-version-os-arch
    ├── node-version-os-arch.dgst
    ├── node-version-os-arch.dgst.sig.1
    ├── node-version-os-arch.dgst.sig... (other signatures files)
    └── release_autorun.sh (optional)
```

{% hint style="warning" %}
If you have other extra files that you want to keep, you will need to modify the commands below according to your needs.
{% endhint %}

#### STEP 1 - Take a backup of your entire ceremonyclient folder

```sh
cp -rp $HOME/ceremonyclient $HOME/ceremonyclient.bak
```

#### STEP 2 - Delete all repo files in the ceremonyclient folder, excluding node and client folders

The below command is safe to run, it will just show what will be deleted, without deleting anything:

{% code overflow="wrap" %}
```sh
find $HOME/ceremonyclient -mindepth 1 -not \( -path "$HOME/ceremonyclient/node*" -o -path "$HOME/ceremonyclient/client*" \) -print
```
{% endcode %}

If the output looks good, run the actual command and delete the files:

{% code overflow="wrap" %}
```sh
find $HOME/ceremonyclient -mindepth 1 -not \( -path "$HOME/ceremonyclient/node*" -o -path "$HOME/ceremonyclient/client*" \) -delete
```
{% endcode %}

#### STEP 3 - Delete all repo files from the /client folder

The below command is safe to run, it will just show what will be deleted, without deleting anything:

{% code overflow="wrap" %}
```sh
find $HOME/ceremonyclient/client -mindepth 1 -not -name "qclient*" -print
```
{% endcode %}

If the output looks good, run the actual command and delete the files:

{% code overflow="wrap" %}
```bash
find $HOME/ceremonyclient/client -mindepth 1 -not -name "qclient*" -exec rm -rf {} +
```
{% endcode %}

#### STEP 4 - Delete all repo files from the /node folder

The below command is safe to run, it will just show what will be deleted, without deleting anything:

```sh
find $HOME/ceremonyclient/node -mindepth 1 -not \( \
    -path "*/\.config*" \
    -o -name "node-[0-9]*.*" \
    -o -name "release_autorun.sh" \
\) -print
```

If the output looks good, run the actual command and delete the files:

```sh
find $HOME/ceremonyclient/node -mindepth 1 -not \( \
    -path "*/\.config*" \
    -o -name "node-[0-9]*.*" \
    -o -name "release_autorun.sh" \
\) -exec rm -rf {} +
```

#### STEP 5 - Restart your node and check the log

If everything in your log looks correct, and you are sure you have not deleted unwanted files, you can proceed to delete your ceremonyclient folder backup.\
It is a good idea, though, to keep the backup for a while in case you discover later that you have deleted something you wanted to keep.

To delete the ceremonyclient backup, you can use this simple command:

```sh
rm -r $HOME/ceremonyclient.bak
```



***

<table data-card-size="large" data-column-title-hidden data-view="cards" data-full-width="false"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><strong>The Best Server Providers for your Nodes</strong></td><td>CLICK TO SEE THEM</td><td><a href="best-server-providers.md">best-server-providers.md</a></td><td></td><td><a href=".gitbook/assets/best-serve-providers-banner-text-1-1-B.jpg">best-serve-providers-banner-text-1-1-B.jpg</a></td></tr><tr><td><strong>Want to say thank you?</strong></td><td>CLICK TO DONATE</td><td><a href="want-to-say-thank-you.md">want-to-say-thank-you.md</a></td><td></td><td><a href=".gitbook/assets/donations-banner-text-1-1-B.jpg">donations-banner-text-1-1-B.jpg</a></td></tr></tbody></table>
