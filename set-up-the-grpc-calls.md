---
description: >-
  This step is not required for the node to work. Even if you receive errors,
  your node should not be affected and keep running normally.
---

# 🔁 Set up the gRPC calls

After your node has been running for 30 minutes, run the below script to set up the gRPC calls.

```bash
wget -O - https://raw.githubusercontent.com/lamat1111/quilibrium-node-auto-installer/master/installer-gRPC-calls | bash
```

### How to enable gRPC calls manually

Open the file root/ceremonyclient/node/.config/config.yml on your local pc using Termius SFTP feature or WinSCP

Find `listenGrpcMultiaddr: “”` (end of the file), and replace it with

```
listenGrpcMultiaddr: /ip4/127.0.0.1/tcp/8337
```

Find `engine:` (about the middle of the file), and paste

```
 statsMultiaddr: "dns/stats.quilibrium.com/tcp/443" 
```

right below it, with two empty spaces before the line

Save the file

***

[![image-text](https://accademiainfinita.it/extra-contents/quil-best-providers-banner-square.jpg)](https://iri.quest/quil-best-server-providers)
