---
title: "Render Options: Media Encoder API"
description: "Media Encoder's Render Options APIs for adding, modifying, and enquing items for render."
id: renderQueue
title: RenderQueue
sidebar_label: RenderQueue
product: mediaencoder
keywords:
  - UXP
  - Adobe Media Encoder
  - Media Encoder API
  - encoding queue
  - presets
  - jobs
  - scripting automation


contributors:
  - https://github.com/justintaylor-dev
---

# Render Options

The Media Encoder Render Options API is the used for all operations involving managing encoding properties in the app.

<InlineAlert variant="info" slots="text"/>

UXP for Adobe Media Encoder is in public beta. This reference is being written, and the supported API surface may change before general availability.

## Constants

These Render Options Constants are used as parameters in various `RenderQueue` and `RenderOptions` API methods for Media Encoder.

All Constants can be accessed via the `RenderOptions` object:

```javascript
const app = require("mediaencoder");
const RenderOptions = app.RenderOptions;
const WORKAREATYPE_CUSTOM = renderQueue.WORKAREATYPE_CUSTOM; // 3
```

### WORKAREATYPE_CUSTOM

Work area type value for custom in / out points

Type: _int_

Since: **26.5**

<HorizontalLine />

### WORKAREATYPE_DEFAULT

Work area type value for the default in / out points from the sequence

Type: _int_

Since: **26.5**

<HorizontalLine />

### WORKAREATYPE_ENTIRE_SEQUENCE

Work area type value for the entire duration of the sequence

Type: _int_

Since: **26.5**

<HorizontalLine />

### WORKAREATYPE_IN_TO_OUT_POINTS

Work area type value for the set in / out points of the sequence

Type: _int_

Since: **26.5**

<HorizontalLine />

### WORKAREATYPE_WORKAREA

Work area type value for the entire workarea of the sequence

Type: _int_

Since: **26.5**

<HorizontalLine />

## Methods
