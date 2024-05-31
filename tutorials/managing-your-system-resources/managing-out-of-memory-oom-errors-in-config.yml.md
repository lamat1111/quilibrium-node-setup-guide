# ☑️ Managing Out of Memory (OOM) errors in config.yml

If you're encountering Out of Memory (OOM) errors in your system, and you haven't followed the recommended 1:2 ratio between CPU cores and RAM, there's a solution available within the configuration settings of your system.&#x20;

This tutorial will guide you through the process of using the `dataWorkerMemoryLimit` setting in your `ceremonyclient/node/.config/config.yml` file to mitigate OOM errors.

### **Stop your service:**

```sh
sudo systemctl stop ceremonyclient
```

### **Locate Your Configuration File**

Find and open your `ceremonyclient/node/.config/config.yml` file. This file typically contains various configuration settings for your system.

### **Navigate to the Engine Settings**

Within the `config.yml` file, locate the section related to the engine settings. This is where you'll make the necessary adjustments.

### **Set the `dataWorkerMemoryLimit`**

Under the engine heading, add or modify the `dataWorkerMemoryLimit` parameter. This parameter allows you to specify the memory limit for each worker (core/thread) in bytes.

```yaml
engine:
  dataWorkerMemoryLimit: [memory_limit_in_bytes]
```

### **Calculate the Memory Limit**

{% hint style="info" %}
Keep in mind that while adjusting the memory limit can help alleviate OOM errors, it's still recommended to have at least 2GB of physical memory per worker for optimal performance.&#x20;
{% endhint %}

Determine the appropriate memory limit based on your system's specifications. The default allocation is 1.75GB per worker. If your system has less memory available, adjust the limit accordingly.

For example, to allocate 500MB per worker: 500 \* 1024 \* 1024 = 524288000

```bash
engine:
  dataWorkerMemoryLimit: 524288000
```

Similarly, for 875MB per worker: 875 \* 1024 \* 1024 = 917504000

```bash
engine:
  dataWorkerMemoryLimit: 917504000
```

### **Apply the Configuration**

Save the changes to your `config.yml` file.

### **Delete the SELF\_TEST file**

This step is crucial to prevent your node from being disqualified for cheating:

```sh
rm ~/ceremonyclient/node/.config/SELF_TEST
```

{% hint style="info" %}
The SELF\_TEST file tells the newtork your node capabilities. If you change specs, you need to delete it so the system can generate a new one. If you don't delete it, you will be lying to the newtork and thus risking to be disqualified.
{% endhint %}

### **Restart your service**

```sh
sudo systemctl start ceremonyclient
```

***

<table data-card-size="large" data-column-title-hidden data-view="cards" data-full-width="false"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><strong>The Best Server Providers for your Nodes</strong></td><td>CLICK TO SEE THEM</td><td><a href="../../best-server-providers.md">best-server-providers.md</a></td><td></td><td><a href="../../.gitbook/assets/best-serve-providers-banner-text-1-1-B.jpg">best-serve-providers-banner-text-1-1-B.jpg</a></td></tr><tr><td><strong>Want to say thank you?</strong></td><td>CLICK TO DONATE</td><td><a href="../../want-to-say-thank-you.md">want-to-say-thank-you.md</a></td><td></td><td><a href="../../.gitbook/assets/donations-banner-text-1-1-B.jpg">donations-banner-text-1-1-B.jpg</a></td></tr></tbody></table>
