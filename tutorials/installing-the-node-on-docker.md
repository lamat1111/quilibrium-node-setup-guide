---
description: With Docker you can create a "container", install Ubuntu in it and run a node
---

# 🐳 Installing the node on Docker

{% hint style="warning" %}
This guide is outdated. Please use [this other one.](https://docs.quilibrium.space/installation/installing-node/running-with-docker)
{% endhint %}

<table data-card-size="large" data-column-title-hidden data-view="cards" data-full-width="false"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><strong>The Best Server Providers for your Nodes</strong></td><td>CLICK TO SEE THEM</td><td><a href="../best-server-providers.md">best-server-providers.md</a></td><td></td><td><a href="../.gitbook/assets/best-serve-providers-banner-text-1-1-B.jpg">best-serve-providers-banner-text-1-1-B.jpg</a></td></tr><tr><td><strong>Want to say thank you?</strong></td><td>CLICK TO DONATE</td><td><a href="../want-to-say-thank-you.md">want-to-say-thank-you.md</a></td><td></td><td><a href="../.gitbook/assets/donations-banner-text-1-1-B.jpg">donations-banner-text-1-1-B.jpg</a></td></tr></tbody></table>



## Outdated - DO NOT use

1. Download and install [Docker](https://www.docker.com/) on your computer
2. Execute Docker
3. Open your computer terminal
4. Run the commands below

Get the latest Ubuntu release

```bash
docker pull ubuntu
```

Create a docker container named “quilibrium” and install Ubuntu in it

```bash
docker run -td --name quilibrium ubuntu
```

Go to the root folder of your Ubuntu installation

```bash
docker exec -it quilibrium bash
```

Proceed with the [step-by-step installation](../archive/old-node-step-by-step-installation.md) of the node

***

## Useful Docker commands

{% hint style="info" %}
Change "quilibrium" with your container name
{% endhint %}

Create new container

```bash
docker create --name quilibrium ubuntu
```

Create new container and run it

```bash
docker run -it --name quilibrium ubuntu /bin/bash
```

Create new container in background

```bash
docker run -td --name quilibrium ubuntu /bin/bash
```

Run container

```bash
docker exec -it quilibrium /bin/bash
```

Stop container

```bash
docker stop quilibrium
```

Rename container

```bash
docker rename quilibrium mycontainernew
```
