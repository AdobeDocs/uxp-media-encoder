---
title: Preset Media Encoder API
description: "Read the name, ID, format, file path, type, comments, and settings summary of a Media Encoder export preset with the Preset API in UXP."
id: preset
sidebar_label: Preset
product: mediaencoder
keywords:
  - UXP
  - Adobe Media Encoder
  - Media Encoder API
  - Preset
  - export preset
  - preset settings
  - getFilePath
  - getSummaryJSON
  - system presets
  - custom presets


contributors:
  - https://github.com/sukriyeLudwig
---

# Preset

<InlineAlert variant="info" slots="text"/>

UXP for Adobe Media Encoder is in public beta. This reference is being written, and the supported API surface may change before general availability.

Since: **27.0**

A `Preset` represents an export preset: a named set of encoding settings for an export format. Use it to read the identity, format, and settings of a preset, and to get the file path that the [RenderQueue](../../render-queue/index.md) methods expect as `presetFilePath`.

A `Preset` is returned by the [PresetManager](../index.md) methods, rather than constructed directly. All `Preset` members are instance methods.

```javascript
const app = require("mediaencoder");
const [preset] = app.PresetManager.getPresetsForFormat("H.264");
preset.getDisplayName();
await app.RenderQueue.renderFile("path/to/source.mov", preset.getFilePath(), "path/to/out.mp4");
```

<HorizontalLine />

## Methods

### getDisplayName

Returns the display name of the preset, localized to the language of the Media Encoder user interface.

Since: **27.0**

#### Parameters

none

#### Returns

| Name        | Type     | Description                    |
| :---------- | :------- | :----------------------------- |
| displayName | _string_ | The display name of the preset |

```javascript
const app = require("mediaencoder");
const [preset] = app.PresetManager.getPresetsForFormat("H.264");
preset.getDisplayName();
```

<HorizontalLine />

### getMatchName

Returns the match name of the preset, which identifies the preset in code.

Since: **27.0**

#### Parameters

none

#### Returns

| Name      | Type     | Description                  |
| :-------- | :------- | :--------------------------- |
| matchName | _string_ | The match name of the preset |

```javascript
const app = require("mediaencoder");
const [preset] = app.PresetManager.getPresetsForFormat("H.264");
preset.getMatchName();
```

<HorizontalLine />

### getID

Returns the unique ID (GUID) of the preset. Pass it to [PresetManager.findPresetByID](../index.md#findpresetbyid) to find the preset again later.

Since: **27.0**

#### Parameters

none

#### Returns

| Name | Type     | Description                |
| :--- | :------- | :------------------------- |
| id   | _string_ | The GUID of the preset     |

```javascript
const app = require("mediaencoder");
const [preset] = app.PresetManager.getPresetsForFormat("H.264");
const presetId = preset.getID();
app.PresetManager.findPresetByID(presetId);
```

<HorizontalLine />

### getFolderDisplayPath

Returns the folder path under which the preset is organized in the Media Encoder user interface.

Since: **27.0**

#### Parameters

none

#### Returns

| Name              | Type     | Description                                    |
| :---------------- | :------- | :--------------------------------------------- |
| folderDisplayPath | _string_ | The folder path of the preset in the preset browser |

```javascript
const app = require("mediaencoder");
const [preset] = app.PresetManager.getPresetsForFormat("H.264");
preset.getFolderDisplayPath();
```

<HorizontalLine />

### getFilePath

Returns the full path to the preset file on disk. Pass it as `presetFilePath` to [RenderQueue.renderFile](../../render-queue/index.md#renderfile), [RenderQueue.enqueueFile](../../render-queue/index.md#enqueuefile), or the other render methods.

Since: **27.0**

#### Parameters

none

#### Returns

| Name     | Type     | Description                       |
| :------- | :------- | :-------------------------------- |
| filePath | _string_ | The full path to the preset file  |

```javascript
const app = require("mediaencoder");
const [preset] = app.PresetManager.getPresetsForFormat("H.264");
await app.RenderQueue.enqueueFile("path/to/source.mov", preset.getFilePath(), "path/to/out.mp4");
```

<HorizontalLine />

### getFormatName

Returns the name of the export format of the preset.

Since: **27.0**

#### Parameters

none

#### Returns

| Name       | Type     | Description                                                |
| :--------- | :------- | :--------------------------------------------------------- |
| formatName | _string_ | The export format name, such as `"H.264"` or `"QuickTime"` |

```javascript
const app = require("mediaencoder");
const preset = app.PresetManager.loadPresetFromFile("path/to/preset.epr");
preset.getFormatName(); // "H.264"
```

<HorizontalLine />

### getPresetType

Returns where the preset comes from: `"system"` for a preset that comes with Media Encoder, or `"custom"` for a preset that a user created. Presets loaded with [PresetManager.loadPresetFromFile](../index.md#loadpresetfromfile) are `"custom"`.

Since: **27.0**

#### Parameters

none

#### Returns

| Name       | Type     | Description                     |
| :--------- | :------- | :------------------------------ |
| presetType | _string_ | `"system"` or `"custom"`        |

```javascript
const app = require("mediaencoder");
const systemPresets = app.PresetManager.getPresetsForFormat("H.264").filter(
  (preset) => preset.getPresetType() === "system",
);
```

<HorizontalLine />

### isIngestPreset

Returns whether the preset is an ingest preset. Ingest presets can't be used for watch folder outputs, see [WatchFolder.addOutput](../../watch-folder/index.md#addoutput).

Since: **27.0**

#### Parameters

none

#### Returns

| Name     | Type      | Description                                  |
| :------- | :-------- | :------------------------------------------- |
| isIngest | _boolean_ | `true` if the preset is an ingest preset     |

```javascript
const app = require("mediaencoder");
const preset = app.PresetManager.loadPresetFromFile("path/to/preset.epr");
preset.isIngestPreset(); // false
```

<HorizontalLine />

### getComments

Returns the comments of the preset, localized to the language of the Media Encoder user interface.

Since: **27.0**

#### Parameters

none

#### Returns

| Name     | Type     | Description                 |
| :------- | :------- | :-------------------------- |
| comments | _string_ | The comments of the preset  |

```javascript
const app = require("mediaencoder");
const preset = app.PresetManager.loadPresetFromFile("path/to/preset.epr");
preset.getComments();
```

<HorizontalLine />

### getSummaryJSON

Returns a summary of all settings of the preset, including the video, audio, and encoding parameters, as a JSON string.

Since: **27.0**

#### Parameters

none

#### Returns

| Name    | Type     | Description                                   |
| :------ | :------- | :-------------------------------------------- |
| summary | _string_ | JSON string with the settings of the preset   |

```javascript
const app = require("mediaencoder");
const preset = app.PresetManager.loadPresetFromFile("path/to/preset.epr");
const summary = JSON.parse(preset.getSummaryJSON());
```

<HorizontalLine />
