---
layout: page
title: Architecture
permalink: /architecture/
---

![Xen for Android Architecture]({{ "/assets/img/xen4android-architecture.png" | absolute_url }})

### Architecture Notes
The Xen for Android architecture aims to be as compatible for current Android mobile hardware as possible.
However, this does not mean that it is not extensible; the xen4android subsystems are designed to make porting to additional platforms as painless as possible.
These notes give a high-level overview of the core architecture encompassing the distribution.

#### Xen
Xen replaces the stock Linux kernel present in the `boot` partition of most Android handsets.
Its purpose is to start provide an initial environment to bootstrap Dom0, and provide a virtualized environment for all running DomUs.
The Xen kernel is semi-portable, only requiring a minimal set of platform-specific drivers during boot-up.
All other drivers are provided by Dom0 via hardware passthrough.

#### Dom0
Dom0 is responsible for providing a unified driver interface for all running Android instances, and for instructing Xen to start, stop, create, and destroy DomUs.
It contains a minimal rootfs that holds Android hardware drivers running under libhybris (on phones) or PC drivers (on desktops), as well as a small daemon utility that communicates with the Dom0 Linux kernel.
The kernel is responsible for receiving paravirtualized calls from the other DomUs (e.g. framebuffer writes, touchscreen input, etc.) and selectively routing these packets to the appropriate driver.
Drivers in Dom0 communicate to the hardware via passthrough mechanisms exposed by Xen.

#### DomU
Each DomU contains a running instance of Android.
They contain a modified kernel designed to intercept driver queries and securely route it to Dom0 using PV calls.
Users typically interact with one DomU instance at a time, with all others given background priorities, and hidden from the current framebuffer.
Switching between DomUs is facilitated by a special key sequence that gives device control back to Dom0.

### Boot Sequence
 * GRUB/uBoot/Custom bootloader loads Xen into memory
 * Xen takes control of execution, bootstraps the system, and starts Dom0
 * Dom0 loads all the necessary drivers, initiates the PV communication channel, and instructs Xen to start DomUs
 * DomU instances are started
