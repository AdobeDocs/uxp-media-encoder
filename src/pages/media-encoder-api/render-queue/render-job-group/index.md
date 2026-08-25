---
title: "RenderJobGroup: Media Encoder API"
description: "Media Encoder's RenderJobGroup API for adding and enumerating multiple outputs that share the same render queue source."
id: renderJobGroup
title: RenderJobGroup
sidebar_label: RenderJobGroup
product: mediaencoder
keywords:
  - UXP
  - Adobe Media Encoder
  - Media Encoder API
  - RenderJobGroup
  - encoding queue
  - scripting automation


contributors:
  - https://github.com/justintaylor-dev
  - https://github.com/sukriyeLudwig
---

# RenderJobGroup

<InlineAlert variant="info" slots="text"/>

UXP for Adobe Media Encoder is in public beta. This reference is being written, and the supported API surface may change before general availability.

Since: **26.5**

A `RenderJobGroup` represents a single source (media file or project) in the render queue that can drive multiple outputs. Use it to add more outputs that share the same source via [addOutput](#addoutput), and to enumerate the outputs already in the group via [getOutputs](#getoutputs). Each output is returned as a [RenderJob](../render-job/index.md).

A `RenderJobGroup` is obtained via [RenderQueue.getJobGroup](../index.md#getjobgroup) or [RenderJob.getGroup](../render-job/index.md#getgroup), rather than constructed directly.

```javascript
const app = require("mediaencoder");
const result = await app.RenderQueue.enqueueFile(
  "path/to/source.mov",
  "path/to/preset.epr",
  "path/to/out.mp4",
);
const group = app.RenderQueue.getJobGroup(result.jobGroupId);
```

<HorizontalLine />

## Properties

### id

GUID of this render job group (its source). Matches [RenderJob.groupID](../render-job/index.md#groupid) for every output it contains.

Type: _string_ (readonly)

Since: **26.5**

<HorizontalLine />

## Methods

### addOutput

Adds another output to this group's shared source using the given preset and output path, and returns the new [RenderJob](../render-job/index.md). Per-output settings (work area, custom in/out points, rotation) are applied on the returned `RenderJob`.

Since: **26.5**

#### Parameters

| Name           | Type     | Description                       |
| :------------- | :------- | :--------------------------------- |
| presetFilePath | _string_ | File path to the preset (`.epr`) file |
| outputPath     | _string_ | File path to the output file       |

#### Returns

[RenderJob](../render-job/index.md), or `null` if the group is no longer in the queue or the preset could not be applied.

```javascript
const app = require("mediaencoder");
const group = app.RenderQueue.getJobGroup(jobGroupId);
const newOutput = group.addOutput("path/to/other-preset.epr", "path/to/other-output.mp4");
```

<HorizontalLine />

### getOutputs

Returns the [RenderJob](../render-job/index.md) outputs currently contained in this group.

Since: **26.5**

#### Parameters

none

#### Returns

| Name    | Type       | Description                                                    |
| :------ | :--------- | :--------------------------------------------------------------- |
| outputs | _object[]_ | Array of [RenderJob](../render-job/index.md) objects in this group |

```javascript
const app = require("mediaencoder");
const group = app.RenderQueue.getJobGroup(jobGroupId);
const outputs = group.getOutputs();
```

<HorizontalLine />

### getOutputCount

Returns the number of outputs currently contained in this group.

Since: **26.5**

#### Parameters

none

#### Returns

| Name  | Type     | Description                              |
| :---- | :------- | :------------------------------------------ |
| count | _number_ | The number of outputs currently in this group |

```javascript
const app = require("mediaencoder");
const group = app.RenderQueue.getJobGroup(jobGroupId);
group.getOutputCount();
```

<HorizontalLine />

### getID

Returns the GUID of this render job group (its source). Equivalent to the [id](#id) property.

Since: **26.5**

#### Parameters

none

#### Returns

| Name | Type     | Description                      |
| :--- | :------- | :----------------------------------- |
| id   | _string_ | GUID of this render job group        |

```javascript
const app = require("mediaencoder");
const group = app.RenderQueue.getJobGroup(jobGroupId);
group.getID();
```

<HorizontalLine />
