# 🪟 Installing the node in Windows WSL

{% hint style="danger" %}
UNTESTED - WORK IN PROGRESS
{% endhint %}

Clona il software di Quilbrium

```sh
cd ~
git clone https://source.quilibrium.com/quilibrium/ceremonyclient.git
```

Se il comando sopra non funziona, prova questo:

```sh
cd ~
git clone https://git.quilibrium-mirror.ch/agostbiro/ceremonyclient.git
```

Dopo aver clonato con successo il codice, passa al ramo release:

```sh
cd ~/ceremonyclient/
git checkout release-cdn
```

Avvia il nodo

<pre class="language-sh"><code class="lang-sh"><strong>cd ~/ceremonyclient/node
</strong>./release_autorun.sh
</code></pre>

