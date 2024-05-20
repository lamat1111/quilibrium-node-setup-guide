---
description: Install your Quilibrium node in a few clicks
---

# ⚡ Node Auto-installer

{% hint style="info" %}
Compatible with Quilibrium 1.4.17
{% endhint %}

{% hint style="warning" %}
This guide will work for a Linux server with Ubuntu 22.04.X - If you use a different OS you can still follow the steps, but the autoinstaller script will likely fail.
{% endhint %}

{% hint style="warning" %}
THIS IS  A NEW VERSION OF THE AUTOINSTALLER

This version will install and run your node "as a service". If you are looking for the old version (running and manging the node via a tmux session), look here [old-node-auto-installer.md](archive/old-node-auto-installer.md "mention")
{% endhint %}

## Step 1

**Rent or use a server with the right** [hardware-requirements.md](hardware-requirements.md "mention") **Here are the** [best-server-providers.md](best-server-providers.md "mention").

Keep in mind that nodes with better specs will earn more rewards. The ratio for optimal rewards from 1.4.18, theoretically, will be 1:2:4 (core:ram in GB:disk in GB). Your bandwidth will also matter.

VDS (Virtual Dedicated Servers) and Bare Metal (Physical dedicated Servers) are your best choice. Using a VPS (Virtual Private Server) may give you issues, as often the providers oversell the resources.\
That being said, using a VPS or a home machine may work just fine if you don't care about absolutely maximizing your rewards.

## Step 2

**Install the OS Ubuntu 22.04.X.**\
If your server has two disks, consider configuring them in "RAID 1" (typically offered by your provider). This setup mirrors one disk to the other, providing redundancy and safeguarding against data loss in case one disk fails.

## Step 3

Run the auto-installer script on your server (OS must be Ubuntu 22.04.X). I suggest you to use [Termius](https://termius.com/) to login and run all the commands. Be sure that you are logging in via port 22 (default with most server providers).

If you prefer to not automate this step you can do it manually step-by-step, simply follow the[node-step-by-step-installation.md](tutorials/node-step-by-step-installation.md "mention")

```
wget -O - https://raw.githubusercontent.com/lamat1111/quilibrium-node-auto-installer/master/installer_2 | bash
```

{% hint style="success" %}
_This script is simply packing all the necessary steps and the required applications in a one-click solution. It won't install your node (you will need to do it manually for security reasons), but it will prepare your server very quickly. You can inspect the source code_ [_here_](https://github.com/lamat1111/Quilibrium-Node-Auto-Installer/blob/main/installer\_2)_. If you are not familiar with code, you can simply copy/paste the whole code in a chatbot such as ChatGPT (or any open-source alternative ;-) and ask them to explain it to you step by step._
{% endhint %}

{% hint style="info" %}
If the script fails and stops, you can try to run it again (if you understand why it stopped, then try to solve the issue first, of course). If you still receive an error, you may want to proceed manually, step by step, instead of using the auto-installer. Here is the [node-step-by-step-installation.md](tutorials/node-step-by-step-installation.md "mention")
{% endhint %}

After this step is recommended to reboot your server and login again.

## Step 4

Install your Quilibrium node and run it as a service (this step will be included in the main auto-installer script ASAP)

```
wget -O - https://raw.githubusercontent.com/lamat1111/quilibrium-node-auto-installer/master/installer_qnode_service | bash
```

The script will create the service and start it.&#x20;

After that, you can safely log out from your server and the node will keep running. Wait at least 30 minutes to allow your node to generate your keys, then [backup-your-private-keys.md](backup-your-private-keys.md "mention")

{% hint style="info" %}
If you inspect the node log you will usually see "0 frames" for up to 5 days before the node is fully synced with the network.&#x20;

After a while you will see the "master\_frame\_head" value increase, while the "current\_head\_frame" stays to 0. This is normal until your "master\_frame\_head" reaches the latest frame in the network.&#x20;

If you suspect that your node is not connecting to the network check the server bandwidth with `speedtest-cli` and check the [troubleshooting.md](troubleshooting.md "mention") section, where it says "frame 0".

***

For faster syncing you can also see: [importing-an-existing-store-folder-for-fast-sync.md](tutorials/importing-an-existing-store-folder-for-fast-sync.md "mention")
{% endhint %}

## Step 6

Let your node run for at least 30 minutes, then check if your keys.yml file has been completely generated. Run the command:

```
wc -c /root/ceremonyclient/node/.config/keys.yml
```

The response should be `1252 /root/ceremonyclient/node/.config/keys.yml`.\
If the number is lower, you need to keep the node running a bit more. You can also [check here](backup-your-private-keys.md#what-does-a-correct-keys.yml-file-look-like) to see how the correct file should look like.

When your keys.yml has been generated, you can proceed to [backup-your-private-keys.md](backup-your-private-keys.md "mention"), and [set-up-the-grpc-calls.md](set-up-the-grpc-calls.md "mention")

## Step 8

This is optional, but recommended! [set-up-ssh-keys.md](set-up-ssh-keys.md "mention")and disable the password connection. Here is a guide to do this.\
To enhance even more your server security, you may install and setup _Fail2ban_, here is [a guide](https://www.digitalocean.com/community/tutorials/how-to-protect-ssh-with-fail2ban-on-ubuntu-20-04).

If you reboot your server, you will need to start the node service again with this command.

***

## Node commands

Start service

```bash
service ceremonyclient start
```

Stop service

```bash
service ceremonyclient stop
```

Restart service

```bash
service ceremonyclient restart
```

View node log

```bash
sudo journalctl -u ceremonyclient.service -f --no-hostname -o cat
```

