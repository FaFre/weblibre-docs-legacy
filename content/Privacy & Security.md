WebLibre is built with privacy and security at its core. Our browser uses reproducible builds via GitHub Actions, and all parts of the Web Engine and Components are sourced from Mozilla’s official Maven repositories.

## Content Blocking

During on-boarding, you can choose to install [uBlock Origin](https://github.com/gorhill/uBlock), a powerful and widely trusted content blocker. This add-on helps block ads, trackers, and other unwanted content, enhancing your privacy and browsing experience from the start.

- **Opt-in:** uBlock Origin is optional and only enabled with your consent.

## Hardening & Advanced Controls

WebLibre provides robust options to strengthen your privacy and security:

- **Extensive Settings:** Access a comprehensive Settings menu to configure hardening options for the Gecko Engine and Mozilla Android Components.
- **`about:config`:** Advanced users can access ```about:config``` for fine-grained control over browser internals, mirroring the flexibility found in Firefox.
- **Container Isolation:** Use [[Container]] to separate browsing contexts, isolate cookies, and even route specific containers through a Tor Proxy for enhanced anonymity.
- **[[Biometric Authentication]]:** Restrict access to sensitive containers using your device’s biometric features (fingerprint or face recognition).
- **[[Tor Proxy]] Integration:** Route selected containers or private tabs through the Tor network for additional privacy.

## Local-First Data Handling

WebLibre is designed with a local-first philosophy:

- **No tracking:** We do not use tracking or monitoring technologies that transmit your data to us.
- **Local storage:** All browsing data, history, and search indexes remain on your device, never sent to our servers.
- **Personal Search Engine:** Search across tabs, web feeds, and history without relying on third-party search providers.

## Additional Security Features

- **Private Tabs:** Easily switch between regular and private tabs. Private tabs erase all data on app restart and never share cookies with other tabs or containers.
- **[[Container Cookie Contexts]]:** Each container maintains its own cookie storage, preventing cross-site tracking and session leakage.
- **Granular Permissions:** WebLibre only accesses device features (like location or files) when you explicitly allow it.

## Transparency & Open Source

- **Reproducible Builds:** Every release is built using public, automated workflows, ensuring that the published app matches the source code.
- **Open Source:** All code is available for review and contribution on [GitHub](https://github.com/FaFre/WebLibre).

