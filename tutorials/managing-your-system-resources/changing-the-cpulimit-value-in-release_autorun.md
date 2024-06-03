# ☑️ Changing the cpulimit value in release\_autorun

If you run your node using the method outlined in this guide or via the release\_autorun.sh file included with the node software, a CPU limit of 50% will be automatically set.&#x20;

This is done to prevent your node from using 100% of the CPU constantly, which can impact performance negatively, especially when generating proofs.

However, it's important to note that each machine has its own optimal CPU limit for maximum performance. For some, this might be 60%, 70%, or another value.&#x20;

A quick way to adjust this CPU limit is by using the following command:

{% code overflow="wrap" %}
```bash
find /root/ceremonyclient/node/ -type f -name release_autorun.sh -exec sed -i 's/cpulimit -l [0-9]\+/cpulimit -l 70/g' {} +

```
{% endcode %}

{% hint style="info" %}
Change 70 at the end of the command with whatever value you want to limit your CPU to, then restart your node after the change
{% endhint %}

### ⚠️ Please note that if you run this command...&#x20;

* Your node will not be able to update by itself anymore (because you have edited a core file). My manual update script however will still work because it contains a specific instruction to overwrite any local edits you made to the file with the source file.
* This edit will be overwritten the next time you update via the update script  ( [updating-your-node.md](../../updating-your-node.md "mention")), you will have to run the command again.

***

<table data-card-size="large" data-column-title-hidden data-view="cards" data-full-width="false"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><strong>The Best Server Providers for your Nodes</strong></td><td>CLICK TO SEE THEM</td><td><a href="../../best-server-providers.md">best-server-providers.md</a></td><td></td><td><a href="../../.gitbook/assets/best-serve-providers-banner-text-1-1-B.jpg">best-serve-providers-banner-text-1-1-B.jpg</a></td></tr><tr><td><strong>Want to say thank you?</strong></td><td>CLICK TO DONATE</td><td><a href="../../want-to-say-thank-you.md">want-to-say-thank-you.md</a></td><td></td><td><a href="../../.gitbook/assets/donations-banner-text-1-1-B.jpg">donations-banner-text-1-1-B.jpg</a></td></tr></tbody></table>
