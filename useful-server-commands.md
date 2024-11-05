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

***

<table data-card-size="large" data-column-title-hidden data-view="cards" data-full-width="false"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><strong>The Best Server Providers for your Nodes</strong></td><td>CLICK TO SEE THEM</td><td><a href="best-server-providers.md">best-server-providers.md</a></td><td></td><td><a href=".gitbook/assets/best-serve-providers-banner-text-1-1-B.jpg">best-serve-providers-banner-text-1-1-B.jpg</a></td></tr><tr><td><strong>Want to say thank you?</strong></td><td>CLICK TO DONATE</td><td><a href="want-to-say-thank-you.md">want-to-say-thank-you.md</a></td><td></td><td><a href=".gitbook/assets/donations-banner-text-1-1-B.jpg">donations-banner-text-1-1-B.jpg</a></td></tr></tbody></table>
