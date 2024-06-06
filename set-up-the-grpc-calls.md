---
description: >-
  This step is not required for the node to work. Even if you receive errors,
  your node should not be affected and keep running normally.
---

# 🔁 Set up the gRPC calls

After your node has been running for 30 minutes, run the below script to set up the gRPC calls.

{% hint style="warning" %}
_Follow the_  [safety-checks.md](safety-checks.md "mention") before running this script in your server
{% endhint %}

{% code overflow="wrap" %}
```bash
wget --no-cache -O - https://raw.githubusercontent.com/lamat1111/quilibriumscripts/master/tools/qnode_gRPC_calls_setup.sh | bash
```
{% endcode %}

If you have issues try the manual method and also see: [#troubleshooting](set-up-the-grpc-calls.md#troubleshooting "mention")

***

### How to enable gRPC calls manually

Open the file root/ceremonyclient/node/.config/config.yml on your local pc using Termius SFTP feature or WinSCP. Or if you want to edit the file via terminal, proceed like this:

Go to ceremonyclient/node folder.

```
cd ~/ceremonyclient/node
```

Run

```
sudo nano .config/config.yml
```

***

Find `listenMultiaddr: /ip4/0.0.0.0/udp/8336/quic` and replace it with

<pre><code><strong>  listenMultiaddr: /ip4/0.0.0.0/tcp/8336
</strong></code></pre>

There are two empty spaces before the line! If the line is already there, you don't need to make any change

***

Find `listenGrpcMultiaddr: ""` (end of the file), and replace it with

```
listenGrpcMultiaddr: "/ip4/127.0.0.1/tcp/8337"
listenRESTMultiaddr: "/ip4/127.0.0.1/tcp/8338"
```

***

Find `engine:` (about the middle of the file), and paste

```
 statsMultiaddr: "/dns/stats.quilibrium.com/tcp/443" 
```

right below it, as a sub-field, with two empty spaces before the line, it will look ike this

```
engine:
  statsMultiaddr: "/dns/stats.quilibrium.com/tcp/443"
```

***

Save the file. \
If you are on terminal you can save by pressing CTRL + X, then Y, then ENTER

***

### Troubleshooting

If after running the automatic script or settings things manually you have issues (for instance your node starting correctly), you may want to pull out a backup of your config.yml file and compare it with your current one. You can use [Diffinity](https://truehumandesign.se/s\_diffinity.php) to do this. &#x20;

Check for any strange differences, pieces of code you may have deleted or that the automatic script may have messed up.

***

<table data-card-size="large" data-column-title-hidden data-view="cards" data-full-width="false"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><strong>The Best Server Providers for your Nodes</strong></td><td>CLICK TO SEE THEM</td><td><a href="best-server-providers.md">best-server-providers.md</a></td><td></td><td><a href=".gitbook/assets/best-serve-providers-banner-text-1-1-B.jpg">best-serve-providers-banner-text-1-1-B.jpg</a></td></tr><tr><td><strong>Want to say thank you?</strong></td><td>CLICK TO DONATE</td><td><a href="want-to-say-thank-you.md">want-to-say-thank-you.md</a></td><td></td><td><a href=".gitbook/assets/donations-banner-text-1-1-B.jpg">donations-banner-text-1-1-B.jpg</a></td></tr></tbody></table>
