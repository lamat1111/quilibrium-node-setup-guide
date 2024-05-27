---
description: >-
  This step is not required for the node to work. Even if you receive errors,
  your node should not be affected and keep running normally.
---

# 🔁 Set up the gRPC calls

After your node has been running for 30 minutes, run the below script to set up the gRPC calls.

{% hint style="warning" %}
_Follow the_  [safety-checks.md](safety-checks.md "mention")before running this script in your server
{% endhint %}

```bash
wget --no-cache -O - https://raw.githubusercontent.com/lamat1111/quilibriumscripts/main_new/tools/qnode_gRPC_calls_setup | bash
```

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

Find `listenGrpcMultiaddr: “”` (end of the file), and replace it with

```
listenGrpcMultiaddr: "/ip4/127.0.0.1/tcp/8337"
listenRESTMultiaddr: "/ip4/127.0.0.1/tcp/8338"
```

Find `engine:` (about the middle of the file), and paste

```
 statsMultiaddr: "/dns/stats.quilibrium.com/tcp/443" 
```

right below it, as a sub-field, with two empty spaces before the line, it will look ike this

```
engine:
  statsMultiaddr: "/dns/stats.quilibrium.com/tcp/443"
```

Save the file. \
If you are on terminal you can save by pressing CTRL + X, then Y, then ENTER

***

[![image-text](https://accademiainfinita.it/extra-contents/quil-best-providers-banner-square.jpg)](https://iri.quest/quil-best-server-providers)
