---
title: Preset Manager Media Encoder API
description: "List export formats, find export presets by format, name, or ID, and load preset files in Adobe Media Encoder with the PresetManager API in UXP."
id: presetManager
sidebar_label: PresetManager
product: mediaencoder
keywords:
  - UXP
  - Adobe Media Encoder
  - Media Encoder API
  - PresetManager
  - export presets
  - export formats
  - getPresetsForFormat
  - findPresetByID
  - loadPresetFromFile
  - user presets


contributors:
  - https://github.com/sukriyeLudwig
---

# Preset Manager

<InlineAlert variant="info" slots="text"/>

UXP for Adobe Media Encoder is in public beta. This reference is being written, and the supported API surface may change before general availability.

Since: **27.0**

The `PresetManager` object gives access to the export presets that Media Encoder knows about: the system presets that come with Media Encoder and the custom presets that users created. Use it to list the available export formats, to find presets by format, display name, or ID, and to load a preset from an `.epr` file. Each preset is returned as a [Preset](./preset/index.md) object.

All `PresetManager` members are class members. Call them on `app.PresetManager`:

```javascript
const app = require("mediaencoder");
const formatNames = app.PresetManager.getFormatNameList(); // ["H.264", "QuickTime", ...]
const presets = app.PresetManager.getPresetsForFormat("H.264");
```

To render with a preset, pass its file path to a [RenderQueue](../render-queue/index.md) method:

```javascript
const app = require("mediaencoder");
const [preset] = app.PresetManager.findPresetsByName("My H.264 Preset");
await app.RenderQueue.renderFile("path/to/source.mov", preset.getFilePath(), "path/to/out.mp4");
```

<HorizontalLine />

## Properties

### userPresetsLocation

The file system path to the folder where Media Encoder stores user presets.

Type: _string_ (readonly, class)

Since: **27.0**

```javascript
const app = require("mediaencoder");
const userPresetsFolder = app.PresetManager.userPresetsLocation;
```

<HorizontalLine />

## Methods

### getFormatNameList

Returns the names of all available export formats.

Since: **27.0**

#### Parameters

none

#### Returns

| Name        | Type       | Description                                             |
| :---------- | :--------- | :------------------------------------------------------ |
| formatNames | _string[]_ | Export format names, such as `"H.264"` or `"QuickTime"` |

```javascript
const app = require("mediaencoder");
const formatNames = app.PresetManager.getFormatNameList();
```

<HorizontalLine />

### getPresetsForFormat

Returns all presets of an export format, first the system presets, then the custom presets. To tell them apart, call [getPresetType](./preset/index.md#getpresettype) on each preset.

Since: **27.0**

#### Parameters

| Name       | Type     | Description                                                         |
| :--------- | :------- | :------------------------------------------------------------------ |
| formatName | _string_ | The export format name, as returned by [getFormatNameList](#getformatnamelist) |

#### Returns

| Name    | Type       | Description                                                                          |
| :------ | :--------- | :----------------------------------------------------------------------------------- |
| presets | _object[]_ | Array of [Preset](./preset/index.md) objects. Empty if the format name is unknown    |

```javascript
const app = require("mediaencoder");
const customPresets = app.PresetManager.getPresetsForFormat("H.264").filter(
  (preset) => preset.getPresetType() === "custom",
);
```

<HorizontalLine />

### findPresetByID

Finds a preset by its unique ID (GUID).

Since: **27.0**

#### Parameters

| Name     | Type     | Description                                                                    |
| :------- | :------- | :----------------------------------------------------------------------------- |
| uniqueID | _string_ | The GUID of the preset, as returned by [Preset.getID](./preset/index.md#getid) |

#### Returns

[Preset](./preset/index.md), or `null` if no preset has this ID.

```javascript
const app = require("mediaencoder");
const preset = app.PresetManager.findPresetByID(presetId);
if (preset) {
  console.log(preset.getDisplayName());
}
```

<HorizontalLine />

### findPresetsByName

Finds presets by display name. The name must match exactly. Presets of different formats can have the same name, so the result can contain several presets.

Since: **27.0**

#### Parameters

| Name       | Type     | Description                     |
| :--------- | :------- | :------------------------------ |
| presetName | _string_ | The display name of the preset |

#### Returns

| Name    | Type       | Description                                                                    |
| :------ | :--------- | :----------------------------------------------------------------------------- |
| presets | _object[]_ | Array of matching [Preset](./preset/index.md) objects. Empty if none match     |

```javascript
const app = require("mediaencoder");
const presets = app.PresetManager.findPresetsByName("My H.264 Preset");
presets.forEach((preset) => console.log(preset.getFormatName(), preset.getID()));
```

<HorizontalLine />

### loadPresetFromFile

Loads a preset from a preset (`.epr`) file. If the file isn't found at the given path, the path is also tried relative to the Media Encoder application folder, where the system presets are installed.

Since: **27.0**

#### Parameters

| Name     | Type     | Description                            |
| :------- | :------- | :------------------------------------- |
| filePath | _string_ | File path to the preset (`.epr`) file |

#### Returns

[Preset](./preset/index.md), or `null` if the file doesn't exist or can't be read. [getPresetType](./preset/index.md#getpresettype) returns `"custom"` for a preset loaded from a file.

```javascript
const app = require("mediaencoder");
const preset = app.PresetManager.loadPresetFromFile("path/to/preset.epr");
if (preset) {
  console.log(preset.getDisplayName(), preset.getFormatName());
}
```

<HorizontalLine />
