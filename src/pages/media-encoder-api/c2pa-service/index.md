---
title: "C2PAService: Media Encoder API"
description: "Media Encoder's C2PAService API for reading Content Credentials (C2PA) manifests from media files."
id: c2paService
title: C2PAService
sidebar_label: C2PAService
product: mediaencoder
keywords:
  - UXP
  - Adobe Media Encoder
  - Media Encoder API
  - C2PA
  - Content Credentials
  - scripting automation


contributors:
  - https://github.com/sukriyeLudwig
---

# C2PAService

<InlineAlert variant="info" slots="text"/>

UXP for Adobe Media Encoder is in public beta. This reference is being written, and the supported API surface may change before general availability.

Since: **26.5**

The `C2PAService` object provides access to Content Credentials (C2PA) manifest data embedded in, or associated with, a media file. Use [getManifest](#getmanifest) to read the manifest for a given file path.

The `C2PAService` object can be accessed from the main app object:

```javascript
const app = require("mediaencoder");
const c2paService = app.C2PAService;
```

<HorizontalLine />

## Constants

These C2PA Manifest Location Flags are class properties, accessed via the `C2PAService` object itself, and indicate where a manifest was found when returned from [getManifest](#getmanifest).

```javascript
const app = require("mediaencoder");
const MANIFEST_LOCATION_EMBEDDED = app.C2PAService.MANIFEST_LOCATION_EMBEDDED;
```

### MANIFEST_LOCATION_NONE

Content credentials NONE. No manifest found in the provided asset.

Type: _number_ (readonly)

Since: **26.5**

<HorizontalLine />

### MANIFEST_LOCATION_EMBEDDED

Content credentials EMBEDDED. An embedded manifest was found.

Type: _number_ (readonly)

Since: **26.5**

<HorizontalLine />

### MANIFEST_LOCATION_SIDE_CAR

Content credentials SIDE_CAR. A sidecar manifest was found.

Type: _number_ (readonly)

Since: **26.5**

<HorizontalLine />

### MANIFEST_LOCATION_CLOUD

Content credentials CLOUD. A reference to a cloud manifest was found.

Type: _number_ (readonly)

Since: **26.5**

<HorizontalLine />

## Methods

<HorizontalLine />

### getManifest

**Class method.** Returns an object with `manifest` (JSON string) and `manifestLocation` (number) indicating where the C2PA manifest was found. Location flags: [MANIFEST_LOCATION_NONE](#manifest_location_none) (0), [MANIFEST_LOCATION_EMBEDDED](#manifest_location_embedded) (1), [MANIFEST_LOCATION_SIDE_CAR](#manifest_location_side_car) (2), [MANIFEST_LOCATION_CLOUD](#manifest_location_cloud) (4). If `withValidation` is true, the file will be validated during processing.

Since: **26.5**

#### Parameters

| Name           | Type      | Description                                             |
| :------------- | :-------- | :------------------------------------------------------ |
| filePath       | _string_  | File path to the media file to read the manifest from   |
| withValidation | _boolean_ | If `true`, the file will be validated during processing |

#### Returns

| Name             | Type     | Description                                                              |
| :--------------- | :------- | :----------------------------------------------------------------------- |
| manifest         | _string_ | The C2PA manifest as a JSON string                                       |
| manifestLocation | _number_ | Where the manifest was found; one of the `MANIFEST_LOCATION_*` constants |

```javascript
const app = require("mediaencoder");
const result = app.C2PAService.getManifest("path/to/file.mp4", true);
result; // { manifest: "{...}", manifestLocation: 1 }
```

<HorizontalLine />
