---
title: Render Queue Media Encoder API
description: "Media Encoder's Render Queue APIs for adding, modifying, and enquing items for render."
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
  - renderProjectItem
  - getProjectItems


contributors:
  - https://github.com/justintaylor-dev
  - https://github.com/sukriyeLudwig
---

# Render Queue

<InlineAlert variant="info" slots="text"/>

UXP for Adobe Media Encoder is in public beta. This reference is being written, and the supported API surface may change before general availability.

Since: **27.0**

The Media Encoder Render Queue API is the used for all operations involving managing the app and render queue.

The RenderQueue object can be acceessed from the main app object:

```javascript
const app = require("mediaencoder");
const renderQueue = app.RenderQueue;
```

<HorizontalLine />

## Constants

These Render Queue Constants are used as parameters in various `RenderQueue` API methods for Media Encoder.

All Constants can be accessed via the `RenderQueue` object:

```javascript
const app = require("mediaencoder");
const renderQueue = app.RenderQueue;
const PROGRESS_CATEGORY_ID = renderQueue.PROGRESS_CATEGORY_ID; // "AMEProgressCategoryRender"
const RENDER_QUEUE_RUNNING = renderQueue.RENDER_QUEUE_RUNNING; // 2
```

### PROGRESS_CATEGORY_ID

Retrieves the unique identifier for the progress category for global progress of the AME renderer. This ID allows access to the global progress of the AME Renderer. To obtain the category, use [getOrCreateProgressCategory()](../progress-category-container/index.md#getorcreateprogresscategory) on the [ProgressCategoryContainer](../progress-category-container/index.md) object. The [ProgressItem](../progress-category-container/progress-item/index.md) object should be used to manage individual progress items. Each job item is registered using its unique reference ID.

Type: _string_

Since: **27.0**

<HorizontalLine />

### RENDER_QUEUE_INVALID_STATE

Render queue invalid state.

Type: _int_

Since: **27.0**

<HorizontalLine />

### RENDER_QUEUE_PAUSED

Render queue paused state.

Type: _int_

Since: **27.0**

<HorizontalLine />

### RENDER_QUEUE_RUNNING

Render queue running state.

Type: _int_

Since: **27.0**

<HorizontalLine />

### RENDER_QUEUE_STOPPED

Render queue stopped state.

Type: _int_

Since: **27.0**

<HorizontalLine />

### RENDER_QUEUE_STOPPING

Render queue stopping state.

Type: _int_

Since: **27.0**

<HorizontalLine />

### RESULT_ERROR

Validation result when your render job returns an error.

Type: _int_

Since: **27.0**

<HorizontalLine />

### RESULT_SUCCESS

Validation result when your render job returns successfully.

Type: _int_

Since: **27.0**

<HorizontalLine />

### RENDER_QUEUE_STATUS_CHANGED

Event ID for when the render queue status changes.

The listener receives a `RenderQueueEvent` object with the following property:

| Name   | Type  | Description                                                                                                   |
| :----- | :---- | :------------------------------------------------------------------------------------------------------------ |
| status | _int_ | The new status of the render queue, one of the `RENDER_QUEUE_*` constants, such as [RENDER_QUEUE_RUNNING](#render_queue_running) |

Type: _string_

Since: **27.0**

<HorizontalLine />

### AUDIO_PREPROGRESS_VALUE_CHANGED

Event ID for when the audio preprogress value changes.

The listener receives a `RenderQueueAudioPreProgressValueChangedEvent` object with the following properties:

| Name           | Type     | Description                                 |
| :------------- | :------- | :------------------------------------------ |
| jobId          | _string_ | The ID of the job                           |
| inProgressText | _string_ | The progress text to display                |
| value          | _number_ | The progress, from `0.0` to `1.0`           |

Type: _string_

Since: **27.0**

<HorizontalLine />

### NEXT_JOB_ENCODING_EVENT

Event ID fired when the next job in the render queue is about to start encoding. Subscribe to it on the [render queue instance](./render-queue-instance/index.md#subscribetoevent).

The listener receives a `RenderNextJobEvent` object with the following property:

| Name  | Type     | Description                                                   |
| :---- | :------- | :------------------------------------------------------------ |
| jobId | _string_ | The ID of the job, use it with [getJob](#getjob)              |

Type: _string_

Since: **27.0**

```javascript
const app = require("mediaencoder");
const instance = app.RenderQueue.getInstance();
const event = app.RenderQueue.NEXT_JOB_ENCODING_EVENT;
instance.subscribeToEvent(event);
instance.addEventListener(event, (nextJobEvent) => {
  const job = app.RenderQueue.getJob(nextJobEvent.jobId);
  console.log("Encoding started:", job.getOutputFilePath());
});
```

<HorizontalLine />

### MEDIA_ITEM_CREATED_EVENT

Event ID fired when Media Encoder has created the source media of a job, as part of preparing the job for encoding. Subscribe to it on the [render queue instance](./render-queue-instance/index.md#subscribetoevent).

The listener receives a `RenderMediaInfoCreatedEvent` object with the following property:

| Name  | Type     | Description                                      |
| :---- | :------- | :----------------------------------------------- |
| jobId | _string_ | The ID of the job, use it with [getJob](#getjob) |

Type: _string_

Since: **27.0**

<HorizontalLine />

### ENCODE_COMPLETE_EVENT

Event ID fired when a job has finished encoding. Subscribe to it on the [render queue instance](./render-queue-instance/index.md#subscribetoevent).

The listener receives a `RenderQueueEncodeCompleteEvent` object with the following properties:

| Name           | Type      | Description                                                         |
| :------------- | :-------- | :------------------------------------------------------------------ |
| jobId          | _string_  | The ID of the job, use it with [getJob](#getjob)                    |
| isOkToMoveFile | _boolean_ | `true` if the source file of the job can now be moved or deleted    |

Type: _string_

Since: **27.0**

```javascript
const app = require("mediaencoder");
const instance = app.RenderQueue.getInstance();
const event = app.RenderQueue.ENCODE_COMPLETE_EVENT;
instance.subscribeToEvent(event);
instance.addEventListener(event, (encodeCompleteEvent) => {
  const job = app.RenderQueue.getJob(encodeCompleteEvent.jobId);
  console.log("Finished:", job.getOutputFilePath());
});
```

<HorizontalLine />

## Methods

### enqueueFile

Enqueues a media source with a given RenderOptions object but does NOT start the queue to render. Renders a media source using a specified preset.

This method currently supports transcoding for various file types, including media files, Adobe Premiere project files, and Adobe After Effects project files.

For Premiere & After Effects projects, the first sequence or comp will be added to the queue. In order to specify a different sequence or comp for rendering, use [enqueueProjectItem](#enqueueprojectitem).

Since: **27.0**

#### Parameters

| Name           | Type     | Description                   |
| :------------- | :------- | :---------------------------- |
| filePath       | _string_ | File path to the media source |
| presetFilePath | _string_ | File path to the preset file  |
| outputPath     | _string_ | File path to the output file  |
| renderOptions  | [RenderOptions](../render-options/index.md) (optional) | Render settings to apply to the job before the queue starts |

#### Returns

| Name       | Type     | Description                          |
| :--------- | :------- | :----------------------------------- |
| jobGroupId | _string_ | The job group ID for the current job |
| jobId      | _string_ | The job ID for the current job       |
| message    | _string_ | Result message of enqueue action     |
| outputPath | _string_ | File path to the output file         |
| result     | _number_ | 0 = success, 1 = error               |

The Promise is rejected with `{ result, message }` if a file or folder doesn't exist or the job can't be added to the queue.

```javascript
const app = require("mediaencoder");
const result = await app.RenderQueue.enqueueFile(
  "path/to/source.mov",
  "path/to/preset.epr",
  "path/to/out.mp4",
);
result; // { jobGroupId: string, jobId: string, message: string, outputPath: string, result: number }
```

<HorizontalLine />

### enqueueImagesAsSequence

Adds a group of images an image sequence to the render queue. The images will be sorted in alphabetical order by default.

Since: **27.0**

#### Parameters

| Name                 | Type                | Description                                                                                                                                  |
| :------------------- | :------------------ | :------------------------------------------------------------------------------------------------------------------------------------------- |
| containingFolderPath | _string_            | The folder containing image files for the sequence                                                                                           |
| imageFilePath        | _string_            | The file to use as the first image file, the extension of this image path will be used in this function to filter the files in the directory |
| presetFilePath       | _string_            | File path to the preset file                                                                                                                 |
| outputFilePath       | _string (optional)_ | If outputPath is empty, then the output file name will be generated based on the containingFolderPath name                                   |

#### Returns

| Name    | Type      | Description                                      |
| :------ | :-------- | :----------------------------------------------- |
| success | _boolean_ | Returns _true_ if the job was added successfully |

```javascript
const app = require("mediaencoder");
const success = await app.RenderQueue.enqueueImagesAsSequence(
  "path/to/imagesequenceFolder",
  "path/to/imagesequenceFolder/IMAGE_0001.jpg",
  "path/to/preset.epr",
  "path/to/output/file.mp4",
);
success; // true
```

<HorizontalLine />

### enqueueProjectItem

Adds a specific sequence from a Premiere Pro project, or a specific composition from an After Effects project, to the render queue, but does not start the queue. Call [start](#start) to begin rendering, or use [renderProjectItem](#renderprojectitem) to add and start in one step.

Use [getProjectItems](#getprojectitems) to look up the IDs of the sequences or compositions in a project.

Since: **27.0**

#### Parameters

| Name           | Type                                                   | Description                                                                          |
| :------------- | :----------------------------------------------------- | :----------------------------------------------------------------------------------- |
| projectPath    | _string_                                               | File path to the Premiere Pro or After Effects project                               |
| projectItemId  | _string_                                               | ID of the sequence or composition, as returned by [getProjectItems](#getprojectitems) |
| presetFilePath | _string_                                               | File path to the preset (`.epr`) file                                                |
| outputPath     | _string_                                               | File path to the output file                                                         |
| renderOptions  | [RenderOptions](../render-options/index.md) (optional) | Render settings to apply to the job before the queue starts                          |

#### Returns

A Promise that resolves with the same result object as [enqueueFile](#enqueuefile): `{ jobGroupId, jobId, message, outputPath, result }`.

The Promise is rejected with `{ result, message }` if `projectItemId` is empty, `projectPath` is not a project file, a file or folder doesn't exist, or the job can't be added to the queue.

```javascript
const app = require("mediaencoder");
const projectPath = "path/to/project.prproj";
const items = await app.RenderQueue.getProjectItems(projectPath);
const result = await app.RenderQueue.enqueueProjectItem(
  projectPath,
  items[0].id,
  "path/to/preset.epr",
  "path/to/out.mp4",
);
result; // { jobGroupId: string, jobId: string, message: string, outputPath: string, result: number }
```

<HorizontalLine />

### renderFile

Enqueues and immediately renders a media source with the queue to render using a specified source file, preset, and output directory.

This method currently supports transcoding for various file types, including media files, Adobe Premiere project files, and Adobe After Effects project files.

For Premiere & After Effects projects, the first sequence or comp will be added to the queue. In order to specify a different sequence or comp for rendering, use [renderProjectItem](#renderprojectitem).

Since: **27.0**

#### Parameters

| Name           | Type     | Description                   |
| :------------- | :------- | :---------------------------- |
| filePath       | _string_ | File path to the media source |
| presetFilePath | _string_ | File path to the preset file  |
| outputPath     | _string_ | File path to the output file  |
| renderOptions  | [RenderOptions](../render-options/index.md) (optional) | Render settings to apply to the job before the queue starts |

#### Returns

| Name       | Type     | Description                          |
| :--------- | :------- | :----------------------------------- |
| jobGroupId | _string_ | The job group ID for the current job |
| jobId      | _string_ | The job ID for the current job       |
| message    | _string_ | Result message of enqueue action     |
| outputPath | _string_ | File path to the output file         |
| result     | _number_ | 0 = success, 1 = error               |

The Promise is rejected with `{ result, message }` if a file or folder doesn't exist or the job can't be added to the queue.

```javascript
const app = require("mediaencoder");
const result = await app.RenderQueue.renderFile(
  "path/to/source.mov",
  "path/to/preset.epr",
  "path/to/out.mp4",
);
result; // { jobGroupId: string, jobId: string, message: string, outputPath: string, result: number }
```

<HorizontalLine />

### renderProjectItem

Adds a specific sequence from a Premiere Pro project, or a specific composition from an After Effects project, to the render queue, and starts the queue. To add the item without starting the queue, use [enqueueProjectItem](#enqueueprojectitem).

Use [getProjectItems](#getprojectitems) to look up the IDs of the sequences or compositions in a project.

Since: **27.0**

#### Parameters

| Name           | Type                                                   | Description                                                                          |
| :------------- | :----------------------------------------------------- | :----------------------------------------------------------------------------------- |
| projectPath    | _string_                                               | File path to the Premiere Pro or After Effects project                               |
| projectItemId  | _string_                                               | ID of the sequence or composition, as returned by [getProjectItems](#getprojectitems) |
| presetFilePath | _string_                                               | File path to the preset (`.epr`) file                                                |
| outputPath     | _string_                                               | File path to the output file                                                         |
| renderOptions  | [RenderOptions](../render-options/index.md) (optional) | Render settings to apply to the job before the queue starts                          |

#### Returns

A Promise that resolves with the same result object as [enqueueFile](#enqueuefile): `{ jobGroupId, jobId, message, outputPath, result }`.

The Promise is rejected with `{ result, message }` if `projectItemId` is empty, `projectPath` is not a project file, a file or folder doesn't exist, or the job can't be added to the queue.

```javascript
const app = require("mediaencoder");
const projectPath = "path/to/project.prproj";
const items = await app.RenderQueue.getProjectItems(projectPath);
const sequence = items.find((item) => item.name === "Final Cut");
const result = await app.RenderQueue.renderProjectItem(
  projectPath,
  sequence.id,
  "path/to/preset.epr",
  "path/to/out.mp4",
);
result; // { jobGroupId: string, jobId: string, message: string, outputPath: string, result: number }
```

<HorizontalLine />

### stitchFiles

Stitches a list of media files together into a single output and adds it to the render queue as one job. Call [start](#start) to begin rendering.

Since: **27.0**

#### Parameters

| Name           | Type       | Description                      |
| :------------- | :--------- | :------------------------------- |
| filePaths      | _string[]_ | Array of media source file paths |
| presetPath     | _string_   | File path to the preset file     |
| outputPath     | _string_   | File path to the output file     |

#### Returns

| Name       | Type     | Description                          |
| :--------- | :------- | :----------------------------------- |
| jobGroupId | _string_ | The job group ID for the current job |
| jobId      | _string_ | The job ID for the current job       |
| message    | _string_ | Result message of enqueue action     |
| outputPath | _string_ | File path to the output file         |
| result     | _number_ | 0 = success, 1 = error               |

The Promise is rejected with `{ result, message }` if a file or folder doesn't exist or the files can't be stitched.

```javascript
const app = require("mediaencoder");
const result = await app.RenderQueue.stitchFiles(
  ["path/to/source_a.mov", "path/to/source_b.mov"],
  "path/to/preset.epr",
  "path/to/out.mp4",
);
result; // { jobGroupId: string, jobId: string, message: string, outputPath: string, result: number }
```

<HorizontalLine />

### getInstance

Gets an instance of the RenderQueue object.

Since: **27.0**

#### Parameters

none

#### Returns

[RenderQueueInstance](./render-queue-instance/index.md)

```javascript
const app = require("mediaencoder");
const instance = app.RenderQueue.getInstance();
instance; // { addEventListener, dispatchEvent, getStatus, removeEventListener, subscribeToEvent }
```

<HorizontalLine />

### getJob

Returns a [RenderJob](./render-job/index.md) object for the given job ID, or `null` if no matching job is found in the queue.

Since: **27.0**

#### Parameters

| Name  | Type     | Description                                       |
| :---- | :------- | :------------------------------------------------- |
| jobId | _string_ | The job ID returned from `renderFile` or `enqueueFile` |

#### Returns

[RenderJob](./render-job/index.md), or `null` if no matching job is found.

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

### getJobGroup

Returns a [RenderJobGroup](./render-job-group/index.md) object for the given job group ID, or `null` if no matching group is found in the queue. A group represents a single source and can contain multiple outputs ([RenderJob](./render-job/index.md) objects).

Since: **27.0**

#### Parameters

| Name       | Type     | Description                                                                        |
| :--------- | :------- | :---------------------------------------------------------------------------------- |
| jobGroupId | _string_ | The group ID returned from `renderFile`/`enqueueFile` (`jobGroupId`) or [RenderJobGroup.getID](./render-job-group/index.md#getid) |

#### Returns

[RenderJobGroup](./render-job-group/index.md), or `null` if no matching group is found.

Throws a parameter error if `jobGroupId` is not a well-formed GUID, or if there is no active render queue to resolve it against.

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

### getLogOutput

Get the Log Output of a specific render job.

Since: **27.0**

#### Parameters

| Name       | Type     | Description                          |
| :--------- | :------- | :----------------------------------- |
| jobGroupId | _string_ | The job group ID for the current job |
| jobId      | _string_ | The job ID for the current job       |

#### Returns

| Name      | Type     | Description                                                                     |
| :-------- | :------- | :------------------------------------------------------------------------------ |
| logOutput | _string_ | Returns the log output including possible warnings and errors as a JSON string. |

```javascript
const app = require("mediaencoder");
const logOutput = app.RenderQueue.getLogOutput(
  "e8105b34-f5f8-4254-84d9-6345120568f4", // jobGroupId
  "2ed0087e-da4e-43f2-86b1-f46b04382b10", // jobId
);
logOutput; // '{"error":"","summary":[],"time":"2026-07-29T10:20:56"}'
```

<HorizontalLine />

### getMissingAssets

Returns a list of missing asests for a specific render job.

Since: **27.0**

#### Parameters

| Name          | Type     | Description                                          |
| :------------ | :------- | :--------------------------------------------------- |
| jobGroupId    | _string_ | The job group ID for the current job                 |
| jobId         | _string_ | The job ID for the current job                       |
| includeSource | _boolean_ | Get missing asset from the source group if requested |
| includeOutput | _boolean_ | Get missing asset from the the job if requested      |

#### Returns

| Name          | Type       | Description                             |
| :------------ | :--------- | :-------------------------------------- |
| missingAssets | _string[]_ | Array of strings of missing asset paths |

```javascript
const app = require("mediaencoder");
const missingAssets = app.RenderQueue.getMissingAssets(
  "0115abc0-37b9-43ea-b192-f6547e57f1d7", // jobGroupId
  "1b814929-65b6-4d83-b822-68ce5cd2f741", // jobId
  true, // includeSource
  true, // includeOutput
);
missingAssets; // [
//     "Offline media detected and will be encoded using the Offline Media graphic.",
//     "Missing Asset: uhd_3840_2160_60fps.mp4"
// ]
```

<HorizontalLine />

### getProjectItems

Returns the sequences of a Premiere Pro project, or the compositions of an After Effects project, at the top level of the project. Pass an item's `id` to [renderProjectItem](#renderprojectitem) or [enqueueProjectItem](#enqueueprojectitem) to render that item.

Item names are not guaranteed to be unique, so use the `id` to identify an item.

Since: **27.0**

#### Parameters

| Name        | Type     | Description                                            |
| :---------- | :------- | :----------------------------------------------------- |
| projectPath | _string_ | File path to the Premiere Pro or After Effects project |

#### Returns

A Promise that resolves with an array of objects with the following properties:

| Name | Type     | Description                                                                        |
| :--- | :------- | :--------------------------------------------------------------------------------- |
| id   | _string_ | ID of the sequence or composition                                                  |
| name | _string_ | Name of the sequence or composition                                                |
| type | _string_ | `"sequence"` for Premiere Pro projects, `"composition"` for After Effects projects |

The Promise is rejected with `{ result, message }` if the file doesn't exist, isn't a project file, or can't be loaded.

```javascript
const app = require("mediaencoder");
const items = await app.RenderQueue.getProjectItems("path/to/project.prproj");
items; // [{ id: "7717fd87-1b69-4290-b5b0-4eb990d7afd8", name: "Sequence 01", type: "sequence" }]
```

<HorizontalLine />

### start

Starts rendering queue. Can be used to continue after a pause.

Since: **27.0**

#### Parameters

none

#### Returns

| Name   | Type      | Description                          |
| :----- | :-------- | :----------------------------------- |
| result | _boolean_ | Returns true if start was successful |

```javascript
const app = require("mediaencoder");
const success = await app.RenderQueue.start();
success; // true
```

<HorizontalLine />

### stop

Stops the complete rendering queue including all rendering items.

Since: **27.0**

#### Parameters

none

#### Returns

| Name   | Type      | Description                         |
| :----- | :-------- | :---------------------------------- |
| result | _boolean_ | Returns true if stop was successful |

```javascript
const app = require("mediaencoder");
const success = await app.RenderQueue.stop();
success; // true
```

<HorizontalLine />

### stopCurrent

Stops the current item, but continues rendering if other items are in the queue.

Since: **27.0**

#### Parameters

none

#### Returns

| Name   | Type      | Description                                |
| :----- | :-------- | :----------------------------------------- |
| result | _boolean_ | Returns true if stopCurrent was successful |

```javascript
const app = require("mediaencoder");
const success = await app.RenderQueue.stopCurrent();
success; // true
```

<HorizontalLine />

### pause

Pauses the complete rendering queue including all rendering items.

Since: **27.0**

#### Parameters

none

#### Returns

| Name   | Type      | Description                          |
| :----- | :-------- | :----------------------------------- |
| result | _boolean_ | Returns true if pause was successful |

```javascript
const app = require("mediaencoder");
const success = await app.RenderQueue.pause();
success; // true
```

<HorizontalLine />

### removeAllJobs

Removes all jobs from the queue. This method can only be called if the rendering is stopped or completed.

Since: **27.0**

#### Parameters

none

#### Returns

| Name   | Type      | Description                           |
| :----- | :-------- | :------------------------------------ |
| result | _boolean_ | Returns true if action was successful |

```javascript
const app = require("mediaencoder");
const success = await app.RenderQueue.removeAllJobs();
success; // true
```

<HorizontalLine />
