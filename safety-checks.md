# ✅ Safety checks

### **Before following this guide, make sure that the guide URL is correct!**&#x20;

Check in the [Telegram official links ](https://t.me/quilibrium/26474)the link of the guide "Node setup guide by LaMat" - it should be [https://iri.quest/quilibrium-node-guide](https://iri.quest/quilibrium-node-guide) and redirect to this same URL you are on now.

Remember, someone could have cloned this guide and insert into them malicious scripts, so this check is very important!

### Auto-installers script: safety concerns

This [auto-installer script](archive/old-node-auto-installer.md), as well as all the other installers you find in the guide, combines all the necessary steps to perform actions such as preparing the server, installing the node, or updating the node into a one-click solution. If you have any doubts about their safety, you can inspect the source code of these installers on GitHub.

If you are not familiar with code, you can simply copy/paste the whole code in a chatbot such as ChatGPT (or any open-source alternative) and ask them to explain it to you step by step.

#### **How to inspect the source code of a script URL?**

For instance, if you see a command like this:

```bash
wget --no-cache -O - https://raw.githubusercontent.com/lamat1111/quilibrium-node-auto-installer/1.4.18/server_setup | bash
```

You can inspect the source code by following these steps:

1. Take the part of the URL after the domain: `/lamat1111/quilibrium-node-auto-installer/1.4.18/server_setup`.
2. Add `https://github.com` at the beginning.
3. Insert `/blob/` before the version number.

So, the complete URL to visit in this case would be:

```url
https://github.com/lamat1111/quilibrium-node-auto-installer/blob/1.4.18/server_setup
```

By visiting this URL, you can review the source code of the script to ensure it is safe.

***

