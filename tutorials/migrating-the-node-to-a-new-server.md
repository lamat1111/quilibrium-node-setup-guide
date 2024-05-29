# ↗️ Migrating the node to a new server

{% hint style="info" %}
This guide will only work if you use username and password to access yuor target server (which is not the best for security). If you use an SSH key, you will need to follow a more advanced method. Or you can simply setup an SSH key AFTER you have migrated the files to the target server.
{% endhint %}

1. Use the auto-installer script in this guide to install the node on the new server and let it run for 10 minutes (or for the time necessary for the root/ceremonyclient/node/.config folder to appear) then stop it with CTRL+C . _This step is clearly optional if you have already installed the node_.
2. Grab your new server IP and password.
3. Login to the old server and run this command. _Change \<NEW\_SERVER\_IP> with your new server IP and enter the new server password when requested._

```bash
scp -f ~/ceremonyclient/node/.config/keys.yml ~/ceremonyclient/node/.config/config.yml root@<NEW_SERVER_IP>:/root/ceremonyclient/node/.config/
```

{% hint style="warning" %}
ATTENTION: The command will ovewrite any existing keys.yml and config.yml files in the target server with no confirmation.

The command will move your keys.yml and config.yml to new server. For this to work the node must already be installed in the new server and the .config folder be generated.
{% endhint %}

### Manual method

Alternatively, you can migrate the files manually. If you already have a local backup of the config.yml and keys.yml files, you just need to upload them to your new server in the folder `root/ceremonyclient/node/.config` .&#x20;

You can use Termius SFTP feature or  [WinSCP](https://winscp.net/eng/index.php) to do this. With Termius SFTP feature, you can also drag and drop the files from your old server to your new server.

***

<table data-card-size="large" data-column-title-hidden data-view="cards" data-full-width="false"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><strong>The Best Server Providers for your Nodes</strong></td><td>CLICK TO SEE THEM</td><td><a href="../best-server-providers.md">best-server-providers.md</a></td><td></td><td><a href="../.gitbook/assets/best-serve-providers-banner-text-1-1-B.jpg">best-serve-providers-banner-text-1-1-B.jpg</a></td></tr><tr><td><strong>Want to say thank you?</strong></td><td>CLICK TO DONATE</td><td><a href="../want-to-say-thank-you.md">want-to-say-thank-you.md</a></td><td></td><td><a href="../.gitbook/assets/donations-banner-text-1-1-B.jpg">donations-banner-text-1-1-B.jpg</a></td></tr></tbody></table>
