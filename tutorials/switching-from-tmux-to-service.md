# 🔄 Switching from tmux to service

{% hint style="danger" %}
DO NOT USE if the update to 1.4.18 has landed (check on Telegram) as the script will not work. Wait for instructions in Telegram. If you want to update your existing node to 1.4.18 you can follow this guide:  [updating-your-node.md](../updating-your-node.md "mention")
{% endhint %}

If you have been running your node via a tmux session (previous version of this guide), but now would like to run it as a service for flexibility, here is what you can do.

Kill your tmux session

```
tmux kill-session -t quil
```

Run the below script

{% hint style="warning" %}
_Follow the_  [safety-checks.md](../safety-checks.md "mention")before running this script in your server
{% endhint %}

```
wget -O - https://raw.githubusercontent.com/lamat1111/quilibrium-node-auto-installer/master/installer_qnode_service_only | bash
```

{% hint style="info" %}
The script simply creates a service file with the right configurations and starts it for you. You can inspect the code [here](https://github.com/lamat1111/Quilibrium-Node-Auto-Installer/blob/main/installer\_qnode\_service\_only)
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

[![image-text](https://accademiainfinita.it/extra-contents/quil-best-providers-banner-square.jpg)](https://iri.quest/quil-best-server-providers)
