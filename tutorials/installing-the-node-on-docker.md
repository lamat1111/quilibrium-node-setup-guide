---
description: With Docker you can create a "container", install Ubuntu in it and run a node
---

# 🐳 Installing the node on Docker

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

Proceed with the [step-by-step installation](../archive/node-step-by-step-installation.md) of the node

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
