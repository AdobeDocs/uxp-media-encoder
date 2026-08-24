---
title: "Render Options: Media Encoder API"
description: "Media Encoder's Render Options APIs for adding, modifying, and enquing items for render."
id: renderOptions
title: RenderOptions
sidebar_label: RenderOptions
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
  - https://github.com/sukriyeLudwig
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
const WORKAREATYPE_CUSTOM = RenderOptions.WORKAREATYPE_CUSTOM; // 3
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

## Properties

These read-only properties reflect the current state of a `RenderOptions` instance, based on the setter methods that have been called on it.

```javascript
const app = require("mediaencoder");
const renderOptions = new app.RenderOptions();
renderOptions.workAreaType; // 4
```

### customInPoint

The custom in point set via `setCustomInAndOutPoints()`, as a [TickTime](../tick-time/index.md) object.

Type: _object_ (readonly)

Since: **26.5**

<HorizontalLine />

### customOutPoint

The custom out point set via `setCustomInAndOutPoints()`, as a [TickTime](../tick-time/index.md) object.

Type: _object_ (readonly)

Since: **26.5**

<HorizontalLine />

### rotation

The rotation value (in a 360-degree system) set via `setRotation()`. Undefined if `setRotation()` has not been called.

Type: _number (optional)_ (readonly)

Since: **26.5**

<HorizontalLine />

### workAreaType

The work area type set via `setWorkAreaType()`. One of the `WORKAREATYPE_*` constants.

Type: _int_ (readonly)

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

See the [TickTime](../tick-time/index.md) reference for how to construct these values.

<HorizontalLine />

### setImportSequencesNatively

Sets the "Import Sequences Natively" flag, which allows Media Encoder to import sequences directly from a Premiere Pro project file without needing to open Premiere Pro.

Since: **26.5**

#### Parameters

| Name  | Type      | Description                                                                       |
| :---- | :-------- | :--------------------------------------------------------------------------------- |
| value | _boolean_ | `true` to import sequences natively; `false` to import via Dynamic Link           |

#### Returns

| Name          | Type     | Description                      |
| :------------ | :------- | :------------------------------- |
| renderOptions | _object_ | The updated renderOptions object |

```javascript
const app = require("mediaencoder");
const renderOptions = new app.RenderOptions();
renderOptions.setImportSequencesNatively(true);
```

<HorizontalLine />

### setIncludeSourceXMP

Sets whether source XMP metadata is included in the output. Default is `false`.

Since: **26.5**

#### Parameters

| Name             | Type      | Description                                    |
| :--------------- | :-------- | :---------------------------------------------- |
| includeSourceXMP | _boolean_ | `true` to include source XMP metadata in the output |

#### Returns

| Name          | Type     | Description                      |
| :------------ | :------- | :------------------------------- |
| renderOptions | _object_ | The updated renderOptions object |

```javascript
const app = require("mediaencoder");
const renderOptions = new app.RenderOptions();
renderOptions.setIncludeSourceXMP(true);
```

<HorizontalLine />

### setOverwriteOutputFile

Controls overwrite behavior for the output file. If set to `true`, the specified output file path will be overwritten. If set to `false`, the global overwrite preference is respected.

Since: **26.5**

#### Parameters

| Name  | Type      | Description                                                    |
| :---- | :-------- | :--------------------------------------------------------------- |
| value | _boolean_ | `true` to overwrite the output file; `false` to respect the global preference |

#### Returns

| Name          | Type     | Description                      |
| :------------ | :------- | :------------------------------- |
| renderOptions | _object_ | The updated renderOptions object |

```javascript
const app = require("mediaencoder");
const renderOptions = new app.RenderOptions();
renderOptions.setOverwriteOutputFile(true);
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

### setSequenceGUID

Sets the sequence or composition to render.

Since: **26.5**

#### Parameters

| Name | Type     | Description                                                                                                                                                    |
| :--- | :------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| guid | _string_ | The unique ID of a sequence or a composition. Use [getProjectItemGUIDs](../render-queue/index.md#getprojectitemguids) on `RenderQueue` to retrieve the GUIDs. |

#### Returns

| Name          | Type     | Description                      |
| :------------ | :------- | :------------------------------- |
| renderOptions | _object_ | The updated renderOptions object |

```javascript
const app = require("mediaencoder");
const renderOptions = new app.RenderOptions();
const res = app.RenderQueue.getProjectItemGUIDs("path/to/project.prproj");
renderOptions.setSequenceGUID(res.guids[0]);
```

<HorizontalLine />

### setWorkAreaType

Sets the designated type of work area. Use the `WORKAREATYPE_*` constants to specify the desired type of work area.

Works only with project files that contain sequences. If the input sequence has a predefined work area or in and out points, this method will set them properly. Note that the custom work area type will only function correctly if you have previously called `setCustomInAndOutPoints`.

Since: **26.5**

#### Parameters

| Name         | Type  | Description                                |
| :----------- | :---- | :------------------------------------------ |
| workAreaType | _int_ | One of the `WORKAREATYPE_*` constant values |

#### Returns

| Name          | Type     | Description                      |
| :------------ | :------- | :------------------------------- |
| renderOptions | _object_ | The updated renderOptions object |

```javascript
const app = require("mediaencoder");
const renderOptions = new app.RenderOptions();
renderOptions.setWorkAreaType(app.RenderOptions.WORKAREATYPE_ENTIRE_SEQUENCE);
```

<HorizontalLine />
