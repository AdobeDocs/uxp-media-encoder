---
title: UXP for Adobe Media Encoder
description: "Build plugins and automation for Adobe Media Encoder with UXP: create panels, automate the encoding queue, and script batch workflows."
contributors:
  - https://github.com/karan0207
---

<Superhero variant="halfWidth" textColor="white" slots="heading, text, image" background="rgb(64, 34, 138)"/>

# Automate Adobe Media Encoder with UXP

Build plugins in HTML, CSS, and JavaScript that run inside Media Encoder, discover presets, and drive the encoding queue. Turn repetitive exports into automated, one-click workflows, the modern successor to ExtendScript.

![Build UXP plugins and automation for Adobe Media Encoder](images/hero.svg)

<Resources slots="heading, links"/>

#### Resources

* [Quickstart Guide](https://developer.adobe.com)
* [Analytics Github Repo](https://github.com/AdobeDocs/dev-site)

## Overview

Media Encoder is built for repetition: the same presets, the same delivery codecs, the same render queue, run again and again. UXP is how you take control of that work in code. It lets you build plugins that run inside Media Encoder using HTML, CSS, and JavaScript, and it is the modern replacement for the older CEP and ExtendScript tooling.

You extend Media Encoder in two ways, and most projects use both:

* **Panels** add interactive UI inside the app, custom controls, preset pickers, or a queue dashboard that sits alongside the native interface.
* **Scripts** drive Media Encoder programmatically: inspect the encoding queue, add and start jobs, choose presets, and run unattended batch exports with no manual clicks.

Both run on the same UXP engine, so your logic, libraries, and patterns carry across panels, automation, and other UXP-enabled Adobe applications. While you build, the UXP Developer Tool (UDT) loads your plugin, hot-reloads changes, and connects a debugger.

<InlineAlert variant="info" slots="text"/>

UXP for Adobe Media Encoder is in public beta. APIs and supported capabilities may change before general availability.

## Start Building

Set up your environment and run your first automation inside Media Encoder.

<DiscoverBlock slots="link, text"/>

[Get Started](guides/getting-started/index.md)

Set up your environment and load a panel with the UXP Developer Tool.

<DiscoverBlock slots="link, text"/>

[Plugins](guides/index.md)

Manifests, entry points, panels, and recipes for common encoding tasks.

<DiscoverBlock slots="link, text"/>

[Migrate from CEP](guides/migrating/index.md)

What carries over from ExtendScript and what changed.

## API Reference

The platform and Media Encoder APIs your plugin calls.

<DiscoverBlock slots="link, text"/>

[UXP API](uxp-api/index.md)

File system, networking, storage, and Spectrum UI components.

<DiscoverBlock slots="link, text"/>

[Media Encoder API](media-encoder-api/index.md)

The encoding queue, presets, jobs, and scripting automation.

## Resources

APIs and samples when you need them.

<DiscoverBlock slots="link, text"/>

[API Playground](api/index.md)

Try UXP and Media Encoder APIs interactively.
