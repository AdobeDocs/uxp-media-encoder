---
title: "RenderJob: Media Encoder API"
description: "Media Encoder's RenderJob API for inspecting and managing an individual job in the render queue."
id: renderJob
title: RenderJob
sidebar_label: RenderJob
product: mediaencoder
keywords:
  - UXP
  - Adobe Media Encoder
  - Media Encoder API
  - RenderJob
  - encoding queue
  - scripting automation


contributors:
  - https://github.com/justintaylor-dev
  - https://github.com/sukriyeLudwig
---

# RenderJob

<InlineAlert variant="info" slots="text"/>

UXP for Adobe Media Encoder is in public beta. This reference is being written, and the supported API surface may change before general availability.

Since: **26.5**

A `RenderJob` represents a single job in the render queue. It is obtained via [RenderQueue.getJob](../index.md#getjob), rather than constructed directly.

```javascript
const app = require("mediaencoder");
const result = await app.RenderQueue.enqueueFile(
  "path/to/source.mov",
  "path/to/preset.epr",
  "path/to/out.mp4",
);
const job = app.RenderQueue.getJob(result.jobId);
```

<HorizontalLine />

## Constants

These Constants are used to interpret [getStatus](#getstatus) and as parameters to [setWorkAreaType](#setworkareatype). All Constants are class properties, accessed via the `RenderJob` object:

```javascript
const app = require("mediaencoder");
const job = app.RenderQueue.getJob(jobId);
job.getStatus() === app.RenderQueue.getJob(jobId).STATUS_ENCODING;
```

### WORKAREATYPE_CUSTOM

Work area type value for custom in / out points.

Type: _int_

Since: **26.5**

<HorizontalLine />

### WORKAREATYPE_DEFAULT

Work area type value for the default in / out points from the sequence.

Type: _int_

Since: **26.5**

<HorizontalLine />

### WORKAREATYPE_ENTIRE_SEQUENCE

Work area type value for the entire duration of the sequence.

Type: _int_

Since: **26.5**

<HorizontalLine />

### WORKAREATYPE_IN_TO_OUT_POINTS

Work area type value for the set in / out points of the sequence.

Type: _int_

Since: **26.5**

<HorizontalLine />

### WORKAREATYPE_WORKAREA

Work area type value for the entire workarea of the sequence.

Type: _int_

Since: **26.5**

<HorizontalLine />

### STATUS_WAITING

Job is waiting to be processed.

Type: _int_

Since: **26.5**

<HorizontalLine />

### STATUS_ENCODING

Job is currently encoding.

Type: _int_

Since: **26.5**

<HorizontalLine />

### STATUS_DONE

Job finished successfully.

Type: _int_

Since: **26.5**

<HorizontalLine />

### STATUS_DONE_WARNING

Job finished with warnings.

Type: _int_

Since: **26.5**

<HorizontalLine />

### STATUS_FAILED

Job failed.

Type: _int_

Since: **26.5**

<HorizontalLine />

### STATUS_PAUSED

Job is paused.

Type: _int_

Since: **26.5**

<HorizontalLine />

### STATUS_STOPPED

Job was stopped.

Type: _int_

Since: **26.5**

<HorizontalLine />

### STATUS_SKIPPED

Job was skipped.

Type: _int_

Since: **26.5**

<HorizontalLine />

### STATUS_INVALID

The job handle is no longer valid, for example if the job was removed from the queue. Returned by [getStatus](#getstatus) instead of throwing.

Type: _int_

Since: **26.5**

<HorizontalLine />

## Properties

These read-only properties are available on any `RenderJob` instance.

```javascript
const app = require("mediaencoder");
const job = app.RenderQueue.getJob(jobId);
job.batchItemID; // "1b814929-65b6-4d83-b822-68ce5cd2f741"
```

### batchItemID

GUID of the job.

Type: _string_ (readonly)

Since: **26.5**

<HorizontalLine />

### groupID

GUID of the containing job group.

Type: _string_ (readonly)

Since: **26.5**

<HorizontalLine />

### encodingTime

Elapsed encoding time, in seconds.

Type: _number_ (readonly)

Since: **26.5**

<HorizontalLine />

## Methods

### setCustomInAndOutPoints

Sets custom in and out points in the sequence. Note that the `WORKAREATYPE_CUSTOM` work area type will be set implicitly here.

Since: **26.5**

#### Parameters

| Name                  | Type     | Description                            |
| :-------------------- | :------- | :------------------------------------- |
| startPositionTickTime | _object_ | [TickTime](../../tick-time/index.md) object for the start position |
| endPositionTickTime   | _object_ | [TickTime](../../tick-time/index.md) object for the end position   |

#### Returns

| Name | Type     | Description                 |
| :--- | :------- | :----------------------------- |
| job  | _object_ | The updated `RenderJob` object |

```javascript
const app = require("mediaencoder");
const job = app.RenderQueue.getJob(jobId);
const startTime = app.TickTime.createWithSeconds(0);
const endTime = app.TickTime.createWithSeconds(1);
job.setCustomInAndOutPoints(startTime, endTime);
```

<HorizontalLine />

### setRotation

Sets the rotation of the job (in a 360-degree system).

Since: **26.5**

#### Parameters

| Name          | Type  | Description                              |
| :------------ | :---- | :--------------------------------------- |
| rotationValue | _int_ | The rotation value between 0-360 degrees |

#### Returns

| Name | Type     | Description                 |
| :--- | :------- | :----------------------------- |
| job  | _object_ | The updated `RenderJob` object |

```javascript
const app = require("mediaencoder");
const job = app.RenderQueue.getJob(jobId);
job.setRotation(45); // Rotate 45 degrees
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

| Name | Type     | Description                 |
| :--- | :------- | :----------------------------- |
| job  | _object_ | The updated `RenderJob` object |

```javascript
const app = require("mediaencoder");
const job = app.RenderQueue.getJob(jobId);
job.setWorkAreaType(job.WORKAREATYPE_ENTIRE_SEQUENCE);
```

<HorizontalLine />

### getStatus

Gets the current status of the job.

Since: **26.5**

#### Parameters

none

#### Returns

| Name   | Type  | Description                              |
| :----- | :---- | :---------------------------------------- |
| status | _int_ | One of the `STATUS_*` constants          |

```javascript
const app = require("mediaencoder");
const job = app.RenderQueue.getJob(jobId);
job.getStatus();
```

<HorizontalLine />

### isInFinalState

Checks whether the job has reached a terminal state (done, failed, or stopped).

Since: **26.5**

#### Parameters

none

#### Returns

| Name   | Type      | Description                                    |
| :----- | :-------- | :---------------------------------------------- |
| result | _boolean_ | `true` if the job has reached a terminal state |

```javascript
const app = require("mediaencoder");
const job = app.RenderQueue.getJob(jobId);
job.isInFinalState();
```

<HorizontalLine />

### getEncodeProgress

Gets the encoding progress as a percentage.

Since: **26.5**

#### Parameters

none

#### Returns

| Name     | Type     | Description                       |
| :------- | :------- | :--------------------------------- |
| progress | _number_ | Encoding progress, from 0 to 100  |

```javascript
const app = require("mediaencoder");
const job = app.RenderQueue.getJob(jobId);
job.getEncodeProgress();
```

<HorizontalLine />

### getEncodeProgressMessage

Gets a human-readable progress message for the job.

Since: **26.5**

#### Parameters

none

#### Returns

| Name    | Type     | Description                                            |
| :------ | :------- | :------------------------------------------------------- |
| message | _string_ | A progress message, such as `"Analyzing audio..."`      |

```javascript
const app = require("mediaencoder");
const job = app.RenderQueue.getJob(jobId);
job.getEncodeProgressMessage();
```

<HorizontalLine />

### getErrorText

Gets a single-line error string for the job, if it failed.

Since: **26.5**

#### Parameters

none

#### Returns

| Name  | Type     | Description                                                          |
| :---- | :------- | :---------------------------------------------------------------------- |
| error | _string_ | A single-line error string. For the full log, use [getLogOutput](#getlogoutput) |

```javascript
const app = require("mediaencoder");
const job = app.RenderQueue.getJob(jobId);
job.getErrorText();
```

<HorizontalLine />

### getLogOutput

Get the log output of the job.

Since: **26.5**

#### Parameters

none

#### Returns

| Name      | Type     | Description                                                                     |
| :-------- | :------- | :------------------------------------------------------------------------------ |
| logOutput | _string_ | Returns the log output including possible warnings and errors as a JSON string. |

```javascript
const app = require("mediaencoder");
const job = app.RenderQueue.getJob(jobId);
job.getLogOutput();
```

<HorizontalLine />

### getOutputFilePath

Gets the output file path for the job.

Since: **26.5**

#### Parameters

none

#### Returns

| Name       | Type     | Description                    |
| :--------- | :------- | :------------------------------- |
| outputPath | _string_ | File path to the output file    |

```javascript
const app = require("mediaencoder");
const job = app.RenderQueue.getJob(jobId);
job.getOutputFilePath();
```

<HorizontalLine />

### getOutputFilesAfterExport

Gets the list of files written by the encoder after export completes.

Since: **26.5**

#### Parameters

none

#### Returns

| Name  | Type       | Description                                    |
| :---- | :--------- | :------------------------------------------------ |
| files | _string[]_ | Array of file paths written after export completes |

```javascript
const app = require("mediaencoder");
const job = app.RenderQueue.getJob(jobId);
job.getOutputFilesAfterExport();
```

<HorizontalLine />

### getPresetName

Gets the name of the preset applied to this job.

Since: **26.5**

#### Parameters

none

#### Returns

| Name       | Type     | Description                    |
| :--------- | :------- | :------------------------------- |
| presetName | _string_ | Name of the applied preset      |

```javascript
const app = require("mediaencoder");
const job = app.RenderQueue.getJob(jobId);
job.getPresetName();
```

<HorizontalLine />

### getVideoSummary

Gets a video format summary string for the job.

Since: **26.5**

#### Parameters

none

#### Returns

| Name    | Type     | Description                                     |
| :------ | :------- | :------------------------------------------------- |
| summary | _string_ | Video format summary, such as `"H.264 1920x1080"` |

```javascript
const app = require("mediaencoder");
const job = app.RenderQueue.getJob(jobId);
job.getVideoSummary();
```

<HorizontalLine />

### getAudioSummary

Gets an audio format summary string for the job.

Since: **26.5**

#### Parameters

none

#### Returns

| Name    | Type     | Description                                  |
| :------ | :------- | :---------------------------------------------- |
| summary | _string_ | Audio format summary, such as `"AAC, 320 kbps"` |

```javascript
const app = require("mediaencoder");
const job = app.RenderQueue.getJob(jobId);
job.getAudioSummary();
```

<HorizontalLine />

### getBitrateSummary

Gets a bitrate summary string for the job.

Since: **26.5**

#### Parameters

none

#### Returns

| Name    | Type     | Description             |
| :------ | :------- | :-------------------------- |
| summary | _string_ | Bitrate summary string      |

```javascript
const app = require("mediaencoder");
const job = app.RenderQueue.getJob(jobId);
job.getBitrateSummary();
```

<HorizontalLine />

### moveToTop

Moves this job's containing group to the top of the render queue so it encodes next, raising its priority.

Since: **26.5**

#### Parameters

none

#### Returns

| Name   | Type      | Description                                                                                                       |
| :----- | :-------- | :------------------------------------------------------------------------------------------------------------------ |
| result | _boolean_ | `true` on success (or if the job is already at the top); `false` if the job handle is no longer valid, or the job has no group |

```javascript
const app = require("mediaencoder");
const job = app.RenderQueue.getJob(jobId);
job.moveToTop();
```

<HorizontalLine />

### getGroup

Returns the [RenderJobGroup](../render-job-group/index.md) that contains this job (its shared source). Use it to add more outputs to the same source via [RenderJobGroup.addOutput](../render-job-group/index.md#addoutput).

Since: **26.5**

#### Parameters

none

#### Returns

[RenderJobGroup](../render-job-group/index.md), or `null` if the job handle is no longer valid or it has no group.

```javascript
const app = require("mediaencoder");
const job = app.RenderQueue.getJob(jobId);
const group = job.getGroup();
```

<HorizontalLine />
