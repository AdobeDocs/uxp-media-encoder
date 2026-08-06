---
title: "Watch Folder: Media Encoder API"
description: "Media Encoder's Watch Folder APIs for adding, modifying, and enquing items for render."
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

# Watch Folder

<InlineAlert variant="info" slots="text"/>

UXP for Adobe Media Encoder is in public beta. This reference is being written, and the supported API surface may change before general availability.

Since: **26.5**

The Media Encoder Watch Folder API is the used for all operations involving managing Watch Folders in Media Encoder.

The Watch Folder object can be acceessed from the main app object:

<InlineAlert variant="info" slots="text"/>

🛑🛑🛑 The below needs to be verified, does not currently function 👇

```javascript
const app = require("mediaencoder");
const WatchFolder = app.WatchFolder;
```

<HorizontalLine />

## Constants

These Watch Folder Constants are used as parameters in various `WatchFolder` API methods for Media Encoder.

All Constants can be accessed via the `WatchFolder` object:

```javascript
const app = require("mediaencoder");
const WatchFolder = app.WatchFolder;
const WATCH_FOLDER_ENCODER_STATUS_CHANGED =
  renderQueue.WATCH_FOLDER_ENCODER_STATUS_CHANGED; // "AMEProgressCategoryRender"
```

### WATCH_FOLDER_ENCODER_STATUS_CHANGED

Event ID for when a watch folder encoder status changes.

Type: _string_

Since: **26.5**

<HorizontalLine />
