---
title: "Set Up Adobe Media Encoder for UXP Development"
description: Enable Developer Mode in Adobe Media Encoder and prepare the host to load plugins from the UXP Developer Tool.
keywords:
  - UXP
  - Adobe Media Encoder
  - Code Editor
  - UDT
  - UXP Developer Tool
  - hot reload
  - debugging
complexity: beginner
reading_time: 3 min
contributors:
  - https://github.com/karan0207
---

# Set Up Media Encoder for Development

This page covers the setup that is specific to Media Encoder. For installing a code editor and the UXP Developer Tool (UDT), enabling UDT's Developer Mode, and learning the shared workflow, see [Set Up Developer Tools](https://developer-stage.adobe.com/uxp/guides/how-to/developer-tools/?aio_external) in the UXP Hub.

If you already build UXP plugins for another Adobe application, keep your existing tools and complete only the Media Encoder steps below.

## Check Your Versions

| Component | Minimum version |
| --- | --- |
| Adobe Media Encoder | 26.5 |
| UXP Developer Tool | 2.2.1.18 |

You can use either the stable or beta Media Encoder release when it meets the minimum version required by your plugin's manifest.

## Enable Media Encoder Developer Mode

Media Encoder has a Developer Mode setting that is separate from the setting in UDT. Both must be enabled before UDT can load a development plugin into the host.

1. Open Media Encoder.
2. Go to **Edit > Preferences > Plugins**.
3. Enable **Developer mode**.
4. Restart Media Encoder.

<InlineAlert variant="warning" slots="text"/>

Restart Media Encoder after changing Developer Mode. UDT cannot load a development plugin until the host restarts with the setting enabled.

## Confirm the Host Is Available

1. Start Media Encoder and wait for it to finish opening.
2. Open UDT.
3. Create or add a plugin that targets Adobe Media Encoder.
4. Confirm that UDT offers **Load** for the plugin while Media Encoder is running.

If Media Encoder is unavailable in UDT, confirm the installed versions, Developer Mode settings, and host restart before continuing.

## Next Step

With Media Encoder ready, [build your first plugin](../build-your-first-plugin/index.md) and load it into the host.
