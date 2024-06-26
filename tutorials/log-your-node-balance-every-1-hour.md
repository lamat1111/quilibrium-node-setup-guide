# 💲 Log your node balance every 1 hour

This script will check your QUIL balance every 1 hour and log it in a CSV file that you can view or download. The CSV file will look like this:

```
"time","balance"
"26/06/2024 14:00","13,45367"
"26/06/2024 15:00","14,34256"
```

You can then import it on a Google sheet, divide the data in columns, and run all kind of formulas to calculate daily rewards, averages, growth in % etc.

{% hint style="info" %}
Your node need to be running for ta least 30 minutes before you can check and log the balance, and you need to have already [set-up-the-grpc-calls.md](../set-up-the-grpc-calls.md "mention")
{% endhint %}

### Step 1 - install the script

{% hint style="warning" %}
Follow the [safety-checks.md](../safety-checks.md "mention") before running this script in your server
{% endhint %}

{% code overflow="wrap" %}
```bash
wget -O - https://raw.githubusercontent.com/lamat1111/QuilibriumScripts/main/tools/qnode_balance_checker_installer.sh | sh
```
{% endcode %}

### Step 2 - see or download the balance log

After installing the script, you can view your balance log by running:

<pre class="language-bash"><code class="lang-bash"><strong>cat ~/scripts/balance_log.csv
</strong></code></pre>

Or you can download the CSV file directly via this script:

{% code overflow="wrap" %}
```bash
mkdir -p ~/scripts && wget -O ~/scripts/qnode_balance_log_download.sh https://raw.githubusercontent.com/lamat1111/QuilibriumScripts/main/tools/qnode_balance_log_download.sh && chmod +x ~/scripts/qnode_balance_log_download.sh && ~/scripts/qnode_balance_log_download.sh
```
{% endcode %}

The second time you want to download it, you just need to run :

```
 ~/scripts/qnode_balance_log_download.sh
```

***

<table data-card-size="large" data-column-title-hidden data-view="cards" data-full-width="false"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><strong>The Best Server Providers for your Nodes</strong></td><td>CLICK TO SEE THEM</td><td><a href="../best-server-providers.md">best-server-providers.md</a></td><td></td><td><a href="../.gitbook/assets/best-serve-providers-banner-text-1-1-B.jpg">best-serve-providers-banner-text-1-1-B.jpg</a></td></tr><tr><td><strong>Want to say thank you?</strong></td><td>CLICK TO DONATE</td><td><a href="../want-to-say-thank-you.md">want-to-say-thank-you.md</a></td><td></td><td><a href="../.gitbook/assets/donations-banner-text-1-1-B.jpg">donations-banner-text-1-1-B.jpg</a></td></tr></tbody></table>
