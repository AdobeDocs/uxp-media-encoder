---
title: "Get Started: UXP for Adobe Media Encoder"
description: "Start building UXP plugins and automation for Adobe Media Encoder: the development loop, prerequisites, and the essentials you need before your first panel."
keywords:
  - UXP
  - Adobe Media Encoder
  - getting started
  - UXP Developer Tool
  - UDT
  - panels
  - scripting
contributors:
  - https://github.com/karan0207
---

# Get Started with UXP for Media Encoder

This section gets you from zero to a running plugin. You write in HTML, CSS, and JavaScript, load your plugin into Media Encoder with the UXP Developer Tool, and call Media Encoder's APIs to drive the encoding queue.

<InlineAlert variant="info" slots="text"/>

UXP for Adobe Media Encoder is in public beta. Load plugins with the UXP Developer Tool, keep Media Encoder running while you develop, and expect APIs and tooling to change.

## The development loop

Three pieces work together, and knowing each role makes every later step easier to reason about:

* **Media Encoder** is the host. Your plugin loads here, its panel renders here, and your code runs here against the Media Encoder APIs.
* **The UXP Developer Tool (UDT)** is the bridge. It scaffolds your plugin, then loads, reloads, and debugs it inside Media Encoder.
* **Your code editor** is where you write the HTML, CSS, and JavaScript.

The loop is short: write code, reload in UDT, see the change in Media Encoder, then run an encode and watch it in the queue.

## Prerequisites

* Adobe Media Encoder (beta), installed and running.
* The UXP Developer Tool (UDT).
* A code editor, such as VS Code.
* Helpful but not required: basic HTML and JavaScript.

## Essentials

Read these first if UXP or extensibility is new to you.

<DiscoverBlock slots="link, text"/>

[Developer Tools](developer-tools/index.md)

Install and use the UXP Developer Tool to scaffold, load, hot-reload, and debug your plugin.

<DiscoverBlock slots="link, text"/>

[Tech Stack Foundations](tech-stack/index.md)

The web technologies and the UXP runtime your plugin is built on.

<DiscoverBlock slots="link, text"/>

[Nomenclature](nomenclature/index.md)

The terms used across these docs: plugins, panels, scripts, manifests, and how they map to CEP and ExtendScript.

## Coming from ExtendScript?

If you have automated Media Encoder before, UXP is the modern path. See [Migrate from CEP and ExtendScript](../plugins/migrating/index.md) for what carries over and what changed.
