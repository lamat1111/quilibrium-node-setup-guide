---
description: >-
  If you're diving into the world of rental servers, it's essential to
  understand the jargon. Let's break it down into bite-sized pieces.
---

# 📄 Renting Servers Unveiled: Exploring Types and Processor Terminology

<figure><img src="../.gitbook/assets/_c62bc411-9e46-4fe2-82a1-fba2d241f657.jpeg" alt=""><figcaption></figcaption></figure>

### Types of Servers

#### VPS (Virtual Private Server)

Think of a VPS as your own little virtual corner of a larger server. It's like renting an apartment in a big building. You have your space, resources, and freedom to customize, but you're still sharing the underlying hardware with others.

#### VDS (Virtual Dedicated Server)

Now, a VDS is like having a section of a server all to yourself. It's still virtual, but you get more dedicated resources compared to a VPS. It's akin to renting a floor in that apartment building. You have more control and power, but you're still in a shared environment.

#### Bare Metal (Dedicated Server)

Imagine having the entire apartment building to yourself. That's what a bare metal server is like. It's a physical server solely dedicated to you. You have complete control over the hardware and software, without sharing resources with anyone else.

[![image-text](https://accademiainfinita.it/extra-contents/quil-best-providers-banner-square.jpg)](https://iri.quest/quil-best-server-providers)

### Processor Lingo

#### CPU (Central Processing Unit)

The CPU is the brains of the operation. It handles all the computations and instructions that make your server run. Think of it as the master chef in a kitchen, orchestrating everything to perfection.

#### vCPU (Virtual Central Processing Unit)

Now, a vCPU is like a CPU, but in a virtual environment. It's a slice of the physical CPU allocated to your virtual server. It's still powerful, but it's like having a chef sharing the kitchen with others. They can still whip up a mean dish, but they have to share the stove.

#### Cores

Cores are the individual processing units within a CPU. Think of them as the cooking burners in our kitchen analogy. The more cores you have, the more tasks your server can handle simultaneously. It's like having more chefs in the kitchen, allowing for greater multitasking prowess.

#### Why You Often Get Double vCPUs

When you rent a server with a specific number of cores, like 8 cores (8c), you'll often end up with double the number of vCPUs (16). This is because of a technology called hyper-threading, which allows each physical core to handle two virtual threads simultaneously. However, in some cases, like with certain older CPU architectures or specific configurations, you might not get double the vCPUs.

### Checking Your vCPUs on Ubuntu

To determine the total number of vCPUs on your Ubuntu server, you have a couple of options:

#### **Using `grep` Command**:&#x20;

You can use the following command to count the total number of processors, which usually corresponds to the total number of vCPUs:

```bash
grep -c ^processor /proc/cpuinfo
```

This command counts the number of lines starting with "processor" in the `/proc/cpuinfo` file, giving you the total number of processors (and thus vCPUs), assuming hyper-threading is enabled.

#### **Checking Threads per Core**:&#x20;

Alternatively, you can use the following command to find the number of threads per core, which, when multiplied by the number of cores, gives you the total number of vCPUs:

```bash
lscpu | grep "Thread(s) per core"
```

This command displays the number of threads per core, which is typically used to calculate the total number of vCPUs. However, it's important to note that if hyper-threading is disabled on your server, the total number of vCPUs will be equal to the number of physical cores, rather than the product of cores and threads per core.

By understanding these commands and the implications of hyper-threading, you can accurately determine the resources available on your server and make informed decisions about your server needs.
