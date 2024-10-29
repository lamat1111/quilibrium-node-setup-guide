# 🔒 Set up SSH keys

{% hint style="info" %}
Usually, when you rent a server, you are given a username and password to connect to it. However, this poses a security risk as hackers can attempt to guess your password using brute force attacks. To mitigate this risk, you can disable password access to your server and use SSH keys instead.

My personal way is to set up just one pair of keys: the private key resides on the local PC and the public key on any server I want to access. If I use more than one local device to access my servers, I set up another key pair for each new device.
{% endhint %}

Here is a [comprehensive guide](https://www.digitalocean.com/community/tutorials/how-to-set-up-ssh-keys-on-ubuntu-22-04) on how to set up SSH keys on your server.

**Alternatively, you can use Termius, which offers a simpler method as outlined below:**

1. Install [Termius](https://termius.com/) and follow [this guide](https://support.termius.com/hc/en-us/articles/4401872025113-Keychain) to generate an SSH key. Remember to securely store your key, either in an encrypted folder on your computer or on an encrypted USB drive.
2. Through Termius, you can easily export the SSH key to your host and create an identity as explained in the guide.
3. Test that you can successfully connect to the server using this SSH key.
4. If you have multiple nodes or servers, you can use the same SSH key for all of them.
5. Once logged into your server, run `sudo nano /etc/ssh/sshd_config`.
6. Scroll down using the down arrow until you locate the line `# PasswordAuthentication yes`. Uncomment the line (remove #) and set it to `no`, like so: `PasswordAuthentication no`.
7. To save the changes, press CTRL+X, then Y, then ENTER.
8. Restart your SSH service by running `sudo systemctl restart ssh`.

Now, you should only be able to access the server via SSH key, and password-based access will no longer work.

***

<table data-card-size="large" data-column-title-hidden data-view="cards" data-full-width="false"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><strong>The Best Server Providers for your Nodes</strong></td><td>CLICK TO SEE THEM</td><td><a href="../../best-server-providers.md">best-server-providers.md</a></td><td></td><td><a href="../../.gitbook/assets/best-serve-providers-banner-text-1-1-B.jpg">best-serve-providers-banner-text-1-1-B.jpg</a></td></tr><tr><td><strong>Want to say thank you?</strong></td><td>CLICK TO DONATE</td><td><a href="../../want-to-say-thank-you.md">want-to-say-thank-you.md</a></td><td></td><td><a href="../../.gitbook/assets/donations-banner-text-1-1-B.jpg">donations-banner-text-1-1-B.jpg</a></td></tr></tbody></table>
