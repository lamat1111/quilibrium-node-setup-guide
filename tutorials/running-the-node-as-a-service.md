# 👾 Running the node as a service

If you have been running your node via a tmux session (previous version of this guide), but now would like to run it as a service for flexibility, here is what you can do.

Kill your tmux session

```
tmux kill-session -t quil
```

Run the below script. You can inspect the code [here](https://github.com/lamat1111/Quilibrium-Node-Auto-Installer/blob/main/installer\_qnode\_service\_only)

```
wget -O - https://raw.githubusercontent.com/lamat1111/quilibrium-node-auto-installer/master/installer_qnode_service_only | bash
```

{% hint style="info" %}
The script simply creates a service file with the right configurations and starts it for you
{% endhint %}

When the script finishes, you will start seeing your node log. Press CTRL+C to stop it (this won't stop your node, just the view of the log).

***

#### Extra step

Delete your cronjob, if you have one, for starting the node automatically after a reboot. The service will now take care of this automatically.

```
crontab -e
```

If you are prompted to choose an editor, choose "nano". Delete the cronjob starting with @reboot, in case you have more than one. Then save with CTRL + X, then Y, then ENTER.
