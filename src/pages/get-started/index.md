---
title: "Get Started: UXP for Adobe Media Encoder"
description: "Set up Media Encoder, build your first UXP plugin, and start working with the Media Encoder API."
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

# Build for Media Encoder

A Media Encoder plugin is a UXP panel that runs inside Adobe Media Encoder and controls it through the Media Encoder API. From a panel you can add sources to the render queue, apply presets and render settings, start and monitor encodes, and manage watch folders.

The steps below follow the order you will work in: set up the host, run a reference sample to see the API in action, then use the API reference to build your own plugin.

<InlineAlert variant="info" slots="text"/>

UXP for Adobe Media Encoder is in public beta. APIs and tooling may change before general availability.

1. [Set up Media Encoder](developer-tools/index.md). Check the required versions, enable Developer Mode, and confirm the host loads plugins from the UXP Developer Tool.
2. [Explore the Render Queue Panel example](samples/render-queue-panel/index.md). Clone, build, and load a working TypeScript panel that exercises the Media Encoder DOM APIs: adding jobs to the render queue, changing render options, and starting, pausing, and stopping renders. It is the fastest way to see how the API behaves before you write your own.
3. Build your own plugin. Browse the [Media Encoder API reference](../media-encoder-api/index.md) for the render queue, render options, jobs, watch folders, and progress reporting, then wire the same calls into your panel.
