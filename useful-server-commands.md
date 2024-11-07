# 🔠 Useful server commands

{% hint style="warning" %}
THIS IS  A NEW VERSION OF THE SERVER COMMANDS

If you are looking for the old version, you will find it here [old-useful-server-commands.md](archive/old-useful-server-commands.md "mention")
{% endhint %}

### Node service commands

Please look in [Node Service Commands](https://lamat.gitbook.io/quilibrium-node-setup-guide/node-auto-installer#node-service-commands)

### Node info (peerID, balance, frame number...)

Please look in [check-your-node-info.md](check-your-node-info.md "mention")

### Prover pause

Use this to send a "pause" message to the network, right after stopping your node for maintenance, to avoid being penalized. Change `version-os-arch` according to your needs

{% code overflow="wrap" %}
```sh
cd $HOME/ceremonyclient/client && ./qclient-version-os-arch prover pause --config $HOME/ceremonyclient/node/.config
```
{% endcode %}

{% hint style="info" %}
Your qclient full binary name can be checked with\
`ls $HOME/ceremonyclient/client`
{% endhint %}

### Bypass signature check

{% hint style="danger" %}
Running the binary this way can be dangerous if you are not sure of it's provenance.
{% endhint %}

If you want to run the node or qclient binary bypassing the signature check, use the flag `--signature-check=false` at the end of your commands.

### Kill node process&#x20;

Use this in case you need to kill duplicated node processes that cause your node to crash.

```bash
pkill -SIGINT node
```

If this doesn't work, use `pkill -SIGKILL node` as  a last resource.

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

### Check total nodes connected to the network&#x20;

Install grpcURL

```bash
go install github.com/fullstorydev/grpcurl/cmd/grpcurl@latest
```

Run



```bash
/root/go/bin/grpcurl -plaintext -max-msg-sz 5000000 localhost:8337 quilibrium.node.node.pb.NodeService.GetPeerInfo | grep peerId | wc -l
```

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
