# ↗️ Migrating the node to a new server

{% hint style="info" %}
The [q1-node-manager.md](../../q1-node-manager.md "mention") has an option to backup your node to StorJ and another one to restore it. Using those options you could also easily migrate the node to another machine.\
\
If you did not backed up the node on Storj, then follow the guides below.
{% endhint %}

{% hint style="warning" %}
SInce v2.0 Node "store" folders are interchangeable. This means that the fastest way to move a node to another machine is the following:\
\
\- Install node on new machine and let it sync to the latest frame (or restore a "store" folder snapshot if you have it)\
\- Stop new machine node\
\- Import config.yml and keys.yml from old to new machine\
\- Stop old machine node\
\- Restart new machine node\
\
Be sure to have a MIGRATIONS file in the node/.config folder of the new machine.
{% endhint %}

<details>

<summary>You have access to the source and target servers and your .config folder is on the source server</summary>

This guide will only work if you use username and password to access your target server (which is not the best for security). If you use an SSH key, you will need to follow a more advanced method. Or you can simply setup an SSH key AFTER you have migrated the files to the target server.

* Use the auto-installer script in this guide to install the node. _This step is clearly optional if you have already installed the node_.
* Remove the whole `node/.config` folder from the new server (this will delete your new server keys!).

```bash
rm -r ~/ceremonyclient/node/.config
```

* Grab your new server IP and password.
* Login to the old server, stop the node and run the below command. This will copy the entire `node/.config` folder from the old to the new server. \
  &#xNAN;_&#x43;hange \<NEW\_SERVER\_IP> with your new server IP and enter the new server password when requested._

{% code overflow="wrap" %}
```bash
scp -r ~/ceremonyclient/node/.config root@<NEW_SERVER_IP>:/root/ceremonyclient/node/
```
{% endcode %}

_Moving files like this via a password connection poses a security risk. It's better to setup SSH keys between your servers instead._

</details>

<details>

<summary>You only have access to the target server and your .config folder is on your local PC</summary>

* Use the auto-installer script in this guide to install the node on the new server.. _This step is clearly optional if you have already installed the node_.
* Remove the whole `node/.config` folder from the new server (this will delete your new server keys!).

```sh
rm -r ~/ceremonyclient/node/.config
```

* Upload your local .config folder to /ceremonyclient/node/.config
* Restart the node

</details>

<details>

<summary>Complete manual process</summary>

_This is the simplest migration process if you don't want to use the node auto-installer. But you will have to create the node service manually._

Login to your target server&#x20;

Upload your .config folder to \~/backup/

Follow the [node-step-by-step-installation.md](node-step-by-step-installation.md "mention") to install the node manually

Go to the node folder

{% code overflow="wrap" %}
```sh
cd ceremonyclient/node
```
{% endcode %}

Copy your .config folder to the node folder

{% code overflow="wrap" %}
```sh
cp -r ~/backup/.config  /.config
```
{% endcode %}

Start the node

</details>

***



<table data-card-size="large" data-column-title-hidden data-view="cards" data-full-width="false"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><strong>The Best Server Providers for your Nodes</strong></td><td>CLICK TO SEE THEM</td><td><a href="../../best-server-providers.md">best-server-providers.md</a></td><td></td><td><a href="../../.gitbook/assets/best-serve-providers-banner-text-1-1-B.jpg">best-serve-providers-banner-text-1-1-B.jpg</a></td></tr><tr><td><strong>Want to say thank you?</strong></td><td>CLICK TO DONATE</td><td><a href="../../want-to-say-thank-you.md">want-to-say-thank-you.md</a></td><td></td><td><a href="../../.gitbook/assets/donations-banner-text-1-1-B.jpg">donations-banner-text-1-1-B.jpg</a></td></tr></tbody></table>
