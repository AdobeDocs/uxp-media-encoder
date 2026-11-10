# Changelog

Changes to the Media Encoder API reference in `src/pages/media-encoder-api`, newest first.

## 2026-11-10

### Added

- [Preset Manager](src/pages/media-encoder-api/preset-manager/index.md) and [Preset](src/pages/media-encoder-api/preset-manager/preset/index.md) pages.
- [Guid](src/pages/media-encoder-api/guid/index.md) page.
- [WatchFolderOutput](src/pages/media-encoder-api/watch-folder/watch-folder-output/index.md) page.
- RenderQueue: `enqueueProjectItem`, `renderProjectItem`, `getProjectItems`, and the `NEXT_JOB_ENCODING_EVENT`, `MEDIA_ITEM_CREATED_EVENT`, and `ENCODE_COMPLETE_EVENT` constants.
- RenderQueue: the optional `renderOptions` parameter of `enqueueFile` and `renderFile`, and when the Promises of `enqueueFile`, `renderFile`, and `stitchFiles` are rejected.
- WatchFolder: `addOutput`, `getOutputs`, `removeOutput`, and `subscribeToEvent`, and the optional `capture` parameter of `addEventListener` and `removeEventListener`.
- C2PAService: `getInstance`.
- ProgressItem: `setType`.
- The properties of the event object that listeners receive, at every event constant.

### Changed

- RenderQueue: `enqueueFile` and `renderFile` point to `enqueueProjectItem` and `renderProjectItem` for a specific sequence or composition.
- RenderQueue: the parameters of `stitchFiles` are `filePaths`, `presetPath`, and `outputPath`, the second parameter of `enqueueImagesAsSequence` is `imageFilePath`, and `getMissingAssets` takes booleans.
- RenderOptions: `setRotation` takes a number.
- TickTime: the first parameter of `timecodeToTime` is `timecode`.
- The reference IDs of the progress APIs, `ProgressItem.referenceId`, and the parameters of `RenderOptions.setCustomInAndOutPoints` link the Guid and TickTime pages.
- Render Queue Instance: the event lists name the five render queue events.

### Removed

- RenderQueue: `getProjectItemGUIDs`. Use `getProjectItems`.
- RenderOptions: `setSequenceGUID`. Use `renderProjectItem` or `enqueueProjectItem`.

### Fixed

- WatchFolder: `createWatchFolder`, `getAllWatchFolders`, and `removeAllWatchFolders` return Promises. The examples await them, and errors reject the Promise instead of throwing.
- WatchFolder: the listener examples call `subscribeToEvent`, without which listeners never fire.
- WatchFolder: the value of `WATCH_FOLDER_ENCODER_STATUS_CHANGED` is `"WatchFolderStatusEvent"`.
- RenderQueue: `stitchFiles` adds one job and doesn't start the queue.
- Render Queue Instance: `WATCH_FOLDER_ENCODER_STATUS_CHANGED` is a watch folder event, and `addEventListener` documents the `capture` parameter instead of a TODO.
- ProgressItem: `referenceId` always has a value.
- Media Encoder API landing page: Render Options doesn't choose presets or output paths.
- Broken anchor links on the Render Queue Instance and ProgressCategoryContainer pages.
