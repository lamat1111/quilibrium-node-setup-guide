# ↗️ Migrating the node to a new server

{% hint style="info" %}
This guide will only work if you use username and password to access yuor target server (which is not the best for security). If you use an SSH key, you will need to follow a more advanced method. Or you can simply setup an SSH key AFTER you have migrated the files to the target server.
{% endhint %}

* Use the auto-installer script in this guide to install the node on the new server and as soon as the first node log entries appears, stop the service. _This step is clearly optional if you have already installed the node_.
* Remove the whole `node/.config` folder from the new server (this will delete your new server keys!).

```bash
rm -r ~/ceremonyclientnode/.config
```

* Grab your new server IP and password.
* Login to the old server, stop the node and run the below command. This will copy the entire `node/.config` folder from the old to the new server. \
  _Change \<NEW\_SERVER\_IP> with your new server IP and enter the new server password when requested._

{% code overflow="wrap" %}
```bash
scp -r ~/ceremonyclient/node/.config root@<NEW_SERVER_IP>:/root/ceremonyclient/node/
```
{% endcode %}

{% hint style="warning" %}
Moving files like this via a password connection poses a security risk. It's better to setup SSH keys between your servers instead.
{% endhint %}

***

<table data-card-size="large" data-column-title-hidden data-view="cards" data-full-width="false"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><strong>The Best Server Providers for your Nodes</strong></td><td>CLICK TO SEE THEM</td><td><a href="../best-server-providers.md">best-server-providers.md</a></td><td></td><td><a href="../.gitbook/assets/best-serve-providers-banner-text-1-1-B.jpg">best-serve-providers-banner-text-1-1-B.jpg</a></td></tr><tr><td><strong>Want to say thank you?</strong></td><td>CLICK TO DONATE</td><td><a href="../want-to-say-thank-you.md">want-to-say-thank-you.md</a></td><td></td><td><a href="../.gitbook/assets/donations-banner-text-1-1-B.jpg">donations-banner-text-1-1-B.jpg</a></td></tr></tbody></table>
