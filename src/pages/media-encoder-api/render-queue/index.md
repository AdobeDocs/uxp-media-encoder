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

| Name                       | Min Version | Type   | Description                                                                                                                                                                                                                                                                                                                                                                                                                    |
| :------------------------- | :---------- | :----- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| PROGRESS_CATEGORY_ID       | 26.5        | string | Retrieves the unique identifier for the progress category for global progress of the AME renderer. This ID allows access to the global progress of the AME Renderer. To obtain the category, use `getOrCreateProgressCategory()` method from the ProgressCategoryContainer object. The ProgressItemScriptObject should be used to manage individual progress items. Each job item is registered using its unique reference ID. |
| RENDER_QUEUE_INVALID_STATE | 26.5        | int    | Render queue invalid state.                                                                                                                                                                                                                                                                                                                                                                                                    |
| RENDER_QUEUE_PAUSED        | 26.5        | int    | Render queue paused.                                                                                                                                                                                                                                                                                                                                                                                                           |
| RENDER_QUEUE_RUNNING       | 26.5        | int    | Render queue running.                                                                                                                                                                                                                                                                                                                                                                                                          |
| RENDER_QUEUE_STOPPED       | 26.5        | int    | Render queue stopped.                                                                                                                                                                                                                                                                                                                                                                                                          |
| RENDER_QUEUE_STOPPING      | 26.5        | int    | Render queue stopping.                                                                                                                                                                                                                                                                                                                                                                                                         |
| RESULT_ERROR               | 26.5        | int    | Validation result when your render job returns an error.                                                                                                                                                                                                                                                                                                                                                                       |
| RESULT_SUCCESS             | 26.5        | int    | Validation result when your render job returns successfully.                                                                                                                                                                                                                                                                                                                                                                   |

<HorizontalLine />

# Methods

<InlineAlert variant="info" slots="text"/>

⚠️ The below items still need to be formatted... 👇

- `enqueueFile(filePath: string, presetFilePath: string, outputPath: string): native object`

Enqueues a media source with a given RenderOptions object but does NOT start the queue to render. Renders a media source using a specified preset. This method currently supports transcoding for various file types, including movie files, Adobe Premiere Pro project files, Adobe After Effects project files, and unified project files. Sequence GUID: When rendering Premiere Pro project files or After Effects you can specify a sequence GUID to define which sequence to render. To retrieve sequence GUIDs, use the getProjectItemGUIDs method and set this guid using RenderOptions object. The method name is setSequenceGUID. If you want to add an Adobe Premiere Pro project file, an Adobe After Effects file, or a unified project file without specifying a sequence GUID, you can use the enqueueFile method. In this case, the first sequence ID found in the project file will be used by default. Available Options: The render options include a variety of settings such as sequenceId, work area type, custom in and out points, rotation, and more. The render options will be applied to scheduled job before the queue starts For a comprehensive list and detailed explanations of each option, please refer to the RenderOptions scripting API documentation

- `filePath`: File path to the media source
- `presetFilePath`: File path to the preset file
- `outputPath`: File path to the output file

- `enqueueImagesAsSequence(containingFolderPath: string, imageFilePath: string, presetFilePath: string, outputFilePath: string = ""): bool`

Adds an image sequence to the render queue as a sequence. The images will be sorted in alphabetical order.

- `containingFolderPath`: The folder containing image files
- `imageFilePath`: The extension of this image path will be used in this function to filter the files in the directory
- `outputFilePath`: If outputPath is empty, then the output file name will be generated based on the containingFolder name - optional -

- `getInstance(): scripting object`

Gets an instance of the RenderQueue object.

- `getLogOutput(jobGroupId: string, jobId: string): string`

Returns the log output including possible warnings and errors as a JSON string.

- `jobGroupId`: Job group id, that contains the job you are looking for
- `jobId`: to be able to get log output info only from the job

- `getMissingAssets(jobGroupId: string, jobId: string, includeSource: bool, includeOutput: bool): array of strings`

Returns a list of missing assets.

- `jobGroupId`: Job group id. To get the missing assets from the group
- `jobId`: to be able to get missing assets info only from the job
- `includeSource`: Get missing asset from the source group if requested
- `includeOutput`: Get missing asset from the the job if requested

- `getProjectItemGUIDs(projectPath: string): native object`

Returns the list of GUIDs for objects (sequences/compositions) at the top/root level.

- `projectPath`: E.g. Premiere Pro or After Effects project path.

- `getStatus(): int`

Provides the current status of the rendering queue, represented as an enumeration. The possible states are: Stopped = 0, Paused = 1, Running = 2, Stopping = 3, InvalidState = 4 These states can be accessed as enum types using a RenderQueueEvent object. For example, you can check the render queue status using renderqueueEventObject.RENDER_QUEUE_RUNNING. For more information, refer to the RenderQueueEvent scripting API documentation

- `pause(): bool`

Pause the complete rendering (all rendering items).

- `removeAllJobs(): bool`

Remove all jobs from the queue. Can only be called if the rendering is stopped (or finished).

- `renderFile(filePath: string, presetFilePath: string, outputPath: string): native object`

Renders a media source using a specified preset. This method currently supports transcoding for various file types, including movie files, Adobe Premiere Pro project files, Adobe After Effects project files, and unified project files. Sequence GUID: When rendering Premiere Pro project files or After Effects you can specify a sequence GUID to define which sequence to render. To retrieve sequence GUIDs, use the getProjectItemGUIDs method and set this guid using RenderOptions object. If you want to add an Adobe Premiere Pro project file, an Adobe After Effects file, or a unified project file without specifying a sequence GUID, you can use the renderFile method. In this case, the first sequence ID found in the project file will be used by default. Available Options: The render options include a variety of settings such as sequenceId, work area type, custom in and out points, rotation, and more. The render options will be applied to scheduled job before the queue starts. For a comprehensive list and detailed explanations of each option, please refer to the RenderOptions scripting API documentation

- `filePath`: File path to the media source
- `presetFilePath`: File path to the preset file
- `outputPath`: File path to the output file

- `start(): bool`

Start the rendering (e.g., used to continue after pause).

- `stitchFiles(filePaths: array of strings, presetPath: string, outputPath: string): native object`

Given a list of media files, this method stitches them together.

- `filePaths`: List of media source file paths.
- `presetPath`: If no preset is used then the default preset of the specified format will be applied.

- `stop(): bool`

Stop the complete rendering (all rendering items).

- `stopCurrent(): bool`

Stop the current item, but continue if there are other items in the queue
