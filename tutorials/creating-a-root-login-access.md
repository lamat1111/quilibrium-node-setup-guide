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
