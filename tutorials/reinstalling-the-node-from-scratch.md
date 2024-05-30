---
description: Sometimes a blank slate is what you need..
---

# ✅ Reinstalling the node from scratch

If you are receiving errors and cannot debug, or you are worried you may have messed thing up, reinstalling the node may be the fastest way to solve.

{% hint style="warning" %}
Backup locally your keys, follow [backup-your-private-keys.md](../backup-your-private-keys.md "mention")
{% endhint %}

Only if you are 100% sure that you have the keys.yml and config.yml backup, then proceed.

Stop the node

```bash
service ceremonyclient stop
```

Delete the ceremonyclient folder&#x20;

{% hint style="danger" %}
Careful, this will delete your keys!
{% endhint %}

```bash
rm -r /root/ceremonyclient
```

Delete the service file

```bash
rm /lib/systemd/system/ceremonyclient.service
```

Now, reinstall your node, just follow again the [node-auto-installer.md](../node-auto-installer.md "mention")

After reinstalling your node, let it run for 5 minutes, then stop the service

```bash
service ceremonyclient stop
```

Import your keys.yml and config.yml in the `ceremonyclient/node/.config/`  folder

restart the service

```bash
service ceremonyclient start
```

Modify the service file if you previously had customizations (like for CPU limiting - [limiting-your-vps-cpu-usage.md](limiting-your-vps-cpu-usage.md "mention") )



Done!
