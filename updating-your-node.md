# ⬆️ Updating your node

If you are running your node as a service, to update your node to 1.4.18, you can simply run the below script.&#x20;

{% hint style="warning" %}
_Follow the_  [safety-checks.md](safety-checks.md "mention")before running this script in your server
{% endhint %}

```
wget -O - https://raw.githubusercontent.com/0xOzgur/QuilibriumTools/v1.4.18/update.sh | bash
```

🙏 _Many tanks to_ [_@OxOzgur_](https://github.com/0xOzgur) _for providing the auto-update script_

***

## Manual method

{% hint style="info" %}
Source: [https://quilibrium.guide/upgrade-1-4-18](https://quilibrium.guide/upgrade-1-4-18) \
_I have only tested and reworked the instructions a bit for clarity_
{% endhint %}

Stop your node service

```bash
service ceremonyclient stop
```

Go to ceremonyclient folder.\
Check whether some files are updated in the ceremonyclient git repo.\
If there are files shown that are changed or different from your local copy, merge them.\
Do a `go clean` command to clear all previous build files.&#x20;

```bash
cd ~/ceremonyclient
git fetch origin
git merge origin
cd ~/ceremonyclient/node
GOEXPERIMENT=arenas go clean -v -n -a ./...
```

Remove the compiled go binary file `node`

```bash
rm /root/go/bin/node
ls /root/go/bin
```

Rebuild the qclient

```bash
cd ~/ceremonyclient/client
rm /root/go/bin/qclient
GOEXPERIMENT=arenas go build -o /root/go/bin/qclient main.go
ls /root/go/bin
```

Switch to branch releases of the repo

```bash
cd /root/ceremonyclient/node
git checkout release
```

Now, in order to appropriately adjust the systemd file, it's crucial to pinpoint the suitable executable file from three available options:

1. node-1.4.18-linux-amd64
2. node-1.4.18-linux-arm64
3. node-1.4.18-darwin-arm64

Begin by determining your server's operating system type using the command:

```bash
echo $OSTYPE
```

If the output matches "darwin", opt for:

```bash
node-1.4.18-darwin-arm64
```

For "linux-gnu" systems, consider these choices:

1. node-1.4.18-linux-amd64
2. node-1.4.18-linux-arm64
3. node-1.4.18-darwin-arm64

To further narrow down the appropriate binary file, execute:

```bash
echo $arch
```

If "arm" is present in the output, select:

```bash
node-1.4.18-linux-arm64
```

In case of a blank result, opt for:

```bash
node-1.4.18-linux-amd64
```

To update the service systemd file, we must adjust the ExecStart directive&#x20;

from `/root/go/bin/node ./...`&#x20;

to `/root/ceremonyclient/node/node-1.4.18-linux-amd64`.

Execute the following command to make the adjustment:

```bash
sed -i 's/ExecStart=\/root\/go\/bin\/node .\/.../ExecStart=\/root\/ceremonyclient\/node\/node-1.4.18-linux-amd64/g' /lib/systemd/system/ceremonyclient.service
```

Don't forget to reload the systemd daemon afterward:

```bash
systemctl daemon-reload
```

{% hint style="info" %}
Replace "node-1.4.18-linux-amd64" with the appropriate binary file based on the prechecks we conducted earlier.
{% endhint %}

Finally, start your node via the service command

```bash
service ceremonyclient start
```

***

[![image-text](https://accademiainfinita.it/extra-contents/quil-best-providers-banner-square.jpg)](https://iri.quest/quil-best-server-providers)
