# 🔒 Creating a root login access

Some server providers will give you log in details that lead to a `home/username` folder on the server, and they will disable root login by default for security.

Since the auto-installer in this guide works better if your working folder is root, here is how you can solve.

Login to your server with username and password you are being given. If the username is nor `root`, then you will likely be in `home/username` after logging in

switch to root

```bash
sudo su
```

create a password for the root user

```bash
sudo passwd root
```

paste the password by right clicking the mouse and click ENTER (you won't see the password in the terminal). You will be asked to enter it a second time.

Now, permit login for root and restart the ssh service, this command does everything in one step

```bash
sudo sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config && sudo service ssh restart
```

If you prefer to proceed step by step

Open the /etc/ssh/sshd\_config

```
sudo nano /etc/ssh/sshd_config
```

Edit the file line #PermitRootLogin and change it to `PermitRootLogin yes`

To save press CTRL+X, then Y, then ENTER

```
sudo service ssh restart
```

***

<table data-card-size="large" data-column-title-hidden data-view="cards" data-full-width="false"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><strong>The Best Server Providers for your Nodes</strong></td><td>CLICK TO SEE THEM</td><td><a href="../best-server-providers.md">best-server-providers.md</a></td><td></td><td><a href="../.gitbook/assets/best-serve-providers-banner-text-1-1-B.jpg">best-serve-providers-banner-text-1-1-B.jpg</a></td></tr><tr><td><strong>Want to say thank you?</strong></td><td>CLICK TO DONATE</td><td><a href="../want-to-say-thank-you.md">want-to-say-thank-you.md</a></td><td></td><td><a href="../.gitbook/assets/donations-banner-text-1-1-B.jpg">donations-banner-text-1-1-B.jpg</a></td></tr></tbody></table>
