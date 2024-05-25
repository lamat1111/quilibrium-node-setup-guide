---
description: Install your Quilibrium node in a few clicks
---

# ⚡ Node Auto-installer

{% hint style="danger" %}
DO NOT RUN if the update to 1.4.18 has landed (check on Telegram) as the script will not work. Wait for instructions in Telegram. If you want to update your existing node to 1.4.18 you can follow this guide:  [updating-your-node.md](updating-your-node.md "mention")
{% endhint %}

{% hint style="warning" %}
This guide will work for a Linux server with Ubuntu 22.04.X - If you use a different OS you can still follow the steps, but the autoinstaller script will likely fail.\
\
If you want to install on Docker, use [this other guide](https://docs.quilibrium.space/installation/installing-node/running-with-docker).

If you are on Windows WSL, iuse the [node-step-by-step-installation.md](tutorials/node-step-by-step-installation.md "mention").
{% endhint %}

{% hint style="warning" %}
THIS IS  A NEW VERSION OF THE AUTOINSTALLER

This version will install and run your node "as a service". If you are looking for the old version (running and manging the node via a tmux session), look here [old-node-auto-installer.md](archive/old-node-auto-installer.md "mention")\
\
If you are running the node via  a tmux session and want to convert to a  service, follow [running-the-node-as-a-service.md](tutorials/running-the-node-as-a-service.md "mention"), it takes 3 minutes.
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

Your working installation folder must be "root" (not home/username) or you will likely see errors.

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

If you get stuck in the "Pink Screen of Death", asking you to restart some services, but pressing ENTER or ESC does not work, please read [escaping-the-pink-screen-of-death.md](tutorials/escaping-the-pink-screen-of-death.md "mention")

## Step 4

Install your Quilibrium node and run it as a service (this step will be included in the main auto-installer script ASAP)

```
wget -O - https://raw.githubusercontent.com/lamat1111/quilibrium-node-auto-installer/master/installer_qnode_service | bash
```

The script will create the service and start it. You will start seeing the node log at the end of the installation, to detach from it and be able to use the terminal just type CTRL +C

Now, you can safely log out from your server and the node will keep running. Wait at least 15-30 minutes to allow your node to generate your keys, then [backup-your-private-keys.md](backup-your-private-keys.md "mention")

{% hint style="info" %}
If you inspect the node log you will usually see "0 frames" for up to 5 days before the node is fully synced with the network.&#x20;

After a while you will see the "master\_frame\_head" value increase, while the "current\_head\_frame" stays to 0. This is normal until your "master\_frame\_head" reaches the latest frame in the network.&#x20;

If you suspect that your node is not connecting to the network check the server bandwidth with `speedtest-cli` and check the [troubleshooting.md](troubleshooting.md "mention") section, where it says "frame 0".

***

For faster syncing you can also see: [importing-an-existing-store-folder-for-fast-sync.md](tutorials/importing-an-existing-store-folder-for-fast-sync.md "mention")
{% endhint %}

## Step 5

Let your node run for at least 15-30 minutes, then check if your keys.yml file has been completely generated. Run the command:

```
wc -c /root/ceremonyclient/node/.config/keys.yml
```

The response should be `1252 /root/ceremonyclient/node/.config/keys.yml`.\
If the number is lower, you need to keep the node running a bit more. You can also [check here](backup-your-private-keys.md#what-does-a-correct-keys.yml-file-look-like) to see how the correct file should look like.

When your keys.yml has been generated, you can proceed to [backup-your-private-keys.md](backup-your-private-keys.md "mention"), and [set-up-the-grpc-calls.md](set-up-the-grpc-calls.md "mention")

## Step 6 (optional)

Import an existing "store" folder for fast syncing. This is optional, but without this step, your node will take up to 9 days to sync. Just run the script below. You can inspect the code [here](https://github.com/lamat1111/Quilibrium-Node-Auto-Installer/blob/main/store\_kickstart).

If you prefer to do this manually, just follow this guide: [importing-an-existing-store-folder-for-fast-sync.md](tutorials/importing-an-existing-store-folder-for-fast-sync.md "mention")

```
wget -O - https://raw.githubusercontent.com/lamat1111/quilibrium-node-auto-installer/master/store_kickstart | bash
```

{% hint style="info" %}
The store snapshot is hosted by [CherryServers](https://iri.quest/cherryservers) to help all node runners. Thank you!
{% endhint %}

## Step 7 (optional)

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

Service status

```bash
service ceremonyclient status
```
