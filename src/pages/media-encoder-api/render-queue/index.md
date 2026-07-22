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

# Constants

These Render Queue Constants are used as parameters in various `RenderQueue` API methods for Media Encoder.

All Constants can be accessed via the `RenderQueue` object:

```javascript
const app = require("mediaencoder");
const renderQueue = app.RenderQueue;
const PROGRESS_CATEGORY_ID = renderQueue.PROGRESS_CATEGORY_ID; // "AMEProgressCategoryRender"
const RENDER_QUEUE_RUNNING = renderQueue.RENDER_QUEUE_RUNNING; // 2
```

| Name                       | Min Version | Type     | Description                                                                                                                                                                                                                                                                                                                                                                                                                    |
| :------------------------- | :---------- | :------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| PROGRESS_CATEGORY_ID       | 26.5        | _string_ | Retrieves the unique identifier for the progress category for global progress of the AME renderer. This ID allows access to the global progress of the AME Renderer. To obtain the category, use `getOrCreateProgressCategory()` method from the ProgressCategoryContainer object. The ProgressItemScriptObject should be used to manage individual progress items. Each job item is registered using its unique reference ID. |
| RENDER_QUEUE_INVALID_STATE | 26.5        | _int_    | Render queue invalid state.                                                                                                                                                                                                                                                                                                                                                                                                    |
| RENDER_QUEUE_PAUSED        | 26.5        | _int_    | Render queue paused.                                                                                                                                                                                                                                                                                                                                                                                                           |
| RENDER_QUEUE_RUNNING       | 26.5        | _int_    | Render queue running.                                                                                                                                                                                                                                                                                                                                                                                                          |
| RENDER_QUEUE_STOPPED       | 26.5        | _int_    | Render queue stopped.                                                                                                                                                                                                                                                                                                                                                                                                          |
| RENDER_QUEUE_STOPPING      | 26.5        | _int_    | Render queue stopping.                                                                                                                                                                                                                                                                                                                                                                                                         |
| RESULT_ERROR               | 26.5        | _int_    | Validation result when your render job returns an error.                                                                                                                                                                                                                                                                                                                                                                       |
| RESULT_SUCCESS             | 26.5        | _int_    | Validation result when your render job returns successfully.                                                                                                                                                                                                                                                                                                                                                                   |

<HorizontalLine />

# Methods

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

| Name       | Type     | Description                                             |
| :--------- | :------- | :------------------------------------------------------ |
| jobGroupId | _string_ | Job group id, that contains the job you are looking for |
| jobId      | _string_ | to be able to get log output info only from the job     |
| message    | _string_ | Result message of enqueue action                        |
| outputPath | _string_ | File path to the output file                            |
| result     | _number_ | 0 = success, 1 = error                                  |

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
