---
layout: page
title: About
permalink: /about/
---

The Xen for Android Project (xen4android) aims to develop a secure, paravirtualized execution environment for multiple isolated Android instances on both mobile and desktop platforms.

Xen4android is an open source community effort to create a more-isolated mobile OS. The goals of this project are to make a free collection of tools to:

 * Deploy isolated instances of Android under a hypervisor
 * Release a distribution based on this that is compatable with both desktop and mobile hardware
 * Offer minimal to no performance degredation compared to a non-paravirtualized system
 * Allow this distribution to be easily-modified and adaptable to new hardware

That is to say, xen4andoid aims to build a software distribution that can be run on, modified using, and ported to both regular desktop systems as well as consumer android phones.

Xen4android offers several benefits compared to a non-PV version of Android. By running virtualized concurrent Android instances, applications and data can be completely isolated from one another.
This provides far greater security compared to regular sandboxing techniques, as even privileged processes running in one instance cannot access any information from the other.
Additionally, xen4android brings about the possibility of running multiple versions of Android simultaneously; allowing users to install legacy builds alongside more-recent instances without compromising security.

For additional information, check out the xen4android wiki, or visit us on #xen4android in Freenode.
