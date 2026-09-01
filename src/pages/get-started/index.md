---
title: "Get Started: UXP for Adobe Media Encoder"
description: "Choose the right starting path for UXP fundamentals or Adobe Media Encoder-specific plugin development."
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

Building for Media Encoder combines two layers: the shared UXP platform and Media Encoder's host-specific APIs. Choose your path based on your UXP experience.

<InlineAlert variant="info" slots="text"/>

UXP for Adobe Media Encoder is in public beta. APIs and tooling may change before general availability.

## Choose Your Starting Point

<Cards slots="image, heading, text, links" repeat="2" width="100%" />

![Learn the shared UXP platform](../images/uxp-tutorials.svg)

### New to UXP?

Begin with the UXP Hub. It covers the shared developer journey: foundations, tools, plugin concepts, building and debugging, migration, and publishing.

[Start with the UXP Developer Journey](uxp-developer-journey/index.md)

![Build plugins for Adobe Media Encoder](../images/media-encoder.svg)

### Already Know UXP?

Go directly to the Media Encoder path: check host requirements, enable Developer Mode, build a plugin, and explore the host API.

[Start with Media Encoder](developer-tools/index.md)

## Recommended Developer Journey

If UXP is new to you:

1. [Learn the shared UXP platform](uxp-developer-journey/index.md) in the UXP Hub.
2. [Set up Media Encoder](developer-tools/index.md) as your host application.
3. [Build your first Media Encoder plugin](build-your-first-plugin/index.md).
4. [Explore the Render Queue Panel](samples/render-queue-panel/index.md) to see host APIs working together.
5. Use the [Media Encoder API reference](../media-encoder-api/index.md) as you build your own integration.

If you already build UXP plugins for another host, begin at step 2.

## Moving Existing Work

Coming from CEP or ExtendScript? Follow the [migration path](migrate-to-uxp/index.md) before replacing host calls with the Media Encoder API.
