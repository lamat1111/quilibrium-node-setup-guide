# ⬆️ Updating your node

To update your node to 1.4.18, you can simply run the below script.&#x20;

{% hint style="info" %}
These methods will only work if you are running your node as a service.
{% endhint %}

**For Linux Amd64 systems**\
This is usually the one you want to use if you rented a server with the Ubuntu OS

```
wget -O - https://raw.githubusercontent.com/0xOzgur/QuilibriumTools/main/update.sh | bash
```

***

**For Linux Arm64 systems**

```
wget -O - https://raw.githubusercontent.com/0xOzgur/QuilibriumTools/main/updateLinuxArm64.sh | bash
```

**For Darwin Arm64 systems**

```
wget -O - https://raw.githubusercontent.com/0xOzgur/QuilibriumTools/main/updateDarwinArm64.sh | bash
```

🙏 _Many tanks to_ [_@OxOzgur_](https://github.com/0xOzgur) _for providing the above scripts_

~~If you prefer to update manually, proceed below.~~

***

{% hint style="danger" %}
DO NOT use the manual method below to update to 1.4.18 - Use tha automtead script above instead
{% endhint %}

Stop your node service

```bash
service ceremonyclient stop
```

Go to ceremonyclient folder

```bash
cd ~/ceremonyclient
```

Check whether some files are updated in the ceremonyclient git repo

```bash
git fetch origin
```

If there are files shown that are changed or different from your local copy, then run

```bash
git merge origin
```

Go to ceremonyclient/node folder

```bash
cd ~/ceremonyclient/node
```

Next, do a `go clean` command to clear all previous build files. Run:

```bash
GOEXPERIMENT=arenas go clean -v -n -a ./...
```

Next, remove the compiled go binary file `node`

```bash
rm /root/go/bin/node
ls /root/go/bin
```

The `ls` command should respond empty Next, make a new build compiled binary file `node`, run:

```bash
GOEXPERIMENT=arenas  go  install  ./...
```

Verify that the `node` binary is built again

```bash
ls /root/go/bin
```

Response should show `node`

Start your node via the service command

```bash
service ceremonyclient start
```
