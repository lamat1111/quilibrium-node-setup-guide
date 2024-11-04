---
icon: bridge
---

# How to Bridge QUIL to WQUIL

### Prerequisites

* Ethereum-compatible browser wallet
* Minimum $100 worth of ETH for gas fees
* Latest QClient version installed

### Step-by-Step Instructions

1. Navigate to [https://quilibrium.com/bridge](https://quilibrium.com/bridge)
2. Enter your QUIL account address
3. **Important**: Save the displayed coin addresses. These are essential for recovery if the bridge operation fails
4. Select a coin address to bridge
5.  Execute the `cross-mint` command shown on the bridge page using QClient. Example command:

    {% code overflow="wrap" %}
    ```bash
    /root/ceremonyclient/client/qclient-2.0.2.4-linux-amd64 --config /root/ceremonyclient/node/.config cross-mint 0x7472sb2b2gs2gdhe3yge3ydw8d9ec1f9024f9829526bd5shy373egshbb80e40760e7d3e81c394d973781acswywg62s064bdb5adhu3hdh7gda9f9730d69fsgwtw53dud789d6ee2
    ```
    {% endcode %}

    _Note: Paths, OS, architecture, and version may vary. See_ [qclient-commands-for-token-transfers.md](../../qclient-commands-for-token-transfers.md "mention") _for details._
6. Copy the QClient response into the bridge page field (don't press Enter)
7. Run a second `cross-mint` command as shown on the bridge page to verify account ownership
8. Copy the second QClient response into the bridge field (don't press Enter)
9. **Important**: Do not refresh the page. Wait for the "Complete Bridge" button to appear, then click it
10. Approve the bridging transaction in your browser wallet when prompted
11. Save the transaction ID for future reference on Etherscan

### Troubleshooting

If you encounter issues, refer to the guide [how-to-retrieve-your-coin-address-after-a-failed-bridging-operation.md](how-to-retrieve-your-coin-address-after-a-failed-bridging-operation.md "mention")



<table data-card-size="large" data-column-title-hidden data-view="cards" data-full-width="false"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><strong>The Best Server Providers for your Nodes</strong></td><td>CLICK TO SEE THEM</td><td><a href="../../best-server-providers.md">best-server-providers.md</a></td><td></td><td><a href="../../.gitbook/assets/best-serve-providers-banner-text-1-1-B.jpg">best-serve-providers-banner-text-1-1-B.jpg</a></td></tr><tr><td><strong>Want to say thank you?</strong></td><td>CLICK TO DONATE</td><td><a href="../../want-to-say-thank-you.md">want-to-say-thank-you.md</a></td><td></td><td><a href="../../.gitbook/assets/donations-banner-text-1-1-B.jpg">donations-banner-text-1-1-B.jpg</a></td></tr></tbody></table>
