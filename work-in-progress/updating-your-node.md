# ⬆️ Updating your node

{% hint style="warning" %}
After 1.4.17 the update method will chnage, so avoid runnig the automated script below, and instead proceed with the manual method. You will still have to do some different steps than git fetch origin, so ask in the Telegram or Discord for guidance.
{% endhint %}

To update your node you can simply run this script

```
wget -O - https://raw.githubusercontent.com/lamat1111/quilibrium-node-auto-installer/master/qnode_service_update | bash
```

If you prefer to update manually, proceed below.

## Manually updating your node

Stop your node service

```bash
service ceremonyclient stop
```

Go to ceremonyclient folder.

```bash
cd ~/ceremonyclient
```

Check whether some files are updated in the ceremonyclient git repo, run:

```bash
git fetch origin
```

If there are files shown that are changed or different from your local copy, run:

```bash
git merge origin
```

Go to ceremonyclient/node folder.

```bash
cd ~/ceremonyclient/node
```

Next, do a `go clean` command to clear all previous build files. Run:

```bash
GOEXPERIMENT=arenas go clean -v -n -a ./...
```

Next, remove the compiled go binary file `node`, run:

```bash
rm /root/go/bin/node
ls /root/go/bin
```

The `ls` command should respond empty Next, make a new build compiled binary file `node`, run:

```bash
GOEXPERIMENT=arenas  go  install  ./...
```

Verify that the `node` binary is built again, run:

```bash
ls /root/go/bin
```

Response should show

> node

Lastly, start yournode via the service command, run:

```bash
service ceremonyclient start
```
