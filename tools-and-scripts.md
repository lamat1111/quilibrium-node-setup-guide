# 🛠️ Tools and scripts

{% hint style="warning" %}
Follow the [safety-checks.md](safety-checks.md "mention") before running these scripts in your server
{% endhint %}

### CPUQuota remover

This script will comment out the CPUQuota line in your node service file. Go with full power 🔥

{% code overflow="wrap" %}
```bash
wget -O - https://raw.githubusercontent.com/lamat1111/quilibriumscripts/master/tools/qnode_cpuquota_remover.sh | bash
```
{% endcode %}

***

### **Extract Peer Manifests by Peer ID**

{% hint style="info" %}
_This command retrieves the manifest details for a specific peer identified by its unique peer ID. You will be probably requested to install some app before being able to execute it._

_The peer details contain much relevant info about your peer, included the "difficulty metric" a score telling you how your node is performing in the network._
{% endhint %}

If it's the first time you are trying to retrieve the manifest, run the below script. This will install the necessary apps and output the manifest last.

{% code overflow="wrap" %}
```bash
wget --no-cache -O - https://raw.githubusercontent.com/lamat1111/quilibriumscripts/main/tools/qnode_peermanifest_checker.sh | bash
```
{% endcode %}

Next time you want to retrieve the manifest, you can simply run the below command (it will be faster). This command temporarily exports some variables, this may be redundant, but it solves the gRPCurl not found error on some systems.

{% code overflow="wrap" %}
```bash
export GOROOT=/usr/local/go && export GOPATH=$HOME/go && export PATH=$GOPATH/bin:$GOROOT/bin:$PATH && peer_id_base64=$(grpcurl -plaintext localhost:8337 quilibrium.node.node.pb.NodeService.GetNodeInfo | jq -r .peerId | base58 -d | base64) && grpcurl -plaintext -max-msg-sz 5000000 localhost:8337 quilibrium.node.node.pb.NodeService.GetPeerManifests | grep -A 15 -B 1 "$peer_id_base64"
```
{% endcode %}

***

### Password authentication disabler

{% hint style="danger" %}
CAREFUL: this script will disable password connections for your server as well as root login. You will only be able to access your server via SSH keys after runnig this, so be sure you have set them up and tested them first!&#x20;
{% endhint %}

{% code overflow="wrap" %}
```bash
wget -O - https://raw.githubusercontent.com/lamat1111/password-connection-disabler/master/script | bash
```
{% endcode %}

***

### Server system cleaner

This script will clean up your system from temporary files and old log entries. It won't delete anything important for your node.

{% code overflow="wrap" %}
```bash
wget -O - https://raw.githubusercontent.com/lamat1111/quilibrium-node-auto-installer/master/tools/qnode_system_cleanup.sh | bash
```
{% endcode %}

***

<table data-card-size="large" data-column-title-hidden data-view="cards" data-full-width="false"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><strong>Want to say thank you?</strong></td><td>CLICK TO DONATE</td><td><a href="want-to-say-thank-you.md">want-to-say-thank-you.md</a></td><td></td><td><a href=".gitbook/assets/donations-banner-text-1-1-B.jpg">donations-banner-text-1-1-B.jpg</a></td></tr></tbody></table>
