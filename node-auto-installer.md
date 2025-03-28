---
description: Install your Quilibrium node in a few clicks
---

# ⚡ Node Auto-installer

{% hint style="danger" %}
This guide and all the linked scripts have not been reviewed for compatibility with Quilibrium 2.1.x (only reviewed up to 2.0.x). Use at your own risk!
{% endhint %}

{% hint style="warning" %}
This guide will work for a Linux server with Ubuntu 22.04 or 24.04 - If you use a different OS you can still follow the steps, but the autoinstaller script will likely fail.\
\
If you want to install on Docker, use [this other guide](https://docs.quilibrium.space/installation/installing-node/running-with-docker).

If you are on Windows WSL, use the [node-step-by-step-installation.md](tutorials/node/node-step-by-step-installation.md "mention").

If you want to install the node on Mac, use [this other guide](https://paragraph.xyz/@kingcaster/quil-node-running-guide-mac-m2-mini).
{% endhint %}

## 1 - Rent a server

Even before thinking about running a node, you should read [Is running a Quilibrium node still profitable?](https://docs.quilibrium.one/start#is-running-a-quilibrium-node-still-profitable)

**Rent or use a server with the right**  [hardware-requirements.md](hardware-requirements.md "mention") \
**Here are the**  [best-server-providers.md](best-server-providers.md "mention").

Keep in mind that nodes with better specs will earn more rewards. The ratio for optimal rewards from 1.4.18, theoretically, will be 1:2:4 (core:ram in GB:disk in GB). Your bandwidth will also matter.

VDS (Virtual Dedicated Servers) and Bare Metal (Physical dedicated Servers) are your best choice. Using a VPS (Virtual Private Server) may give you issues, as often the providers oversell the resources.\
That being said, using a VPS or a home machine may work just fine if you don't care about absolutely maximizing your rewards.

{% hint style="info" %}
If you choose to use  a VPS and you are worried your provider may block you, read  [limiting-your-cpu-usage.md](tutorials/node/managing-your-system-resources/limiting-your-cpu-usage.md "mention")
{% endhint %}

## 2 - Install Ubuntu

**Install the OS Ubuntu 22.04 or 24.04.**\
If your server has two disks, consider configuring them in "RAID 1" (typically offered by your provider). This setup mirrors one disk to the other, providing redundancy and safeguarding against data loss in case one disk fails.

From now on, you can also use the [q1-node-manager.md](q1-node-manager.md "mention") tool directly in your terminal. If this is the first node you install, I still recommend following the guide here to understand all the steps.

## 3 - Check if everything is OK

Things change fast, and we may be not fast enough to update the scripts you find from now on in the guide. So, to avoid any issue, I suggest checking [Telegram ](https://t.me/quilibriumANN)[announcements](https://t.me/quilibriumANN) and [Discord announcements](https://discord.gg/quilibrium) for any last minute issue or update. If there is something you don't understand, ask in the chats.

If everything looks fine, proceed to the next step.

{% hint style="info" %}
Even if you run the scripts but they don't work because there was a last minute update, don't worry. The worst that can happen is that they will give you an error.&#x20;
{% endhint %}

## 4 - Install the Quilibrium Node

#### Recommendations

Run the auto-installer script on your server (OS must be Ubuntu 22.04 or 24.04). I recommend you to use [Termius](https://termius.com/) to login and run all the commands. Be sure that you are logging in via port 22 (default with most server providers). You will need sudo privileges.

If you prefer to not automate this step you can do it manually step-by-step, simply follow the[node-step-by-step-installation.md](tutorials/node/node-step-by-step-installation.md "mention")

{% hint style="info" %}
If the script fails and stops, you can try to run it again (if you understand why it stopped, then try to solve the issue first, of course). If you still receive an error, you may want to proceed manually, step by step, instead of using the auto-installer. Here is the [node-step-by-step-installation.md](tutorials/node/node-step-by-step-installation.md "mention")
{% endhint %}

If you get stuck in the "Pink Screen of Death", asking you to restart some services, but pressing ENTER or ESC does not work, please read [escaping-the-pink-screen-of-death.md](tutorials/node/escaping-the-pink-screen-of-death.md "mention")

#### Install your Quilibrium node and run it as a service.

{% hint style="warning" %}
Follow the [safety-checks.md](safety-checks.md "mention") before running this script in your server. You can inspect the code[ here](https://github.com/lamat1111/Quilibrium-Node-Auto-Installer/blob/1.4.18/qnode_service_installer).&#x20;
{% endhint %}

{% code overflow="wrap" %}
```bash
wget --no-cache -O - https://raw.githubusercontent.com/lamat1111/QuilibriumScripts/master/qnode_service_installer.sh | bash
```
{% endcode %}

The script will upgrade your machine, install some necessary apps, set some security features, install the Node, the Qclient, and set everything for you.&#x20;

After this step is recommended to reboot your server and login again.

Wait at least 15-30 minutes to allow your node to generate your keys, then [backup-your-private-keys.md](backup-your-private-keys.md "mention")

## 5 - Let the node run

After rebooting and logging in again, let your node run for at least 15-30 minutes, then check if your keys.yml file has been completely generated. Run the command:

```
wc -c /root/ceremonyclient/node/.config/keys.yml
```

The response should be `1252 /root/ceremonyclient/node/.config/keys.yml`.\
If the number is lower, you need to keep the node running a bit more. You can also [check here](backup-your-private-keys.md#what-does-a-correct-keys.yml-file-look-like) to see how the correct file should look like.

When your keys.yml has been generated, you can proceed to [backup-your-private-keys.md](backup-your-private-keys.md "mention"), and [set-up-the-grpc-calls.md](set-up-the-grpc-calls.md "mention")

After 1.4.19, ensure consistent daily backups of the entire `node/.config/` folder too. Why? Read [backup-your-node.md](backup-your-node.md "mention")

## 6 - Set up SSH keys (optional)

This is optional, but recommended! [set-up-ssh-keys.md](tutorials/node/set-up-ssh-keys.md "mention") and disable the password connection.

***

## Node service commands

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

{% hint style="info" %}
More commands in  [check-your-node-info.md](check-your-node-info.md "mention") and in  [useful-server-commands.md](useful-server-commands.md "mention").
{% endhint %}

***

<table data-card-size="large" data-column-title-hidden data-view="cards" data-full-width="false"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><strong>Want to say thank you?</strong></td><td>CLICK TO DONATE</td><td><a href="want-to-say-thank-you.md">want-to-say-thank-you.md</a></td><td></td><td><a href=".gitbook/assets/donations-banner-text-1-1-B.jpg">donations-banner-text-1-1-B.jpg</a></td></tr></tbody></table>
