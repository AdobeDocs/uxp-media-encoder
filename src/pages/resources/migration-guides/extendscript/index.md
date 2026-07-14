---
title: ExtendScript Migration Guide
description: Move ExtendScript-based automation to UXP's JavaScript APIs
keywords:
  - migration
  - ExtendScript
  - JSX
  - UXP
contributors:
  - https://github.com/kasivn
---

# ExtendScript Migration Guide

<InlineAlert variant="info" slots="heading, text" />

Content pending

This guide is a placeholder. It will cover moving ExtendScript (`.jsx`) automation scripts to UXP's modern JavaScript APIs—including language and runtime differences, equivalent Media Encoder DOM APIs, and how to restructure a script as a UXP plugin.

## What to expect

- Language differences between ExtendScript (ES3) and UXP's modern JavaScript engine (ES2020+, async/await, modules)
- Mapping common ExtendScript object model calls to their Media Encoder DOM API equivalents
- Restructuring a standalone script into a UXP plugin (commands, panels, and the `manifest.json`)
- Handling file system, network, and UI differences between the two environments

In the meantime, see [Understanding UXP APIs](../../fundamentals/apis/index.md) for an overview of the UXP API model.
