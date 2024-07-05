# 🔢 Node step by step installation

{% hint style="info" %}
This is a step by step process alternative to the node auto-installer script. Always refer to the  [node-auto-installer.md](../node-auto-installer.md "mention") for any other info or assistance.
{% endhint %}

_(...) following up from_ [_step 2 of the main guide_](https://docs.quilibrium.one/quilibrium-node-setup-guide/node-auto-installer#id-2-install-ubuntu)_._

Simply run the commands one after the other by copy/pasting. When several commands are grouped, you can safely copy and paste all of them at the same time, and they will be executed sequentially.

#### Check if everything is alright

Things change fast, and we may be not fast enough to update the scripts you find from now on in the guide. So, to avoid any issue, I suggest checking [Telegram pinned messages](https://t.me/quilibrium) and [Discord announcements](https://discord.gg/quilibrium) for any last minute issue or update. If there is something you don't understand, ask in the chats.

If everything looks fine, proceed.

{% hint style="info" %}
Even if you run some commands but they don't work because there was a last minute update, don't worry. The worst that can happen is that they will give you an error.&#x20;
{% endhint %}

***

Update the package lists to ensure the latest versions are available.

```bash
sudo apt -q update
```

Install necessary packages: git, wget, tmux, and tar.

```bash
sudo apt-get install git wget tmux tar -y
```

Download and extract the required version of Go (below commands are for amd64 architectures, if you are on a Linux server they should be fine)

```bash
wget https://go.dev/dl/go1.22.4.linux-amd64.tar.gz
sudo tar -C /usr/local -xzf go1.22.4.linux-amd64.tar.gz
sudo rm go1.22.4.linux-amd64.tar.gz
```

Update PATH and GOPATH environment variables in \~/.bashrc.

```bash
echo 'export PATH=$PATH:/usr/local/go/bin' >> ~/.bashrc
echo 'export GOPATH=$HOME/go' >> ~/.bashrc
echo 'export GO111MODULE=on' >> ~/.bashrc
echo 'export GOPROXY=https://goproxy.cn,direct' >> ~/.bashrc
source ~/.bashrc
```

Create and configure swap space for weak server - optional (not needed if you are running on Docker)

```bash
sudo mkdir /swap && sudo fallocate -l 24G /swap/swapfile && sudo chmod 600 /swap/swapfile
sudo mkswap /swap/swapfile && sudo swapon /swap/swapfile
sudo bash -c 'echo "/swap/swapfile swap swap defaults 0 0" >> /etc/fstab'
```

Modify network buffer sizes for better performance (likely won't work if you are running on Docker)

```bash
sudo bash -c 'echo -e "\nnet.core.rmem_max=600000000" >> /etc/sysctl.conf'
sudo bash -c 'echo -e "\nnet.core.wmem_max=600000000" >> /etc/sysctl.conf'
sudo sysctl -p
```

Create some useful folders

```bash
mkdir -p /root/backup/ /root/scripts/ /root/scripts/log/
```

Reboot your server (not needed on Docker)

```bash
sudo reboot
```

Login again in your server after 3–5 mins and proceed below

***

## Install your node and run it as a service

Clone the ceremony client from GitHub

{% code overflow="wrap" %}
```bash
cd ~ && git clone https://github.com/QuilibriumNetwork/ceremonyclient.git
```
{% endcode %}

After cloning successfully the code, checkout the release

```bash
cd ~/ceremonyclient/ && git checkout release
```

Create the service file and open it in the nano editor

```bash
nano /lib/systemd/system/ceremonyclient.service
```

Copy/paste the below code (for pasting, simply right click with the mouse)\
If your working directory is different from "root" than edit the code accordingly.

```bash
[Unit]
Description=Ceremony Client Go App Service

[Service]
Type=simple
Restart=always
RestartSec=5s
WorkingDirectory=/root/ceremonyclient/node
ExecStart=/root/ceremonyclient/node/release_autorun.sh

[Install]
WantedBy=multi-user.target

```

_To save press CTRL+X, then Y, then ENTER_

Enable the service

```bash
sudo systemctl daemon-reload && sudo systemctl enable ceremonyclient
```

Start the node

```bash
service ceremonyclient start
```

Now continue [here](https://docs.quilibrium.one/quilibrium-node-setup-guide/node-auto-installer#id-5-let-the-node-run)

***

<table data-card-size="large" data-column-title-hidden data-view="cards" data-full-width="false"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><strong>The Best Server Providers for your Nodes</strong></td><td>CLICK TO SEE THEM</td><td><a href="../best-server-providers.md">best-server-providers.md</a></td><td></td><td><a href="../.gitbook/assets/best-serve-providers-banner-text-1-1-B.jpg">best-serve-providers-banner-text-1-1-B.jpg</a></td></tr><tr><td><strong>Want to say thank you?</strong></td><td>CLICK TO DONATE</td><td><a href="../want-to-say-thank-you.md">want-to-say-thank-you.md</a></td><td></td><td><a href="../.gitbook/assets/donations-banner-text-1-1-B.jpg">donations-banner-text-1-1-B.jpg</a></td></tr></tbody></table>
