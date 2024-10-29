# 🩷 Escaping the "Pink Screen of Death"

Sometimes when updating the apps with the [node-auto-installer.md](../../node-auto-installer.md "mention"), or even manually, you will receive what I call the "Pink Screen of Death".

This is just a screen that asks you which services you want to restart, and usually clicking ENTER should suffice to move on. The issue is… sometimes it doesn't work, and you get stuck here.

<figure><img src="../../.gitbook/assets/2024-05-24_17-55-04.png" alt=""><figcaption><p>The Pink Screen of Death</p></figcaption></figure>

**To solve this issue, you may try these steps:**

1. Have you already tried pressing ENTER or ESC? If yes, then move on.
2. Have already tried pressing TAB to navigate to \<Cancel> and confirm with ENTER? If yes, then move on.
3. Log in to your server via another terminal window and reboot: `sudo reboot`
4. Run again the app update manually: `sudo apt -q update`
5. Install some extra apps: `sudo apt-get install git wget tmux tar -y`
6. If everything went smoothly up to here, you can either run again the  [node-auto-installer.md](../../node-auto-installer.md "mention")script (step 3), or you can proceed with the  [node-step-by-step-installation.md](node-step-by-step-installation.md "mention")where you left off.

_This process almost always solved the issue for me, I really hope you don't get stuck in the pink forever ;-)_

***

<table data-card-size="large" data-column-title-hidden data-view="cards" data-full-width="false"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><strong>The Best Server Providers for your Nodes</strong></td><td>CLICK TO SEE THEM</td><td><a href="../../best-server-providers.md">best-server-providers.md</a></td><td></td><td><a href="../../.gitbook/assets/best-serve-providers-banner-text-1-1-B.jpg">best-serve-providers-banner-text-1-1-B.jpg</a></td></tr><tr><td><strong>Want to say thank you?</strong></td><td>CLICK TO DONATE</td><td><a href="../../want-to-say-thank-you.md">want-to-say-thank-you.md</a></td><td></td><td><a href="../../.gitbook/assets/donations-banner-text-1-1-B.jpg">donations-banner-text-1-1-B.jpg</a></td></tr></tbody></table>
