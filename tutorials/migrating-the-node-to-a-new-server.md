# ↗️ Migrating node to a new server

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
