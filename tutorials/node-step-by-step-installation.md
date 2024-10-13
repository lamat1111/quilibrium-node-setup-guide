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

Update/upgrade the package lists to ensure the latest versions are available.

```bash
sudo apt update -y && sudo apt upgrade -y
```

Install some necessary packages.

```bash
sudo apt install git wget tar curl cron -y
```

Install some optional packages (optional).

```bash
sudo apt install tmux jq htop -y
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

#### Clone the ceremony client from GitHub

{% code overflow="wrap" %}
```bash
cd ~ && git clone --depth 1 --branch release https://github.com/QuilibriumNetwork/ceremonyclient.git
```
{% endcode %}



#### Download the node binary

You can download the correct node binary automatically via this script:

{% code overflow="wrap" %}
```bash
mkdir -p ~/scripts && \
curl -sSL "https://raw.githubusercontent.com/lamat1111/QuilibriumScripts/main/tools/qnode_download_node_binary.sh" -o ~/scripts/qnode_download_node_binary.sh && \
chmod +x ~/scripts/qnode_download_node_binary.sh && \
~/scripts/qnode_download_node_binary.sh
```
{% endcode %}

Or you can do it manually:

Check the current node release on [https://releases.quilibrium.com/release](https://releases.quilibrium.com/release)

Retrieve the release from the following urls (using curl or wget) and place the files where your node release normally resides (usually in the `ceremonyclient/node` folder):

```
https://releases.quilibrium.com/node-2.0.0-<os>-<arch> 
https://releases.quilibrium.com/node-2.0.0-<os>-<arch>.dgst
https://releases.quilibrium.com/node-2.0.0-<os>-<arch>.dgst.sig.1
https://releases.quilibrium.com/node-2.0.0-<os>-<arch>.dgst.sig.2
https://releases.quilibrium.com/node-2.0.0-<os>-<arch>.dgst.sig.3
etc.
```

If on mac, replace \<os> with darwin, or on linux, replace \<os> with linux. \
For arch, use arm64 or amd64 as needed for your system.



**Download the qclient**

Check the current qclient release on [https://releases.quilibrium.com/qclient-release](https://releases.quilibrium.com/qclient-release)

Retrieve the release from the following URLs (using curl or wget) and place the files in `~/ceremonyclient/client`

For mac, download the darwin release. For linux, the linux release. \
For arch, use arm64 or amd64 as needed for your system.



#### Create the service file and open it in the nano editor

```bash
nano /lib/systemd/system/ceremonyclient.service
```

Copy/paste the below code (for pasting, simply right click with the mouse)\
If your working directory is different from "root" than edit the code accordingly\
Change the node binary file name `node-1.4.21.1-linux-amd64` according to what you see in your `/ceremonyclient/node/` folder

```bash
[Unit]
Description=Ceremony Client Go App Service

[Service]
Type=simple
Restart=always
RestartSec=5s
WorkingDirectory=/root/ceremonyclient/node
ExecStart=/root/ceremonyclient/node/node-1.4.21.1-linux-amd64
KillSignal=SIGINT
TimeoutStopSec=30s

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
