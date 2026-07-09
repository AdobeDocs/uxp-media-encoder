---
title: "Nomenclature: UXP for Adobe Media Encoder"
description: "The vocabulary used across the UXP for Media Encoder docs: plugin, panel, command, manifest, entry point, script, and how they relate to CEP and ExtendScript."
keywords:
  - UXP
  - Adobe Media Encoder
  - nomenclature
  - glossary
  - plugin
  - panel
  - manifest
  - CEP
  - ExtendScript
contributors:
  - https://github.com/karan0207
---

# Nomenclature

These docs use a small, consistent vocabulary. This page defines the core terms so the rest of the guides read clearly.

## Core terms

* **Plugin**: the unit you build and load. It bundles a manifest, your code, and assets.
* **Manifest** (`manifest.json`): declares the plugin's identity, the host it targets, and its entry points.
* **Entry point**: a declared way into your plugin, such as a panel or a command.
* **Panel**: an entry point that renders UI inside Media Encoder.
* **Command**: an entry point that runs an action without a persistent panel.
* **Script**: JavaScript that drives the host through its APIs, with or without UI.
* **Host**: the Adobe application your plugin runs in. Here, that is Media Encoder.

## Mapping from CEP and ExtendScript

If you have built extensions before, this is roughly how the old vocabulary maps to UXP:

| Legacy (CEP / ExtendScript) | UXP |
|---|---|
| CEP extension panel | UXP plugin with a panel entry point |
| ExtendScript (`.jsx`) automation | UXP script using the host APIs |
| `CSInterface` / host bridge | the host APIs you `require` directly |
| Manifest in `CSXS/manifest.xml` | `manifest.json` |

The mapping is conceptual, not line for line. For the practical migration path, see [Migrate from CEP and ExtendScript](../../plugins/migrating/index.md).
