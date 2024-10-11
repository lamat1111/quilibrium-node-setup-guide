# ⬆️ Updating your node

If you are running your node as a service, you can simply run the below script.&#x20;

#### Check if everything is alright

Things change fast, and we may be not fast enough to update the scripts you find from now on in the guide. So, to avoid any issue, I suggest checking [Telegram pinned messages](https://t.me/quilibrium) and [Discord announcements](https://discord.gg/quilibrium) for any last minute issue or update. If there is something you don't understand, ask in the chats.

If everything looks fine, proceed to the next step.

{% hint style="info" %}
Even if you run the script but it doesn't work because there was a last minute update, don't worry. The worst that can happen is that they will give you an error.&#x20;
{% endhint %}

{% hint style="warning" %}
Follow the  [safety-checks.md](safety-checks.md "mention") before running this script in your server
{% endhint %}

{% code overflow="wrap" %}
```bash
wget --no-cache -O - https://raw.githubusercontent.com/lamat1111/QuilibriumScripts/master/qnode_service_update.sh | bash
```
{% endcode %}

The script will NOT change any customization you have made to your service file.

If you want to check your service file after the update, run:

```bash
cat /lib/systemd/system/ceremonyclient.service
```

***

<table data-card-size="large" data-column-title-hidden data-view="cards" data-full-width="false"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><strong>The Best Server Providers for your Nodes</strong></td><td>CLICK TO SEE THEM</td><td><a href="best-server-providers.md">best-server-providers.md</a></td><td></td><td><a href=".gitbook/assets/best-serve-providers-banner-text-1-1-B.jpg">best-serve-providers-banner-text-1-1-B.jpg</a></td></tr><tr><td><strong>Want to say thank you?</strong></td><td>CLICK TO DONATE</td><td><a href="want-to-say-thank-you.md">want-to-say-thank-you.md</a></td><td></td><td><a href=".gitbook/assets/donations-banner-text-1-1-B.jpg">donations-banner-text-1-1-B.jpg</a></td></tr></tbody></table>
