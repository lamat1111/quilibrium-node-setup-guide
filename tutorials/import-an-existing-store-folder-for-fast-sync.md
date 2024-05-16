# ⚡ Import an existing store folder for fast sync

For syncing fast your new node it is possible to import the ceremonyclient/node/.config/store folder from an already synced node.

If you don't have one, try to ask in the Telegram or Discord and maybe someone will help you.

Once you have your store.zip proceed like this (this procedure assumes that you are using Termius SFTP feature or WinSCP to navigate the folders.

1. Open the .zip locally, check that it contains a "store" folder and that the folder contains a long list of .sst files
2. Stop your node&#x20;
3. Backup your existing store folder (just change its name)
4. Upload the new store folder and extract the archive in ceremonyclient/node/.config/
5. Check that your new ceremonyclient/node/.config/store folder contains a list of .sst files
6. Import the ceremonyclient/node/.config/REPAIR file from an existing synced node (backup your existing REPAIR file). If you don't have a REPAIR file you can use the one below
7. Restart your node and wait. \
   It's normal for the node process to crash 1 or 2 times, but after 15 minutes it should start to sync normally.

{% file src="../.gitbook/assets/REPAIR" %}
import in your ceremonyclient/node/.config/ folder
{% endfile %}

