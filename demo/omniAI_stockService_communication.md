# OmniAI and Stock Service Communication

OmniAI when prompted with a text that contains the **keyword "latest"** and a **ticker symbol** **among "TSLA", "AAPL", "GOOGL", "AMZN", "MSFT", and "NFLX"** will fetch the last 30-day stock data and their corresponding technical indicators from Stock Service data provider. This bidirectional communication between machines requires valid VC JWT for both parties to be successful.

**Important Notice:** As of December 2024, our beta repositories and corresponding demos are no longer functioning. This is due to TBD discontinuing operations and shutting down their gateway node on the DHT network. For more information, see [TechCrunch's article on Block scaling back investments](https://techcrunch.com/2024/11/07/block-scales-back-tidal-investment-and-shutters-tbd-in-favor-of-bitcoin-mining/).

<!-- * OmniAI URL: [http://172.86.114.187:8001/](http://172.86.114.187:8001/)   -->
<!-- * Stock Service URL: [http://172.86.114.187:8002/](http://172.86.114.187:8002/)   -->
<!-- * Wireshark URL for visualizing HTTP communication between machines: [http://172.86.114.187:14500/?floating\_menu=false\&password=wireshark\&sharing=true](http://172.86.114.187:14500/?floating_menu=false&password=wireshark&sharing=true)  
  * Select `Loopback: lo` interface.  
  * Fill `http && (tcp.port == 8001 || tcp.port == 8002)` in the filter box to visualize communication between OmniAI and Stock Service only. -->

![Wireshark](../images/omni_to_stock.png)

[Back to Index](../index.md) | [Previous: OmniAI-WealthWhisperer Communication](./omniAI_wealthWhisperer_communication.md)
