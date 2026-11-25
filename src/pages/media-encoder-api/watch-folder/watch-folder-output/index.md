---
title: WatchFolderOutput Media Encoder API
description: "Read the ID, preset, and destination folder of a single Media Encoder watch folder output with the WatchFolderOutput API in UXP."
id: watchFolderOutput
sidebar_label: WatchFolderOutput
product: mediaencoder
keywords:
  - UXP
  - Adobe Media Encoder
  - Media Encoder API
  - WatchFolderOutput
  - watch folder output
  - watch folder
  - automatic encoding
  - addOutput
  - getOutputs
  - removeOutput


contributors:
  - https://github.com/sukriyeLudwig
---

# WatchFolderOutput

<InlineAlert variant="info" slots="text"/>

UXP for Adobe Media Encoder is in public beta. This reference is being written, and the supported API surface may change before general availability.

Since: **27.0**

A `WatchFolderOutput` represents a single output of a [watch folder](../index.md), with its own preset and destination folder. A watch folder encodes every new file once for each of its outputs.

A `WatchFolderOutput` is returned by [addOutput](../index.md#addoutput) and [getOutputs](../index.md#getoutputs) on a watch folder object, rather than constructed directly. To remove an output, pass its [id](#id) to [removeOutput](../index.md#removeoutput).

```javascript
const app = require("mediaencoder");
const watchFolder = await app.WatchFolder.createWatchFolder(
  "path/to/source",
  "path/to/destination",
  "path/to/preset.epr",
);
const output = await watchFolder.addOutput("path/to/other-preset.epr", "path/to/other-destination");
output.id; // "3f2b6c1e-9d4a-4c8e-a1f7-5b2d8e6c0a94"
```

<HorizontalLine />

## Properties

### id

The unique identifier for the output. Pass it to [removeOutput](../index.md#removeoutput) to remove the output from its watch folder.

Type: _string_ (readonly)

Since: **27.0**

<HorizontalLine />

### presetPath

The preset used for encoding this output.

Type: _string_ (readonly)

Since: **27.0**

<HorizontalLine />

### destinationPath

The destination path where this output's encoded files are saved.

Type: _string_ (readonly)

Since: **27.0**

<HorizontalLine />
