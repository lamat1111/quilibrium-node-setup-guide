# 🛠️ Extra tools

### External tools

* To manage your nodes, use [Termius](https://termius.com/), the coolest SSH client and terminal around :)
* To track your server uptime and resources usage use [Hetrixtools.com](https://hetrix.tools/u-862828), you can track up to 15 servers for free and the setup is very easy

### Internal tools&#x20;

<details>

<summary>vnstat - monitor bandwidth and data flow</summary>

```bash
sudo apt update && sudo apt install vnstat
```

To check the current bandwidth usage use `vnstat`.\
To check hourly stats e use `vnstat -h`.\
Daily: `vnstat -d`. Monthly: `vnstat -m`. Top 10 traffic days: `vnstat -t`.

</details>

<details>

<summary>speedtest - monitor bandwidth speed</summary>

```bash
sudo apt-get install curl
curl -s https://packagecloud.io/install/repositories/ookla/speedtest-cli/script.deb.sh | sudo bash
sudo apt-get install speedtest
```

</details>

<details>

<summary>htop - monitor all processes and resources' consumption</summary>

```bash
sudo apt update && sudo apt install htop
```

To use it just type `htop`

</details>
