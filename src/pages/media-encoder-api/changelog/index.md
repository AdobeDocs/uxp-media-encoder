---
title: Media Encoder API Changelog
description: "Release notes for the Adobe Media Encoder UXP API, including new APIs, behavior changes, bug fixes, and documentation updates."
keywords:
  - Adobe Media Encoder
  - UXP
  - Media Encoder API
  - changelog
---

# Changelog

## Media Encoder v27.0.0

This release adds new Media Encoder APIs, updates the behavior and parameters of existing APIs, and brings the API reference in line with the current scripting API.

**Documentation updated:** November 10, 2026

### Breaking Changes

#### Project item rendering

The `RenderQueue.getProjectItemGUIDs` method and the `RenderOptions.setSequenceGUID` method have been removed.

Use `RenderQueue.getProjectItems` to find the sequences or compositions in a project. Pass the returned item ID to `RenderQueue.enqueueProjectItem` to add a job without starting the queue, or to `RenderQueue.renderProjectItem` to add and start the job.

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
```

### New APIs

The following APIs are now documented in the Media Encoder reference:

- [Preset Manager](../preset-manager/index.md) provides access to available export formats and presets.
- [Preset](../preset-manager/preset/index.md) describes the preset objects returned by Preset Manager.
- [Guid](../guid/index.md) provides GUID creation and conversion methods.
- [Watch Folder Output](../watch-folder/watch-folder-output/index.md) describes the output settings managed by a watch folder.
- [Render Queue](../render-queue/index.md) now documents `getProjectItems`, `enqueueProjectItem`, and `renderProjectItem`.
- [Render Queue](../render-queue/index.md) now documents the `NEXT_JOB_ENCODING_EVENT`, `MEDIA_ITEM_CREATED_EVENT`, and `ENCODE_COMPLETE_EVENT` constants.
- [Watch Folder](../watch-folder/index.md) now documents `addOutput`, `getOutputs`, `removeOutput`, and `subscribeToEvent`.
- [C2PAService](../c2pa-service/index.md) now documents `getInstance`.
- [Progress Item](../progress-category-container/progress-item/index.md) now documents `setType`.

### API Updates

- [Render Queue](../render-queue/index.md) `enqueueFile` and `renderFile` accept an optional `renderOptions` parameter.
- [Render Queue](../render-queue/index.md) documents the conditions under which the Promises returned by `enqueueFile`, `renderFile`, and `stitchFiles` are rejected.
- [Render Queue](../render-queue/index.md) `stitchFiles` takes `filePaths`, `presetPath`, and `outputPath`. The second parameter of `enqueueImagesAsSequence` is `imageFilePath`, and `getMissingAssets` takes booleans.
- [Watch Folder](../watch-folder/index.md) `addEventListener` and `removeEventListener` accept an optional `capture` parameter.
- [Render Options](../render-options/index.md) `setRotation` takes a number.
- [TickTime](../tick-time/index.md) `timecodeToTime` takes `timecode` as its first parameter.
- The progress APIs, `ProgressItem.referenceId`, and the parameters of `RenderOptions.setCustomInAndOutPoints` now link to the [Guid](../guid/index.md) and [TickTime](../tick-time/index.md) reference pages.
- [Render Queue Instance](../render-queue/render-queue-instance/index.md) lists the five render queue events.
- Event constants document the properties of the event objects received by listeners.

### Bug Fixes

- [Watch Folder](../watch-folder/index.md) `createWatchFolder`, `getAllWatchFolders`, and `removeAllWatchFolders` return Promises. Their examples now await the results, and errors reject the Promise instead of throwing.
- [Watch Folder](../watch-folder/index.md) listener examples call `subscribeToEvent`, which is required for listeners to fire.
- [Watch Folder](../watch-folder/index.md) `WATCH_FOLDER_ENCODER_STATUS_CHANGED` has the value `"WatchFolderStatusEvent"`.
- [Render Queue](../render-queue/index.md) `stitchFiles` adds one job and does not start the queue.
- [Render Queue Instance](../render-queue/render-queue-instance/index.md) identifies `WATCH_FOLDER_ENCODER_STATUS_CHANGED` as a watch folder event and documents the `capture` parameter for `addEventListener`.
- [Progress Item](../progress-category-container/progress-item/index.md) `referenceId` always has a value.

### Documentation Updates

- The [Media Encoder API overview](../index.md) no longer says that Render Options chooses presets or output paths.
- Broken anchor links on the [Render Queue Instance](../render-queue/render-queue-instance/index.md) and [Progress Category Container](../progress-category-container/index.md) pages have been fixed.
