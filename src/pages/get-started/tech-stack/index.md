---
title: "UXP Tech Stack for Adobe Media Encoder"
description: "Find the canonical UXP tech stack guide and the shared API reference used when building Adobe Media Encoder plugins."
keywords:
  - UXP
  - Adobe Media Encoder
  - tech stack
  - JavaScript
  - HTML
  - CSS
  - Spectrum
  - runtime
contributors:
  - https://github.com/karan0207
---

# UXP Tech Stack

Media Encoder plugins use the same HTML, CSS, JavaScript runtime, UI system, and development tools as plugins for every other UXP-enabled Adobe application. The canonical explanation is maintained in the UXP Hub.

<DiscoverBlock slots="link, text"/>

[Read the UXP Tech Stack Guide](https://developer-stage.adobe.com/uxp/guides/explanation/tech-stack/?aio_external)

Learn how HTML, CSS, JavaScript, Spectrum components, and the UXP runtime fit together across hosts.

<DiscoverBlock slots="link, text"/>

[Browse the UXP API Reference](https://developer-stage.adobe.com/uxp/uxp-api/?aio_external)

Check the exact HTML elements, CSS features, JavaScript globals, modules, and Spectrum components supported by UXP.

## Media Encoder Layer

After choosing supported UXP capabilities, use the [Media Encoder API](../../media-encoder-api/index.md) for the render queue, jobs, presets, watch folders, and progress reporting.
