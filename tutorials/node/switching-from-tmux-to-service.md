# 🔄 Switching from tmux to service

If you have been running your node via a tmux session (previous version of this guide), but now would like to run it as a service for flexibility, here is what you can do.

Kill your tmux session

```
tmux kill-session -t quil
```

Run the below script

{% hint style="warning" %}
Follow the  [safety-checks.md](../../safety-checks.md "mention") before running this script in your server
{% endhint %}

```
wget --no-cache -O - https://raw.githubusercontent.com/lamat1111/QuilibriumScripts/master/qnode_service_update.sh | bash
```

{% hint style="info" %}
The script simply check for new node updates, then creates a service file with the right configurations and starts it for you. You can inspect the code [here](https://github.com/lamat1111/QuilibriumScripts/blob/main/qnode\_service\_update.sh)
{% endhint %}

When the script finishes, you will start seeing your node log. Press CTRL+C to stop it (this won't stop your node, just the view of the log).

***

#### Extra step

Delete your cronjob, if you have one, for starting the node automatically after a reboot. The service will now take care of this automatically.

```
crontab -e
```

If you are prompted to choose an editor, choose "nano". Delete the cronjob starting with @reboot, in case you have more than one. Then save with CTRL + X, then Y, then ENTER.

***

<table data-card-size="large" data-column-title-hidden data-view="cards" data-full-width="false"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><strong>The Best Server Providers for your Nodes</strong></td><td>CLICK TO SEE THEM</td><td><a href="../../best-server-providers.md">best-server-providers.md</a></td><td></td><td><a href="../../.gitbook/assets/best-serve-providers-banner-text-1-1-B.jpg">best-serve-providers-banner-text-1-1-B.jpg</a></td></tr><tr><td><strong>Want to say thank you?</strong></td><td>CLICK TO DONATE</td><td><a href="../../want-to-say-thank-you.md">want-to-say-thank-you.md</a></td><td></td><td><a href="../../.gitbook/assets/donations-banner-text-1-1-B.jpg">donations-banner-text-1-1-B.jpg</a></td></tr></tbody></table>
