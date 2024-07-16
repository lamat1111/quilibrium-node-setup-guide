# 🪟 Installing the node in Windows WSL

{% hint style="danger" %}
UNTESTED - WORK IN PROGRESS
{% endhint %}

Clone Quilibrium software

{% code overflow="wrap" %}
```sh
cd ~ && git clone https://github.com/QuilibriumNetwork/ceremonyclient.git
```
{% endcode %}

Move to branch release

{% code overflow="wrap" %}
```sh
cd ~/ceremonyclient/ && git checkout release
```
{% endcode %}

Start node

<pre class="language-sh" data-overflow="wrap"><code class="lang-sh"><strong>cd ~/ceremonyclient/node &#x26;&#x26; ./release_autorun.sh
</strong></code></pre>

