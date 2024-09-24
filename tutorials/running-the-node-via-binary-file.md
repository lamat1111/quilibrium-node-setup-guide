# ℹ️ Running the node via binary file

If you use the [node-auto-installer.md](../node-auto-installer.md "mention"), this will set a service file that runs the node via the release\_autorun.sh script\
This script is able to auto-update your node when there is a new version available.\
\
In some rare cases though, this file does not work as intended, and you will get an error in the node log, which won't be able to start.\
What you can do then is edit the service file and set it to run the node directly via binary file.

Stop the node if it's running and open the service file.

{% code overflow="wrap" %}
```bash
nano /lib/systemd/system/ceremonyclient.service
```
{% endcode %}

Change this line

{% code overflow="wrap" %}
```bash
ExecStart=/root/ceremonyclient/node/release_autorun.sh
```
{% endcode %}

With this one

{% code overflow="wrap" %}
```bash
ExecStart=/root/ceremonyclient/node/node-1.4.21.1-amd64
```
{% endcode %}

Please note that `node-1.4.21.1-amd64` will be different depending on the node version and architecture. Look in your `ceremonyclient/node folder`  and you should see the correct version you have downloaded.\
Now save the file and exit with CTRL+X and then Y

Update your daemon, run:

```sh
systemctl daemon-reload
```

Restart your node which at this point should work correctly.

{% hint style="warning" %}
If you make this change in the service file you will lose the ability to auto-update, and you will have to update manually.&#x20;

Also, when updating via my script, you may face again the same issue, because that line will be set again to release\_autorun.sh.  You will have to manually make again the edit and set it to the new node binary version.
{% endhint %}

<table data-card-size="large" data-column-title-hidden data-view="cards" data-full-width="false"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><strong>The Best Server Providers for your Nodes</strong></td><td>CLICK TO SEE THEM</td><td><a href="../best-server-providers.md">best-server-providers.md</a></td><td></td><td><a href="../.gitbook/assets/best-serve-providers-banner-text-1-1-B.jpg">best-serve-providers-banner-text-1-1-B.jpg</a></td></tr><tr><td><strong>Want to say thank you?</strong></td><td>CLICK TO DONATE</td><td><a href="../want-to-say-thank-you.md">want-to-say-thank-you.md</a></td><td></td><td><a href="../.gitbook/assets/donations-banner-text-1-1-B.jpg">donations-banner-text-1-1-B.jpg</a></td></tr></tbody></table>
