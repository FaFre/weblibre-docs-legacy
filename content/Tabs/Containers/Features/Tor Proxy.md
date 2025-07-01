---
title: Tor Proxy
draft: false
---
A **Tor proxy** is a privacy-enhancing tool that routes your internet traffic through the **Tor (The Onion Router) network**. By relaying your requests through multiple encrypted nodes (relays) worldwide, Tor helps **anonymize your online activities** and protect your identity.

## How Tor Proxy Works

- **Multi-layered Encryption:** Each request is encrypted multiple times and sent through a series of Tor relays. Each relay decrypts only enough information to know where to send the data next, but never the full path or the original source.
- **Anonymity by Design:** This process makes it **extremely difficult to trace your internet activity** back to you. No single relay knows both your identity and your destination.

## Common Uses of Tor Proxy

- **Bypassing censorship** and geographic restrictions
- **Protecting privacy** from surveillance and monitoring
- **Shielding browsing habits** from ISPs and third-party trackers

## Important Notes

- **WebLibre’s Tor Service** is designed to enhance privacy, **not to guarantee complete anonymity**. In certain scenarios, your real IP address or identity may still be exposed.
- For **maximum anonymity*, use the official [Tor Browser](https://www.torproject.org/download/).

---

## How to Use the Tor Service

### Initial Setup

When you enable the Tor Proxy, an initial **bootstrapping process** occurs, typically taking 10–60 seconds. During this time, Tor:

- Performs cryptographic handshakes
- Selects relays
- Establishes secure tunnels

Once bootstrapped, browsing uses pre-built circuits, with new circuits created periodically for ongoing privacy.

### Using with [[Container]]

- Enable Tor Proxy via the [[Container]] feature.
- All tabs assigned to a Tor-enabled container will connect through the Tor network.
- **Note:** This requires a separate [[Container Cookie Contexts]] for privacy. Only normal (non-private) tabs are supported.

#### Video

<div style="position: relative; padding-top: 112.235%;"><iframe title="WebLibre - Container with Tor" width="100%" height="100%" src="https://peertube.ondevice.eu/videos/embed/nqVSFNRDyn4abXHer6wR3e" frameborder="0" allowfullscreen="" sandbox="allow-same-origin allow-scripts allow-popups allow-forms" style="position: absolute; inset: 0px;"></iframe></div>

### Private Tabs

- Due to limitations in the Gecko engine, fine-grained control (as with containers) is not available for private tabs.
- You can choose to route **all or none** of your private tabs through the Tor Proxy.
- The setting for private tab routing is available on the Proxy page.

---

## Why Choose Tor Over VPN?

- **Stronger Anonymity:** Tor’s multi-layered encryption and distributed network provide **greater anonymity** than VPNs, which only shift trust from your ISP to the VPN provider.
- **No Single Point of Failure:** Tor’s **decentralized architecture** means no single entity can compromise your entire connection, unlike VPNs where the provider can see all your traffic.
- **Free and Open Source:** Tor is **completely free** and its source code is publicly available for audit. Quality VPNs typically require a paid subscription.
- **No Central Trust Required:** With Tor, you do **not need to trust any single company** with your data. The distributed design ensures no single node has the full picture.

---

**For the highest level of anonymity and access to the full Tor network, always use the official Tor Browser.**

