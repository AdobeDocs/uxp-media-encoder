---
title: "Developer Tools: UXP for Adobe Media Encoder"
description: "Use the UXP Developer Tool (UDT) to scaffold, load, hot-reload, and debug UXP plugins inside Adobe Media Encoder."
keywords:
  - UXP
  - Adobe Media Encoder
  - UXP Developer Tool
  - UDT
  - debugging
  - hot reload
contributors:
  - https://github.com/karan0207
---

# Developer Tools

The UXP Developer Tool (UDT) is the desktop app you use to build UXP plugins. It scaffolds a new plugin, loads it into Media Encoder, reloads it as you edit, and opens a debugger, all without an install step.

<InlineAlert variant="info" slots="text"/>

UDT is required for development. Start Media Encoder before you load a plugin, and keep it running while you work.

## What UDT does

* **Scaffold**: create a starter plugin with a valid `manifest.json` that targets Media Encoder.
* **Load**: register your plugin with Media Encoder so its panel appears in the workspace.
* **Reload**: apply code changes in place, so you can iterate without restarting Media Encoder.
* **Debug**: attach Chrome DevTools to inspect the DOM, read console output, and set breakpoints.

## A typical session

1. Open UDT and create or add your plugin.
2. Set the host application to Adobe Media Encoder.
3. Start Media Encoder and wait until it is fully open.
4. In UDT, click **Load**. The panel appears in Media Encoder.
5. Edit your code, then click **Reload** to see the change.
6. Click **Debug** to open DevTools when you need to inspect or step through code.

## If Media Encoder does not appear

* Update UDT to the latest version, then start Media Encoder before refreshing UDT.
* Confirm your plugin's `manifest.json` sets the host app to Media Encoder.
* If a manifest change is not applied, unload the plugin in UDT and load it again.

## Next

<DiscoverBlock slots="link, text"/>

[Tech Stack Foundations](../tech-stack/index.md)

Understand the runtime and web technologies your plugin uses.
