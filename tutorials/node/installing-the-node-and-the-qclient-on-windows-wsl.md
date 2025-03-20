# 🪟 Installing the node and the qclient on Windows WSL

### Activating WSL and installing Ubuntu

Activate WSL on Windows to be able to run Linux and Ubuntu. Here is a great tutorial: [https://www.youtube.com/watch?v=vxTW22y8zV8](https://www.youtube.com/watch?v=vxTW22y8zV8) (you just need to follow the first 7 minutes or so)

Once you have Linux available and Ubuntu installed, to access Ubuntu via terminal you run:

```
wsl -d Ubuntu
```

### Installing the node

I have not personally tested this but I think once you are into Ubuntu you could simply install the [q1-node-manager.md](../../q1-node-manager.md "mention") and take it from there.

One issue you could have on Windows is related to option 1 in the menu (Prepare your server). That script does various operations on your machine that could throw errors for Windows.

If so, no problem, just move directly to option 2 and 3.

Remember, you can also follow the [node-auto-installer.md](../../node-auto-installer.md "mention") if the QONE menu is not working for you.

Finally, f you have issues with these automated scripts, simply follow the [node-step-by-step-installation.md](node-step-by-step-installation.md "mention") instead.

### Installing the qclient

The qclient is a software that allows you to manage your QUIL tokens without having to run a node.

If you want to install the qclient on Windows WSL without running a node simply follow these steps:

Create the ceremonyclient and client folders:

```bash
mkdir ceremonyclient && cd ceremonyclient && mkdir client && cd client
```

Set release OS and arch variables (change these if needed - on Windows WSL they shoudl be ok):

```bash
release_os="linux"
release_arch="amd64"
```

download qclient:

{% code overflow="wrap" %}
```bash
files=$(curl https://releases.quilibrium.com/qclient-release | grep $release_os-$release_arch)
for file in $files; do
    qclient_version=$(echo "$file" | cut -d '-' -f 2)
    if ! test -f "./$file"; then
        curl "https://releases.quilibrium.com/$file" > "$file"
        echo "... downloaded $file"
    fi
done
mv qclient-$qclient_version-$release_os-$release_arch qclient
chmod +x ./qclient
```
{% endcode %}

Done!

Now you should be able to use the [qclient-commands.md](../qclient/qclient-commands.md "mention")

These will only work after v2.0

<table data-card-size="large" data-column-title-hidden data-view="cards" data-full-width="false"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><strong>The Best Server Providers for your Nodes</strong></td><td>CLICK TO SEE THEM</td><td><a href="../../best-server-providers.md">best-server-providers.md</a></td><td></td><td><a href="../../.gitbook/assets/best-serve-providers-banner-text-1-1-B.jpg">best-serve-providers-banner-text-1-1-B.jpg</a></td></tr><tr><td><strong>Want to say thank you?</strong></td><td>CLICK TO DONATE</td><td><a href="../../want-to-say-thank-you.md">want-to-say-thank-you.md</a></td><td></td><td><a href="../../.gitbook/assets/donations-banner-text-1-1-B.jpg">donations-banner-text-1-1-B.jpg</a></td></tr></tbody></table>

