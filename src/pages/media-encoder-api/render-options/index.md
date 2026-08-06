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

A Render Options instance can be created from the main app object:

```javascript
const app = require("mediaencoder");
const renderOptions = new app.RenderOptions();
```

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

### setCustomInAndOutPoints

Sets custom in and out points in the sequence. Note that the `WORKAREATYPE_CUSTOM` work area type will be set implicitly here.

Since: **26.5**

#### Parameters

| Name                  | Type     | Description                            |
| :-------------------- | :------- | :------------------------------------- |
| startPositionTickTime | _object_ | TickTime object for the start position |
| endPositionTickTime   | _object_ | TickTime object for the end position   |

#### Returns

| Name          | Type     | Description                      |
| :------------ | :------- | :------------------------------- |
| renderOptions | _object_ | The updated renderOptions object |

```javascript
const app = require("mediaencoder");
const renderOptions = new app.RenderOptions();
const startTime = app.TickTime.createWithSeconds(0);
const endTime = app.TickTime.createWithSeconds(1);
renderOptions.setCustomInAndOutPoints(startTime, endTime);
```

<HorizontalLine />

### setRotation

Sets the rotation of the render options instance (in a 360-degree system).

Since: **26.5**

#### Parameters

| Name          | Type  | Description                              |
| :------------ | :---- | :--------------------------------------- |
| rotationValue | _int_ | The rotation value between 0-360 degrees |

#### Returns

| Name          | Type     | Description                      |
| :------------ | :------- | :------------------------------- |
| renderOptions | _object_ | The updated renderOptions object |

```javascript
const app = require("mediaencoder");
const renderOptions = new app.RenderOptions();
renderOptions.setRotation(45); // Rotate 45 degrees
```

<HorizontalLine />
