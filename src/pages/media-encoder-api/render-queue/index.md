---
title: "Render Queue: Media Encoder API"
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


contributors:
  - https://github.com/justintaylor-dev
---

# Render Queue

<InlineAlert variant="info" slots="text"/>

UXP for Adobe Media Encoder is in public beta. This reference is being written, and the supported API surface may change before general availability.

Since: **26.5**

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

Retrieves the unique identifier for the progress category for global progress of the AME renderer. This ID allows access to the global progress of the AME Renderer. To obtain the category, use `getOrCreateProgressCategory()` method from the ProgressCategoryContainer object. The ProgressItemScriptObject should be used to manage individual progress items. Each job item is registered using its unique reference ID.

Type: _string_

Since: **26.5**

<HorizontalLine />

### RENDER_QUEUE_INVALID_STATE

Render queue invalid state.

Type: _int_

Since: **26.5**

<HorizontalLine />

### RENDER_QUEUE_PAUSED

Render queue paused state.

Type: _int_

Since: **26.5**

<HorizontalLine />

### RENDER_QUEUE_RUNNING

Render queue running state.

Type: _int_

Since: **26.5**

<HorizontalLine />

### RENDER_QUEUE_STOPPED

Render queue stopped state.

Type: _int_

Since: **26.5**

<HorizontalLine />

### RESULT_ERROR

Validation result when your render job returns an error.

Type: _int_

Since: **26.5**

<HorizontalLine />

### RESULT_SUCCESS

Validation result when your render job returns successfully.

Type: _int_

Since: **26.5**

<HorizontalLine />

## Methods

### enqueueFile

Enqueues a media source with a given RenderOptions object but does NOT start the queue to render. Renders a media source using a specified preset.

This method currently supports transcoding for various file types, including media files, Adobe Premiere project files, Adobe After Effects project files, and unified project files.

For Premiere & After Effects projects, the first sequence or comp will be added to the queue. In order to specify a different sequence or comp for rendering, see `getProjectItemGUIDs()` and `setSequenceGUID()`.

Since: **26.5**

#### Parameters

| Name           | Type     | Description                   |
| :------------- | :------- | :---------------------------- |
| filePath       | _string_ | File path to the media source |
| presetFilePath | _string_ | File path to the preset file  |
| outputPath     | _string_ | File path to the output file  |

#### Returns

| Name       | Type     | Description                          |
| :--------- | :------- | :----------------------------------- |
| jobGroupId | _string_ | The job group ID for the current job |
| jobId      | _string_ | The job ID for the current job       |
| message    | _string_ | Result message of enqueue action     |
| outputPath | _string_ | File path to the output file         |
| result     | _number_ | 0 = success, 1 = error               |

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

Since: **26.5**

#### Parameters

| Name                 | Type                | Description                                                                                                                                  |
| :------------------- | :------------------ | :------------------------------------------------------------------------------------------------------------------------------------------- |
| containingFolderPath | _string_            | The folder containing image files for the sequence                                                                                           |
| firstImageFilePath   | _string_            | The file to use as the first image file, the extension of this image path will be used in this function to filter the files in the directory |
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

### renderFile

Enqueues and immediately renders a media source with the queue to render using a specified source file, preset, and output directory.

This method currently supports transcoding for various file types, including media files, Adobe Premiere project files, Adobe After Effects project files, and unified project files.

For Premiere & After Effects projects, the first sequence or comp will be added to the queue. In order to specify a different sequence or comp for rendering, see `getProjectItemGUIDs()` and `setSequenceGUID()`.

Since: **26.5**

#### Parameters

| Name           | Type     | Description                   |
| :------------- | :------- | :---------------------------- |
| filePath       | _string_ | File path to the media source |
| presetFilePath | _string_ | File path to the preset file  |
| outputPath     | _string_ | File path to the output file  |

#### Returns

| Name       | Type     | Description                          |
| :--------- | :------- | :----------------------------------- |
| jobGroupId | _string_ | The job group ID for the current job |
| jobId      | _string_ | The job ID for the current job       |
| message    | _string_ | Result message of enqueue action     |
| outputPath | _string_ | File path to the output file         |
| result     | _number_ | 0 = success, 1 = error               |

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

### getInstance

Gets an instance of the RenderQueue object.

Since: **26.5**

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

### getLogOutput

Get the Log Output of a specific render job.

Since: **26.5**

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

Since: **26.5**

#### Parameters

| Name          | Type     | Description                                          |
| :------------ | :------- | :--------------------------------------------------- |
| jobGroupId    | _string_ | The job group ID for the current job                 |
| jobId         | _string_ | The job ID for the current job                       |
| includeSource | _string_ | Get missing asset from the source group if requested |
| includeOutput | _string_ | Get missing asset from the the job if requested      |

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

### start

Starts rendering queue. Can be used to continue after a pause.

Since: **26.5**

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

Since: **26.5**

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

Since: **26.5**

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

Since: **26.5**

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

Since: **26.5**

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
