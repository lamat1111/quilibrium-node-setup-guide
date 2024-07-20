# 🪟 Installing the node and the qclient on Windows WSL

_In Windows there is an option to run Linux via a feature called WSL._

### Activating WSL and installing Ubuntu

Activate WSL on Windows to be able to run Linux and Ubuntu. Here is a great tutorial: [https://www.youtube.com/watch?v=vxTW22y8zV8](https://www.youtube.com/watch?v=vxTW22y8zV8) (you just need to follow the first 7 minutes or so)

Once you have Linux available and Ubuntu installed, to access Ubuntu via terminal you run:

```
wsl -d Ubuntu
```

### Installing the node

I have not personally tested this but I think once you are into Ubuntu you could simply install the [q.one-node-quickstart-menu.md](../q.one-node-quickstart-menu.md "mention") and take it from there.

One issue you could have on Windows is related to option 1 in the menu (Prepare your server). That script does various operations on your machine that could throw errors for Windows.

If so, no problem, just move directly to option 2 and 3.

Remember, you can also follow the [node-auto-installer.md](../node-auto-installer.md "mention") if the QONE menu is not working for you.

Finally, f you have issues with these automated scripts, simply follow the [node-step-by-step-installation.md](node-step-by-step-installation.md "mention") instead.

### Installing the qclient

The qclient is a software that allows you to manage your QUIL tokens without having to run a node.

If you want to install the qclient on Windows WSL without running a node simply follow these steps:



