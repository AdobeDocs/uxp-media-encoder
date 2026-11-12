---
title: Watch Folder Media Encoder API
description: "Media Encoder's Watch Folder APIs for creating and managing watch folders that automatically encode new files."
id: watchFolder
title: WatchFolder
sidebar_label: WatchFolder
product: mediaencoder
keywords:
  - UXP
  - Adobe Media Encoder
  - Media Encoder API
  - watch folder
  - encoding queue
  - scripting automation
  - addOutput
  - WatchFolderOutput


contributors:
  - https://github.com/justintaylor-dev
  - https://github.com/sukriyeLudwig
---

# Watch Folder

<InlineAlert variant="info" slots="text"/>

UXP for Adobe Media Encoder is in public beta. This reference is being written, and the supported API surface may change before general availability.

Since: **27.0**

The Media Encoder Watch Folder API is the used for all operations involving managing Watch Folders in Media Encoder. A watch folder monitors a source directory and automatically encodes new files using a specified preset.

The Watch Folder object can be acceessed from the main app object:

```javascript
const app = require("mediaencoder");
const WatchFolder = app.WatchFolder;
```

<HorizontalLine />

## Constants

These Watch Folder Constants are used as parameters in various `WatchFolder` API methods for Media Encoder.

All Constants can be accessed via the `WatchFolder` object:

```javascript
const app = require("mediaencoder");
const WatchFolder = app.WatchFolder;
const WATCH_FOLDER_ENCODER_STATUS_CHANGED =
  WatchFolder.WATCH_FOLDER_ENCODER_STATUS_CHANGED; // "WatchFolderStatusEvent"
```

### PROGRESS_CATEGORY_ID

Retrieves the unique identifier for the progress category for global progress of the AME renderer. This ID allows access to the global progress of the AME Renderer. To obtain the category, use [getOrCreateProgressCategory()](../progress-category-container/index.md#getorcreateprogresscategory) on the [ProgressCategoryContainer](../progress-category-container/index.md) object. The [ProgressItem](../progress-category-container/progress-item/index.md) object should be used to manage individual progress items. Each job item is registered using its unique reference ID.

Type: _string_

Since: **27.0**

<HorizontalLine />

### WATCH_FOLDER_ENCODER_STATUS_CHANGED

Event ID for when a watch folder encoder status changes.

The listener receives a `WatchFolderStatusEvent` object with the following property:

| Name   | Type  | Description                                                                                                                 |
| :----- | :---- | :-------------------------------------------------------------------------------------------------------------------------- |
| status | _int_ | The new status of the watch folder encoder. Uses the same values as the [RENDER_QUEUE_* constants](../render-queue/index.md#constants) |

Type: _string_

Since: **27.0**

<HorizontalLine />

## Properties

These read-only properties are available on a watch folder object, such as the one returned by [createWatchFolder](#createwatchfolder).

```javascript
const app = require("mediaencoder");
const watchFolder = await app.WatchFolder.createWatchFolder(
  "path/to/source",
  "path/to/destination",
  "path/to/preset.epr",
);
watchFolder.id; // "e8105b34-f5f8-4254-84d9-6345120568f4"
```

### id

The unique identifier (GUID) for the watch folder.

Type: _string_ (readonly)

Since: **27.0**

<HorizontalLine />

### filePath

The source path being monitored by the watch folder.

Type: _string_ (readonly)

Since: **27.0**

<HorizontalLine />

### presetPath

The preset file path used for encoding.

Type: _string_ (readonly)

Since: **27.0**

<HorizontalLine />

### destinationPath

The destination path where encoded files are saved.

Type: _string_ (readonly)

Since: **27.0**

<HorizontalLine />

## Methods

### getInstance

Gets an instance of the `WatchFolder` object.

Since: **27.0**

#### Parameters

none

#### Returns

| Name        | Type     | Description             |
| :---------- | :------- | :------------------------ |
| watchFolder | _object_ | A `WatchFolder` object   |

```javascript
const app = require("mediaencoder");
const watchFolder = app.WatchFolder.getInstance();
```

<HorizontalLine />

### createWatchFolder

Creates a watch folder that monitors the source directory and automatically encodes new files using the specified preset. The watch folder will process any new files added to the source directory and save the encoded output to the destination directory.

Since: **27.0**

#### Parameters

| Name            | Type     | Description                                                        |
| :--------------- | :------- | :-------------------------------------------------------------------- |
| sourcePath       | _string_ | The path to the folder which should be monitored as a watch folder   |
| destinationPath  | _string_ | The path where encoded files will be saved                           |
| presetPath       | _string_ | The full path to the preset file (`*.epr`) to use for encoding       |

#### Returns

A watch folder item object with the following read-only properties:

| Name            | Type     | Description                                          |
| :--------------- | :------- | :------------------------------------------------------ |
| id              | _string_ | The unique identifier (GUID) for the watch folder     |
| filePath        | _string_ | The source path being monitored by the watch folder   |
| presetPath      | _string_ | The preset file path used for encoding                |
| destinationPath | _string_ | The destination path where encoded files are saved     |

```javascript
const app = require("mediaencoder");
const watchFolder = await app.WatchFolder.createWatchFolder(
  "path/to/source",
  "path/to/destination",
  "path/to/preset.epr",
);
watchFolder; // { id, filePath, presetPath, destinationPath }
```

The Promise is rejected with an error message if the source path, destination path, or preset path does not exist or is invalid, or if the preset uses an unsupported HEVC encoding format (when called from a non-first-party context).

<HorizontalLine />

### getAllWatchFolders

Returns an array of all active watch folder objects.

Since: **27.0**

#### Parameters

none

#### Returns

| Name         | Type       | Description                             |
| :----------- | :--------- | :---------------------------------------- |
| watchFolders | _object[]_ | Array of all active watch folder objects |

```javascript
const app = require("mediaencoder");
const watchFolders = await app.WatchFolder.getAllWatchFolders();
```

<HorizontalLine />

### removeAllWatchFolders

Removes all active watch folders from the system.

Since: **27.0**

#### Parameters

none

#### Returns

| Name   | Type      | Description                          |
| :----- | :-------- | :-------------------------------------- |
| result | _boolean_ | Returns `true` if removal was successful |

```javascript
const app = require("mediaencoder");
const success = await app.WatchFolder.removeAllWatchFolders();
success; // true
```

<HorizontalLine />

### addOutput

Adds another output to this watch folder. Each output has its own preset and destination folder, so a single watch folder can encode every new file into several formats. Ingest presets are not supported.

Call this method on a watch folder object, such as one returned by [createWatchFolder](#createwatchfolder) or [getAllWatchFolders](#getallwatchfolders).

Since: **27.0**

#### Parameters

| Name            | Type     | Description                                                          |
| :-------------- | :------- | :------------------------------------------------------------------- |
| presetPath      | _string_ | The full path to the preset file (`*.epr`) to use for the new output |
| destinationPath | _string_ | The path where the output's encoded files are saved                  |

#### Returns

A Promise that resolves with a [WatchFolderOutput](./watch-folder-output/index.md) describing the new output.

The Promise is rejected with an error message if the destination folder doesn't exist, if the preset file is missing, can't be read, is an ingest preset, or uses an unsupported HEVC encoding format (when called from a non-first-party context), if the watch folder no longer exists, or if the output can't be added.

```javascript
const app = require("mediaencoder");
const watchFolder = await app.WatchFolder.createWatchFolder(
  "path/to/source",
  "path/to/destination",
  "path/to/preset.epr",
);
const output = await watchFolder.addOutput("path/to/other-preset.epr", "path/to/other-destination");
output; // { id, presetPath, destinationPath }
```

<HorizontalLine />

### getOutputs

Returns the outputs of this watch folder. Call this method on a watch folder object.

Since: **27.0**

#### Parameters

none

#### Returns

| Name    | Type       | Description                                                          |
| :------ | :--------- | :------------------------------------------------------------------- |
| outputs | _object[]_ | Array of [WatchFolderOutput](./watch-folder-output/index.md) objects |

The Promise resolves with an empty array if the watch folder no longer exists.

```javascript
const app = require("mediaencoder");
const [watchFolder] = await app.WatchFolder.getAllWatchFolders();
const outputs = await watchFolder.getOutputs();
outputs.forEach((output) => console.log(output.id, output.destinationPath));
```

<HorizontalLine />

### removeOutput

Removes an output from this watch folder. Call this method on a watch folder object.

Since: **27.0**

#### Parameters

| Name     | Type     | Description                                                                    |
| :------- | :------- | :----------------------------------------------------------------------------- |
| outputId | _string_ | The `id` of the [WatchFolderOutput](./watch-folder-output/index.md) to remove |

#### Returns

| Name   | Type      | Description                              |
| :----- | :-------- | :--------------------------------------- |
| result | _boolean_ | Returns `true` if the output was removed |

The Promise is rejected with an error message if `outputId` is empty, the watch folder no longer exists, or the output can't be removed.

```javascript
const app = require("mediaencoder");
const [watchFolder] = await app.WatchFolder.getAllWatchFolders();
const [output] = await watchFolder.getOutputs();
await watchFolder.removeOutput(output.id); // true
```

<HorizontalLine />

### subscribeToEvent

Registers a subscription to a watch folder event. After subscribing, call [addEventListener](#addeventlistener) to react to the event.

Since: **27.0**

#### Parameters

| Name     | Type     | Description                                                                                                         |
| :------- | :------- | :------------------------------------------------------------------------------------------------------------------ |
| eventKey | _string_ | The event ID to subscribe to: [WATCH_FOLDER_ENCODER_STATUS_CHANGED](#watch_folder_encoder_status_changed)            |

#### Returns

| Name    | Type      | Description                                                                          |
| :------ | :-------- | :----------------------------------------------------------------------------------- |
| success | _boolean_ | Returns `true` if subscription was successful, `false` if `eventKey` is not a watch folder event |

```javascript
const app = require("mediaencoder");
const watchFolder = app.WatchFolder.getInstance();
const event = app.WatchFolder.WATCH_FOLDER_ENCODER_STATUS_CHANGED;
watchFolder.subscribeToEvent(event); // true
watchFolder.addEventListener(event, (statusEvent) => {
  console.log("Watch folder encoder status:", statusEvent.status);
});
```

<HorizontalLine />

### addEventListener

Registers an event handler for the specified event on this `WatchFolder`. The event handling follows the W3C DOM Level 2 Events Specification.

Since: **27.0**

#### Parameters

| Name      | Type       | Description                                                                                                     |
| :-------- | :--------- | :----------------------------------------------------------------------------------------------------------------- |
| eventType | _string_   | The event to listen for, such as [WATCH_FOLDER_ENCODER_STATUS_CHANGED](#watch_folder_encoder_status_changed)      |
| handler   | _function_ | A function to be triggered when the specified event occurs                                                       |
| capture   | _boolean (optional)_ | `true` to call the handler during the capture phase. Also accepts an options object with a `capture` property. Defaults to `false` |

#### Returns

none

```javascript
const app = require("mediaencoder");
const watchFolder = app.WatchFolder.getInstance();
const event = app.WatchFolder.WATCH_FOLDER_ENCODER_STATUS_CHANGED;
watchFolder.subscribeToEvent(event);
const callback = (statusEvent) => {
  console.log("Watch Folder Encoder Status Changed", statusEvent.status);
};
watchFolder.addEventListener(event, callback);
```

<HorizontalLine />

### removeEventListener

Unregisters a previously registered event handler for the specified event on this `WatchFolder`.

Since: **27.0**

#### Parameters

| Name      | Type       | Description                                          |
| :-------- | :--------- | :------------------------------------------------------ |
| eventType | _string_   | The event to stop listening for                        |
| handler   | _function_ | The previously registered callback to remove             |
| capture   | _boolean (optional)_ | Must match the `capture` value used in [addEventListener](#addeventlistener). Defaults to `false` |

#### Returns

none

```javascript
const app = require("mediaencoder");
const watchFolder = app.WatchFolder.getInstance();
const event = app.WatchFolder.WATCH_FOLDER_ENCODER_STATUS_CHANGED;
watchFolder.subscribeToEvent(event);
const callback = (statusEvent) => {
  console.log("Watch Folder Encoder Status Changed", statusEvent.status);
};
watchFolder.addEventListener(event, callback);
watchFolder.removeEventListener(event, callback);
```

<HorizontalLine />
