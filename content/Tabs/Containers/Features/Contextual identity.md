---
title: Contextual identity
draft: false
---
[[Container]] can specify their own cookie contexts that are inherited to their tabs.

With this container feature enabled, website cookies of the containing tabs are put into the same "jar". This means cookies like login information for websites are shared within one contextual identity (multiple tabs can access them) but not outside them. Private tabs will always have a separate cookie handling.