---
description: Sometimes a blank slate is what you need..
---

# ✅ Reinstalling the node from scratch

If you are receiving errors and cannot debug, or you are worried you may have messed things up, reinstalling the node may be the fastest way to save the day.

{% hint style="warning" %}
The procedure below will guide you to ensure you do not lose your keys. However, make sure to have a local backup of your entire `node/.config` folder for security.
{% endhint %}

Only if you are 100% sure that you have an extra `node/.config` folder backup somewhere, then proceed.

Stop the node

```bash
service ceremonyclient stop
```

IMPORTANT: Backup your `.config` folder to `~/backup`&#x20;

```bash
mv ~/ceremonyclient/node/.config ~/backup
```

Delete the ceremonyclient folder&#x20;

```bash
rm -r ~/ceremonyclient
```

Delete the service file (back up any customizations you had made to the file).

```bash
rm /lib/systemd/system/ceremonyclient.service
```

Now, reinstall your node, just follow again the [node-auto-installer.md](../node-auto-installer.md "mention")

After reinstalling your node, let it run for 5 minutes, then stop the service

```bash
service ceremonyclient stop
```

Import your previous .config folder in `ceremonyclient/node/`

```bash
mv ~/backup/.config ~/ceremonyclient/node/
```

Restart your node

```bash
service ceremonyclient start
```

Modify the service file if you previously had customizations (like for CPU limiting - [limiting-your-cpu-usage.md](managing-your-system-resources/limiting-your-cpu-usage.md "mention") )

Done!

<table data-card-size="large" data-column-title-hidden data-view="cards" data-full-width="false"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><strong>The Best Server Providers for your Nodes</strong></td><td>CLICK TO SEE THEM</td><td><a href="../best-server-providers.md">best-server-providers.md</a></td><td></td><td><a href="../.gitbook/assets/best-serve-providers-banner-text-1-1-B.jpg">best-serve-providers-banner-text-1-1-B.jpg</a></td></tr><tr><td><strong>Want to say thank you?</strong></td><td>CLICK TO DONATE</td><td><a href="../want-to-say-thank-you.md">want-to-say-thank-you.md</a></td><td></td><td><a href="../.gitbook/assets/donations-banner-text-1-1-B.jpg">donations-banner-text-1-1-B.jpg</a></td></tr></tbody></table>
