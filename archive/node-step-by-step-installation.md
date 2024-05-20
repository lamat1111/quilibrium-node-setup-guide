# 🔢 Node step by step installation

{% hint style="info" %}
This is a step by step process alternative to the node auto-installer script. Always refer to the [node auto-installer steps](node-auto-installer.md) for any other info or assistance.
{% endhint %}

_(...) following up from_ [_step 2 of the main guide_](https://app.gitbook.com/o/OarGuxi0cVButvqcFwRt/s/wYHoFaVat0JopE1zxmDI/node-auto-installer#step-2)_._

Simply run the commands one after the other by copy/pasting. When several commands are grouped, you can safely copy and paste all of them at the same time, and they will be executed sequentially.

***

Update the package lists to ensure the latest versions are available.

```bash
sudo apt -q update
```

Install necessary packages: git, wget, tmux, and tar.

```bash
sudo apt-get install git wget tmux tar -y
```

Download and extract the required version of Go

```bash
wget https://go.dev/dl/go1.20.14.linux-amd64.tar.gz
sudo tar -C /usr/local -xzf go1.20.14.linux-amd64.tar.gz
sudo rm go1.20.14.linux-amd64.tar.gz
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

Create /root/scripts/qnode\_restart.sh (simple script to start the node and restart it automatically if it stops)

```bash
sudo wget -O /root/scripts/qnode_restart.sh -N https://raw.githubusercontent.com/lamat1111/quilibrium-node-auto-installer/master/qnode_restart && sudo chmod +x /root/scripts/qnode_restart.sh
```

Clone the ceremony client from GitHub (after 1.4.17 this step may change, ask in the [Telegram group](https://t.me/quilibrium))

```bash
cd ~ && git clone https://github.com/QuilibriumNetwork/ceremonyclient.git
```

Build the Quilibrium client (for transferring tokens)

```bash
cd ~/ceremonyclient/client && GOEXPERIMENT=arenas go build -o qclient main.go
```

Reboot your server (not needed on Docker)

```bash
sudo reboot
```

Now continue [here](node-auto-installer.md#step-5)
