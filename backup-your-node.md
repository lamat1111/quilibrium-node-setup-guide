# 📦 Backup your node

A good practice is to back up the entire `node/.config/` folder, which contains the store folder, the node keys files, and some necessary files if you have to import the node to a different machine.

{% hint style="info" %}
In 2.0 the store folder is the same for all nodes, so you can import it from another node in oder to quickly sync up a new node. \
To swap keys between machines, you only needs to swap the config.yml and keys.yml, and nothing else.
{% endhint %}

Personally, I do backup the entire `node/.config/` folder, but I DO NOT back up my keys.yml and config.yml files with it, for security. Instead, I back up those files locally, since they just need to be backed up once (see [backup-your-private-keys.md](backup-your-private-keys.md "mention")).

### How to back up?

* If you have set up your server with RAID 1, you are already backing up all your data on your second disk. Still, ensure your provider offers reliable support in case of need.
* If you are using [CherryServers,](https://quilibrium.one/go/cherryservers) they already provide backup storage by default, and you can set up a cronjob to back up your store folder every hour (they will assist you if needed).
* If you don't have many nodes, you could manually back up your store folder once a day.
* You could utilize an online service such as  [StorJ](https://www.storj.io/) or  [iDrive](https://quilibrium.one/idrive) and set up automatic backups every hour via their Linux CLI tools.
* There are also more sophisticated methods to create automatic backups on Linux, but you need to have expertise in this area.

***

## If you have used the "Backup Node" option in the Q1 menu, read this

The current Q1 backup node option backs up your entire `.config` folder, including your store folder, at your chosen time interval.

### Drawbacks in Q2.0

1. Backing up while the node is running is not ideal. While it can work, it may cause issues when restoring a backup in some cases.
2. Backing up the store folder is less necessary than before, as the store is no longer unique to your node. You can now restore a store from a different node if needed.

### Stopping Current Backup Process

If you're using the "node backup" feature and want to stop these backups from running while the node is active:

1. Access your crontabs by running:

```bash
crontab -e
```

2. Find and comment out or delete the line that begins with:

{% code overflow="wrap" %}
```bash
rclone sync --transfers 10 --checkers 20 --disable-http2 --retries 1 --filter '+ store/**' --filter '+ store' --filter '- SELF_TEST' (...)
```
{% endcode %}

3. To save, press `CTRL+X` and then `Y`

### Setting Up Safe Store Folder Backups

To keep a snapshot of your store folder while the node is stopped, you can add a cronjob like this:

{% code overflow="wrap" %}
```sh
0 5 * * * systemctl stop ceremonyclient && sleep 30 && rclone sync --filter '+ store/**' --filter '- SELF_TEST' --filter '- keys.yml' --filter '- config.yml' /root/ceremonyclient/node/.config/ storj:/bucket/folder/.config/ && sleep 5 && systemctl start ceremonyclient
```
{% endcode %}

#### Important Notes:

* Replace `bucket/folder` with your StorJ bucket name and backup folder path
* Test the command before setting up the cronjob
* This will run daily at 5 AM. You can adjust the frequency, but remember that each run will stop and restart your node. The node will remain stopped during the upload to StorJ.
* The command is set to NOT back up your keys.yml and config.yml, for security. Delete the command filters if you want to back them up.
* Using the `sync` command means only new files are copied. After the initial backup, subsequent backups will be quick (approximately 1 minute).

***

## Back up automatically on Storj

{% hint style="danger" %}
**This script is outdated for Q2.0.** \
Please read the paragraph above. While this script will still work, it's not optimized for 2.0, particularly because it performs backups while the node is running. This is no longer recommended as it can sometimes cause issues when restoring a backup.
{% endhint %}

I created a script to set up automatic backups on [StorJ](https://www.storj.io/).&#x20;

Before using the script, you need to create a bucket specific to Quilibrium and public/private keys to read/write in this specific bucket.&#x20;

To create your Keys on StorJ click on "Access Keys" in your left menu, then choose  "S3 Credentials", and select the various options you want (suggested: read/write on a  specific bucket).

I like StorJ more than Amazon AWS, it is more user-friendly, cheaper, and in my opinion more secure.

The script allows you to also back up your cronjobs and any custom script that you have in the `/root/scripts` folder

If you are ready, you can use the script by running this:

{% hint style="warning" %}
Follow the [safety-checks.md](safety-checks.md "mention") before running this script in your server
{% endhint %}

{% code overflow="wrap" %}
```bash
mkdir -p ~/scripts && wget -P ~/scripts -O ~/scripts/qnode_backup_storj.sh https://raw.githubusercontent.com/lamat1111/QuilibriumScripts/main/tools/qnode_backup_storj.sh && chmod +x ~/scripts/qnode_backup_storj.sh && ~/scripts/qnode_backup_storj.sh

```
{% endcode %}

### Restore a backup hosted on StorJ

I also made another script to restore your backup. It will only work if you backed up your entire `.config` folder via the script above.

I recommend you to install the [q1-node-manager.md](q1-node-manager.md "mention") where you will find both options (Backup and Restore). Or you can run the restore script directly with this command:

{% code overflow="wrap" fullWidth="false" %}
```bash
mkdir -p ~/scripts && wget -O ~/scripts/qnode_backup_restore_storj.sh https://raw.githubusercontent.com/lamat1111/quilibriumscripts/main/tools/qnode_backup_restore_storj.sh && chmod +x ~/scripts/qnode_backup_restore_storj.sh && ~/scripts/qnode_backup_restore_storj.sh
```
{% endcode %}

***

### Troubleshooting

If after running the script, your backups do not work, here are some things you can check.

Check your cronjobs with `crontab -l` they should begin with rclone and have the source and target path set correctly. You can manually edit them with `crontab -e` , but be careful.

Check the rclone configs, run `nano ~/.config/rclone/rclone.conf.`

They should look something like this:

```shellscript
[storj]
type = s3
provider = Storj
access_key_id = access-key-here
secret_access_key = private-key-here
endpoint = https://gateway.storjshare.io
acl = private
```

If up until this point everything looks correct, you may want to check your StorJ account and see if you are using the correct keys to access the bucket that you have set in your cronjobs.

***

### Backing up your whole .config folder

{% hint style="info" %}
If you have run the previous version of the script (before 15.06.2024 13.30 UTC), your cronjob is set to back up only the store folder. Since it seems now better to back up the whole .config folder, here is what you can do.
{% endhint %}

<details>

<summary>Automatic method (slower but easier)</summary>

Run again the backup script provided above and follow the procedure again from the beginning. This will set up a new backup for you for the entire `.config` folder.

</details>

<details>

<summary>Manual method (faster but requires experience with terminal commands)</summary>

Open your crontab with `crontab -e`

Find the crontab that begins with `rclone sync --transfers 10 --checkers 20...`, move the cursor there and pres CTRL +K to delete it.

Now copy this whole command

{% code overflow="wrap" %}
```bash
5 */1 * * * rclone sync --transfers 10 --checkers 20 --disable-http2 --retries 1 --filter '+ store/**' --filter '+ store' --filter '- SELF_TEST' --filter '- keys.yml' --filter '- config.yml' /root/ceremonyclient/node/.config/ storj:/bucket/folder/.config/
```
{% endcode %}

Change `bucket` and `folder` with your StorJ bucket name and the target folder name.

Paste (simply right click after copying) the entire code in the crontab screen that you previously opened.

Save with CTRL + X, then Y, then ENTER

Now this new cronjob will backup your entire config folder every 1 hour, except for your keys.yml and config.yml, which I recommend backing up locally for security. If you want to back up those files as well, simply delete `--filter '- keys.yml' --filter '- config.yml'`from the cronjob command above.

#### FINAL STEP! Delete your `storj:/your_bucket/your_folder/store/` folder from StorJ

The new backup method stores your backups in `storj:/your_bucket/your_folder/.config/`, so now you will have  an extra folder  `storj:/your_bucket/your_folder/store/` that you can delete.

</details>

***

### Other backup scripts

<details>

<summary>Back up on Cherry backup storage</summary>

If you are  [Cherryservers](https://quilibrium.one/go/cherryservers) customer, you have access to  their free back up storage, and you can use the below script (made by Lili) to set up automatically a backup for your `ceremonyclient/node` folder.

Via the script, you can pick between uploading to [Cherry backup storage](https://docs.cherryservers.com/knowledge/backup-storage) (free with every server), or to [StorJ ](https://www.storj.io/)

Please note that this script is backing up your whole `ceremonyclient/node` folder, so also your keys.yml and config.yml files.

{% code overflow="wrap" %}
```bash
wget --no-check-certificate https://snapshots.cherryservers.com/quilup.sh && chmod +x quilup.sh && ./quilup.sh
```
{% endcode %}

</details>

<details>

<summary>Back up automatically on Amazon AWS</summary>

I created a little script to set up automatic backups on Amazon AWS. This script is still working, but I don't support it anymore. I recommend using the one for StorJ. This script will only back up your "store" folder and not the whole ".config" folder.

Please note that in order for this to work, you need:

* Amazon AWS account
* Public/Private keys to access your account
* A "bucket" in Amazon AWS (better if specific to Quilibrium)

For security, it is better to create Public/Private keys that only access your Quilibrium bucket. The whole process of creating users and keys on Amazon AWS is not very user-friendly, keep this in mind!

If you have all of the above, you can use the script by running this:

{% code overflow="wrap" %}
```bash
wget -P ~/scripts -O ~/scripts/qnode_store_backup_aws.sh https://raw.githubusercontent.com/lamat1111/QuilibriumScripts/main/tools/qnode_store_backup_aws.sh && chmod +x ~/scripts/qnode_store_backup_aws.sh && ~/scripts/qnode_store_backup_aws.sh
```
{% endcode %}

</details>

***

<table data-card-size="large" data-column-title-hidden data-view="cards" data-full-width="false"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><strong>Want to say thank you?</strong></td><td>CLICK TO DONATE</td><td><a href="want-to-say-thank-you.md">want-to-say-thank-you.md</a></td><td></td><td><a href=".gitbook/assets/donations-banner-text-1-1-B.jpg">donations-banner-text-1-1-B.jpg</a></td></tr></tbody></table>
