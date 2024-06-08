---
description: Install your Quilibrium node in a few clicks
---

# ⚡ OLD - Node Auto-installer

{% hint style="danger" %}
NOT COMPATIBLE with Quilibrium 1.4.18
{% endhint %}

{% hint style="warning" %}
This guide will work for a Linux server with Ubuntu 22.04.X - If you use a different OS you can still follow the steps, but the autoinstaller script will likely fail.
{% endhint %}

## Step 1

**Rent or use a server with the right** [**hardware requirements**](../hardware-requirements.md)**. Here are the** [**best server providers.**](../best-server-providers.md)

Keep in mind that nodes with better specs will earn more rewards. The ratio for optimal rewards from 1.4.18, theoretically, will be 1:2:4 (core:ram in GB:disk in GB). Your bandwidth will also matter.

VDS (Virtual Dedicated Servers) and Bare Metal (Physical dedicated Servers) are your best choice. Using a VPS (Virtual Private Server) may give you issues, as often the providers oversell the resources.\
That being said, using a VPS or a home machine may work just fine if you don't care about absolutely maximizing your rewards.

## Step 2

**Install the OS Ubuntu 22.04.X.**\
If your server has two disks, consider configuring them in "RAID 1" (typically offered by your provider). This setup mirrors one disk to the other, providing redundancy and safeguarding against data loss in case one disk fails.

## Step 3

Run the auto-installer script on your server (OS must be Ubuntu 22.04.X). I suggest you to use [Termius](https://termius.com/) to login and run all the commands. Be sure that you are logging in via port 22 (default with most server providers).

If you prefer to not automate this step you can do it manually step-by-step, simply follow [this tutorial](old-node-step-by-step-installation.md).

```
wget -O - https://raw.githubusercontent.com/lamat1111/quilibrium-node-auto-installer/master/installer | bash
```

{% hint style="success" %}
_This script is simply packing all the necessary steps and the required applications in a one-click solution. It won't install your node (you will need to do it manually for security reasons), but it will prepare your server very quickly. You can inspect the source code_ [_here_](https://github.com/lamat1111/Quilibrium-Node-Auto-Installer/blob/main/installer)_. If you are not familiar with code, you can simply copy/paste the whole code in a chatbot such as ChatGPT (or any open-source alternative ;-) and ask them to explain it to you step by step._
{% endhint %}

{% hint style="info" %}
If the script fails and stops, you can try to run it again (if you understand why it stopped, then try to solve the issue first, of course). If you still receive an error, you may want to proceed manually, step by step, instead of using the auto-installer. Here is the [step by step guide](old-node-step-by-step-installation.md) you can follow.
{% endhint %}

After this step is recommended to reboot your server and login again.

## Step 4

Install your Quilibrium node (this step will be included in the auto-installer script ASAP)

Clone the ceremony client from GitHub  (after 1.4.17 this step may change, ask in the [Telegram group](https://t.me/quilibrium))

```bash
cd ~ && git clone https://github.com/QuilibriumNetwork/ceremonyclient.git
```

Build the Quilibrium client (for transferring tokens)

```bash
cd ~/ceremonyclient/client && GOEXPERIMENT=arenas go build -o qclient main.go
```

## Step 5

Run the command below. This will go to the node folder, create a persistent shell (session), start the node via the _qnode\_restart_ script (more info about this script below) and detach from the session again. You won't see any output after running the command, but you can move to Step 6.

```bash
tmux new-session -d -s quil 'export PATH=$PATH:/usr/local/go/bin && cd ~/ceremonyclient/node && ~/scripts/qnode_restart.sh'
```

<details>

<summary>Alternative: step by step commands</summary>

You can also run these command one after the other if you prefer.

```
cd ceremonyclient/node 
```

```
tmux new-session -s quil 
```

```
~/scripts/qnode_restart.sh
```

To detach from tmux press CTRL+B then D. Now you can safely logout from your server and the node will keep running in its persistent shell.\
To reattach to the tmux session and see your node log, just use `tmux a -t quil`. You can recognize when you are inside your tmux session because there will be a green bar at the bottom of the screen.\
To stop the node, from inside tmux click CTRL+C\
To restart the node, from inside tmux run `./poor_mans_cd.sh`

</details>

{% hint style="info" %}
The qnode\_restart.sh is a script used to run the node. It will restart it automatically if it gets killed.
{% endhint %}

{% hint style="warning" %}
If you ever reboot your server, you will need to go through this step 5 again to start the node from scratch (to avoid this, in [Useful Server Commands](old-useful-server-commands.md#create-cronjob-to-run-the-node-automatically-after-a-reboot) there is a command to setup an automation (AKA cronjob) that will start your node automatically after any server reboot :-)
{% endhint %}

## Step 6

**You are done!** Now you can safely log out from your server and the node will keep running in its persistent shell.\
\
If you want to see your node log, you can reattach to the tmux session with `tmux a -t quil`\
Once you are in the tmux session a green bar will appear at the bottom of the screen, to detach from tmux press CTRL+B then D.

It will usually take 10 minutes before you will begin to see new log entries in the node log. And it will take up to 30 minutes before your private keys will be created correctly, so that you can back up them.

{% hint style="info" %}
If you inspect the node log you will usually see "0 frames" for up to 72+ hours before the node is fully synced with the network.&#x20;

After a while you will see the "master\_frame\_head" value increase, while the "current\_head\_frame" stays to 0. This is normal until your "master\_frame\_head" reaches the latest frame in the network.&#x20;

If you suspect that your node is not connecting to the network check the server bandwidth with `speedtest-cli` and check the [Troubleshooting section](../troubleshooting.md) where it says "frame 0".

***

For faster syncing you can also [import an existing store folder](importing-an-existing-store-folder-for-fast-sync.md).
{% endhint %}

## Step 7

Let your node run for at least 30 minutes, then check if your keys.yml file has been completely generated. Run the command:

```
wc -c /root/ceremonyclient/node/.config/keys.yml
```

The response should be `1252 /root/ceremonyclient/node/.config/keys.yml`.\
If the number is lower, you need to keep the node running a bit more. You can also [check here](../backup-your-private-keys.md#what-does-a-correct-keys.yml-file-look-like) to see how the correct file should look like.

When your keys.yml has been generated, you can proceed to [back up your keys.yml and config.yml files](../backup-your-private-keys.md), and [set up your gRPC calls](../set-up-the-grpc-calls.md).

## Step 8

This is optional, but recommended! [Set up SSH keys to connect to your server](../tutorials/set-up-ssh-keys.md) and disable the password connection. Here is a guide to do this.\
To enhance even more your server security, you may install and setup _Fail2ban_, here is [a guide](https://www.digitalocean.com/community/tutorials/how-to-protect-ssh-with-fail2ban-on-ubuntu-20-04).

## Step 9

When you need to update your node, follow these steps:&#x20;

1 - kill your tmux session

```bash
tmux kill-session -t quil
```

2- update the node: update method after 1.4.17 is still unclear, stay tuned to the various channels!

3 - create a new tmux session and run the qnode\_restart script (you will not see any output after running the command).

```bash
tmux new-session -d -s quil 'export PATH=$PATH:/usr/local/go/bin && cd ~/ceremonyclient/node && ~/scripts/qnode_restart.sh'
```
