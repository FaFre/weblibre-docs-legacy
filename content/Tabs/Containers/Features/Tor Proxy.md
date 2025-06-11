---
title: Tor Proxy
draft: false
---
A **Tor proxy** is a privacy tool that routes internet traffic through **The Onion Router (Tor) network** to anonymize users' online activities. When you use Tor as a proxy, your internet requests are **encrypted and bounced through multiple relay servers** (nodes) around the world before reaching their destination.

This multi-layered routing process makes it **extremely difficult to trace** the original source of the traffic, providing strong anonymity protection. Each relay only knows the previous and next step in the chain, not the complete path.

Tor proxy is commonly used to:

- **Bypass censorship** and geographic restrictions
- **Protect privacy** from surveillance
- **Shield browsing habits** from ISPs and trackers

Note that WebLibre implemented the Tor Service to improve users privacy, **not to provide complete anonymity**. It might be possible that your real IP/Identity is leaked in certain scenarios. It is also not possible to access .onion sites and the implementation is not scope of this project. For a hardened implementation use the specifically designed Tor Browser.

## Why Tor over VPN? 

We recommend using Tor over VPNs for various reasons:

**True Anonymity**: Tor provides **stronger anonymity** through its multi-layered encryption and distributed network. VPNs only shift trust from your ISP to the VPN provider, who can still see your traffic.

**No Single Point of Failure**: Tor's **decentralized network** means no single entity controls or can compromise your entire connection, unlike VPNs where the provider has complete visibility.

**Free and Open Source**: Tor is **completely free** and its code is publicly auditable, while quality VPNs require paid subscriptions.

**No Trust Required**: You don't need to **trust any single company** with your data, as the distributed network design prevents any one node from seeing the complete picture.

## How to use the Tor Service?

Enabling Tor proxy works through the [[Container]] feature. Once set, all assigned container tabs are forced to connect through the Tor proxy to the internet. Note that this feature requires a separate [[Contextual identity]] to ensure the users privacy. Both normal and private tabs are supported.

When you initially set up the Tor Proxy, the initial **bootstrapping process** typically takes up 10-60 seconds. This **bootstrapping process** involves cryptographic handshakes, relay selection, and establishing secure tunnels before any actual browsing can begin. Once established, subsequent browsing uses the pre-built circuits, though new circuits are periodically created. 
