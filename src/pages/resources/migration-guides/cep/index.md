---
title: CEP Migration Guide
description: Move a Common Extensibility Platform (CEP) panel to a UXP plugin
keywords:
  - migration
  - CEP
  - CSInterface
  - UXP
contributors:
  - https://github.com/kasivn
---

# CEP Migration Guide

<InlineAlert variant="info" slots="heading, text" />

Content pending

This guide is a placeholder. It will cover moving a Common Extensibility Platform (CEP) extension to a UXP plugin—mapping `CSInterface` calls to their UXP equivalents, converting the manifest, and adjusting the packaging and signing workflow.

## What to expect

- Key architectural differences between CEP and UXP (no more Chromium Embedded Framework bridge; UXP plugins run natively alongside the host application)
- Mapping common `CSInterface` calls to UXP Core and Media Encoder DOM APIs
- Converting a CEP `manifest.xml` to a UXP `manifest.json`
- Packaging and distributing your migrated plugin

In the meantime, see [Understanding UXP APIs](../../fundamentals/apis/index.md) for an overview of how UXP's unified JavaScript engine replaces the CEP bridge model.
