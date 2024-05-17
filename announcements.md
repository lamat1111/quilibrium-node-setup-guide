---
description: Important updates if you have used this guide auto-installer
---

# 📣 Announcements

## Do this before 1.4.18, if you are still using poor\_mans\_cd to run your node

### Run your node normally

Stop your node with  `tmux kill-session -t quil`

Run the below command. This creates a new tmux session and run the node normally inside it. You will not see any output after running the command.&#x20;

```
tmux new-session -d -s quil 'export PATH=$PATH:/usr/local/go/bin && cd ~/ceremonyclient/node && GOEXPERIMENT=arenas go run ./...'
```

You can check your node log with `tmux a -t quil` . To detach from tmux type CTRL+B and then D.

### Change the cronjob command

If you are using the old cronjob command to restart the node after a server reboot, you need to change it as well. Type `crontab -e` and check if there is a cronjob.

If so, change `./poor_mans_cd.sh` with `GOEXPERIMENT=arenas go run ./...` \
To save: CTRL+X, then Y then ENTER

this is the whole correct command you should see&#x20;

`@reboot sleep 10 && bash -lc "export PATH=$PATH:/usr/local/go/bin && cd ~/ceremonyclient/node && tmux new-session -d -s quil 'GOEXPERIMENT=arenas go run ./...'"`

{% hint style="info" %}
the export PATH=$PATH:/usr/local/go/bin part is redundant but it can solve the "go command not found" error that sometimes happens even if you have the correct variables in your .bashrc file
{% endhint %}

