---
description: Important updates if you have used this guide auto-installer
---

# 📣 Announcements

## 📌 1.4.18 is out NOW! How to update.

Make sure to stop your autoscript! Update by doing this in the ceremonyclient/node folder:

```
cd ~/ceremonyclient/node && git checkout release && ./release_autorun.sh
```

### If you are running the node as a service.&#x20;

Follow this guide  [updating-your-node.md](updating-your-node.md "mention")

### If you are running via  a tmux session

Kill your session.

```
tmux kill-session -t quil
```

Create a new session and enter it

```
tmux new-session -s quil
```

Run the command below to update the node

```
cd ~/ceremonyclient/node && git checkout release && ./release_autorun.sh
```

Detach from the tmux session by pressing CTRL+B and then D



### A few important notes about this release:

* we are switching to a proof system for validating nodes resources directly, this is a miniature version of PoMW
* this update when it hits main _will_ break the CD script, be sure you are not still using it
* if you want to run something like it, please do the following:

1. Pull the latest
2. Switch to the release branch
3. In the node folder, run ./release\_autorun.sh

* if you want to run from source still and you know what you're doing (or you're on windows as we don't have signed builds for windows yet), run via GOEXPERIMENT=arenas go run ./... --signature-check=false

There will be a 24 hour grace period. The release branch is now live.

**Things you will notice:**

* this release will use your CPU a lot more than previous ones. This will reflect what 2.0 will demand from your node, plan accordingly
* this release should use less bandwidth than previous ones.
* the logging is much quieter

***

.

.

.

.

.

.

.

.

.

.

.

## OLD Announcements

### 📌 Run your node as a service

The new [node-auto-installer.md](node-auto-installer.md "mention") in this guide will now install and manage the node as a service.

Running a node as a service offers automatic startup, robustness, isolation, resource management, logging, monitoring, and security benefits compared to using a tmux session.

If you're already running the node in a tmux session here is a tutorial to quickly convert it to a node run as a service: [switching-from-tmux-to-service.md](tutorials/switching-from-tmux-to-service.md "mention")

Do you have to convert? Not really, your node will work just fine in a tmux session, but my guide will only cover nodes run as a service from now on, so you may want to consider it.\
By the way... converting to a service takes only 3 mins ;-)

***

### Do this before 1.4.18, if you are still using poor\_mans\_cd to run your node

#### Run your node normally

Stop your node with  `tmux kill-session -t quil`

Run the below command. This creates a new tmux session and run the node normally inside it. You will not see any output after running the command.&#x20;

```
tmux new-session -d -s quil 'export PATH=$PATH:/usr/local/go/bin && cd ~/ceremonyclient/node && GOEXPERIMENT=arenas go run ./...'
```

You can check your node log with `tmux a -t quil` . To detach from tmux type CTRL+B and then D.

#### Change the cronjob command

If you are using the old cronjob command to restart the node after a server reboot, you need to change it as well. Type `crontab -e` and check if there is a cronjob.

If so, change `./poor_mans_cd.sh` with `GOEXPERIMENT=arenas go run ./...` \
To save: CTRL+X, then Y then ENTER

this is the whole correct command you should see&#x20;

`@reboot sleep 10 && bash -lc "export PATH=$PATH:/usr/local/go/bin && cd ~/ceremonyclient/node && tmux new-session -d -s quil 'GOEXPERIMENT=arenas go run ./...'"`

{% hint style="info" %}
the export PATH=$PATH:/usr/local/go/bin part is redundant but it can solve the "go command not found" error that sometimes happens even if you have the correct variables in your .bashrc file
{% endhint %}

