---
title: "Watch Folder: Media Encoder API"
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


contributors:
  - https://github.com/justintaylor-dev
  - https://github.com/sukriyeLudwig
---

# Watch Folder

<InlineAlert variant="info" slots="text"/>

UXP for Adobe Media Encoder is in public beta. This reference is being written, and the supported API surface may change before general availability.

Since: **26.5**

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
  WatchFolder.WATCH_FOLDER_ENCODER_STATUS_CHANGED; // "AMEProgressCategoryRender"
```

### PROGRESS_CATEGORY_ID

Retrieves the unique identifier for the progress category for global progress of the AME renderer. This ID allows access to the global progress of the AME Renderer. To obtain the category, use [getOrCreateProgressCategory()](../progress-category-container/index.md#getorcreateprogresscategory) on the [ProgressCategoryContainer](../progress-category-container/index.md) object. The [ProgressItem](../progress-category-container/progress-item/index.md) object should be used to manage individual progress items. Each job item is registered using its unique reference ID.

Type: _string_

Since: **26.5**

<HorizontalLine />

### WATCH_FOLDER_ENCODER_STATUS_CHANGED

Event ID for when a watch folder encoder status changes.

Type: _string_

Since: **26.5**

<HorizontalLine />

## Properties

These read-only properties are available on a watch folder object, such as the one returned by [createWatchFolder](#createwatchfolder).

```javascript
const app = require("mediaencoder");
const watchFolder = app.WatchFolder.createWatchFolder(
  "path/to/source",
  "path/to/destination",
  "path/to/preset.epr",
);
watchFolder.id; // "e8105b34-f5f8-4254-84d9-6345120568f4"
```

### id

The unique identifier (GUID) for the watch folder.

Type: _string_ (readonly)

Since: **26.5**

<HorizontalLine />

### filePath

The source path being monitored by the watch folder.

Type: _string_ (readonly)

Since: **26.5**

<HorizontalLine />

### presetPath

The preset file path used for encoding.

Type: _string_ (readonly)

Since: **26.5**

<HorizontalLine />

### destinationPath

The destination path where encoded files are saved.

Type: _string_ (readonly)

Since: **26.5**

<HorizontalLine />

## Methods

### getInstance

Gets an instance of the `WatchFolder` object.

Since: **26.5**

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

Since: **26.5**

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
const watchFolder = app.WatchFolder.createWatchFolder(
  "path/to/source",
  "path/to/destination",
  "path/to/preset.epr",
);
watchFolder; // { id, filePath, presetPath, destinationPath }
```

Throws a parameter error if the source path, destination path, or preset path does not exist or is invalid, or if the preset uses an unsupported HEVC encoding format (when called from a non-first-party context).

<HorizontalLine />

### getAllWatchFolders

Returns an array of all active watch folder objects.

Since: **26.5**

#### Parameters

none

#### Returns

| Name         | Type       | Description                             |
| :----------- | :--------- | :---------------------------------------- |
| watchFolders | _object[]_ | Array of all active watch folder objects |

```javascript
const app = require("mediaencoder");
const watchFolders = app.WatchFolder.getAllWatchFolders();
```

<HorizontalLine />

### removeAllWatchFolders

Removes all active watch folders from the system.

Since: **26.5**

#### Parameters

none

#### Returns

| Name   | Type      | Description                          |
| :----- | :-------- | :-------------------------------------- |
| result | _boolean_ | Returns `true` if removal was successful |

```javascript
const app = require("mediaencoder");
const success = app.WatchFolder.removeAllWatchFolders();
success; // true
```

<HorizontalLine />

### addEventListener

Registers an event handler for the specified event on this `WatchFolder`. The event handling follows the W3C DOM Level 2 Events Specification.

Since: **26.5**

#### Parameters

| Name      | Type       | Description                                                                                                     |
| :-------- | :--------- | :----------------------------------------------------------------------------------------------------------------- |
| eventType | _string_   | The event to listen for, such as [WATCH_FOLDER_ENCODER_STATUS_CHANGED](#watchfolderencoderstatuschanged)      |
| handler   | _function_ | A function to be triggered when the specified event occurs                                                       |

#### Returns

none

```javascript
const app = require("mediaencoder");
const watchFolder = app.WatchFolder.getInstance();
const event = app.WatchFolder.WATCH_FOLDER_ENCODER_STATUS_CHANGED;
const callback = (statusEvent) => {
  console.log("Watch Folder Encoder Status Changed", statusEvent.status);
};
watchFolder.addEventListener(event, callback);
```

<HorizontalLine />

### removeEventListener

Unregisters a previously registered event handler for the specified event on this `WatchFolder`.

Since: **26.5**

#### Parameters

| Name      | Type       | Description                                          |
| :-------- | :--------- | :------------------------------------------------------ |
| eventType | _string_   | The event to stop listening for                        |
| handler   | _function_ | The previously registered callback to remove             |

#### Returns

none

```javascript
const app = require("mediaencoder");
const watchFolder = app.WatchFolder.getInstance();
const event = app.WatchFolder.WATCH_FOLDER_ENCODER_STATUS_CHANGED;
const callback = (statusEvent) => {
  console.log("Watch Folder Encoder Status Changed", statusEvent.status);
};
watchFolder.addEventListener(event, callback);
watchFolder.removeEventListener(event, callback);
```

<HorizontalLine />
