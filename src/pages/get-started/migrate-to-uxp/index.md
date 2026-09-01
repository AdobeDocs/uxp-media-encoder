---
title: "Migrate Media Encoder Extensions to UXP"
description: "Use the UXP Migration Center to move CEP extensions and ExtendScript automation to UXP, then connect the result to Media Encoder APIs."
keywords:
  - UXP
  - Adobe Media Encoder
  - CEP
  - ExtendScript
  - migration
---

# Migrate to UXP

The architecture and API migration process is shared across UXP hosts. Use the UXP Hub Migration Center to inventory your CEP or ExtendScript dependencies, map them to supported UXP capabilities, and rebuild your extension as a UXP plugin.

<DiscoverBlock slots="link, text"/>

[Open the UXP Migration Center](https://developer-stage.adobe.com/uxp/migration-center/?aio_external)

Choose the CEP or ExtendScript path and follow the shared technical migration guidance.

<DiscoverBlock slots="link, text"/>

[Read the Guide for CEP Developers](https://developer-stage.adobe.com/uxp/migration-center/uxp-for-cep-devs/?aio_external)

Compare architectures, replace CEP dependencies, and plan an incremental move to UXP.

<DiscoverBlock slots="link, text"/>

[Read the Guide for ExtendScript Developers](https://developer-stage.adobe.com/uxp/migration-center/uxp-for-extendscript-devs/?aio_external)

Update legacy JavaScript patterns and move host automation into the UXP runtime.

## Continue with Media Encoder

After migrating the shared plugin structure, use the [Media Encoder API reference](../../media-encoder-api/index.md) to replace host calls for render queues, jobs, presets, and progress reporting.