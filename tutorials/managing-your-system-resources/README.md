---
description: >-
  If you are using a VPS with limited resources, your node keeps crashing, or
  you experience OOM errors, try one of these methods
---

# ⚙️ Managing your system resources

The easiest method to implement is [limiting-your-vcores-usage.md](limiting-your-vcores-usage.md "mention")

If that doesn't work, you may try [limiting-your-cpu-usage.md](limiting-your-cpu-usage.md "mention") , or [limiting-the-ram-assigned-to-each-vcore.md](limiting-the-ram-assigned-to-each-vcore.md "mention")



### Quick FAQ

<details>

<summary>My CPU is frying!</summary>

Diminish the number of vCores used by your node (easier): [limiting-your-vcores-usage.md](limiting-your-vcores-usage.md "mention")

Limit your overall CPU usage: [limiting-your-cpu-usage.md](limiting-your-cpu-usage.md "mention")

***

_In this case, there is a theory that limiting CPU usage is better than reducing the number of active cores. The former approach allows all vCores to operate at a reduced capacity, enabling them to 'breathe,' while the latter essentially deactivates some cores while maintaining full power usage for the remaining ones._

</details>

<details>

<summary>My RAM is burning hot!</summary>

Diminish the number of vCores used by your node (easier): [limiting-your-vcores-usage.md](limiting-your-vcores-usage.md "mention")

Diminish the RAM assigned to each vCore (more complex): [limiting-the-ram-assigned-to-each-vcore.md](limiting-the-ram-assigned-to-each-vcore.md "mention")

</details>

<details>

<summary>If I limit my CPU usage, do I still need to limit my vCores?</summary>

That depends. Each vCore is assigned 2 GB of RAM. So the ratio between your vCores and your total RAM needs to be least 1/2.\
Even if you limit your overall CPU usage, this ratio needs to stay the same, or you will go OOM (Out of Memory).

The only case in which you may not need to limit your vCores number, is if you assign less RAM to each vCore by [limiting-the-ram-assigned-to-each-vcore.md](limiting-the-ram-assigned-to-each-vcore.md "mention") (This, though, it's not the best for your node performance).

</details>

***

<table data-card-size="large" data-column-title-hidden data-view="cards" data-full-width="false"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><strong>The Best Server Providers for your Nodes</strong></td><td>CLICK TO SEE THEM</td><td><a href="../../best-server-providers.md">best-server-providers.md</a></td><td></td><td><a href="../../.gitbook/assets/best-serve-providers-banner-text-1-1-B.jpg">best-serve-providers-banner-text-1-1-B.jpg</a></td></tr><tr><td><strong>Want to say thank you?</strong></td><td>CLICK TO DONATE</td><td><a href="../../want-to-say-thank-you.md">want-to-say-thank-you.md</a></td><td></td><td><a href="../../.gitbook/assets/donations-banner-text-1-1-B.jpg">donations-banner-text-1-1-B.jpg</a></td></tr></tbody></table>
