---
title: Guid Media Encoder API
description: "Create Guid objects from GUID strings and convert them back to strings with the Media Encoder Guid API in UXP, for example to set the type of a progress item."
id: guid
sidebar_label: Guid
product: mediaencoder
keywords:
  - UXP
  - Adobe Media Encoder
  - Media Encoder API
  - Guid
  - GUID
  - unique identifier
  - fromString
  - toString
  - setType


contributors:
  - https://github.com/sukriyeLudwig
---

# Guid

<InlineAlert variant="info" slots="text"/>

UXP for Adobe Media Encoder is in public beta. This reference is being written, and the supported API surface may change before general availability.

Since: **27.0**

A `Guid` object holds a globally unique identifier (GUID). Most Media Encoder APIs pass GUIDs as strings, such as job IDs, but the progress APIs listed below use `Guid` objects.

Create a `Guid` from a string with the class method [fromString](#fromstring), and convert it back to a string with the instance method [toString](#tostring):

```javascript
const app = require("mediaencoder");
const guid = app.Guid.fromString("6f1c2b7e-3d4a-4f5b-9c8d-1e2f3a4b5c6d");
guid.toString(); // "6f1c2b7e-3d4a-4f5b-9c8d-1e2f3a4b5c6d"
```

These APIs take or return a `Guid`:

| API                                                                                                                                   | Use of the `Guid`                                 |
| :------------------------------------------------------------------------------------------------------------------------------------ | :------------------------------------------------ |
| [ProgressCategory.createProgressItemWithReferenceId](../progress-category-container/progress-category/index.md#createprogressitemwithreferenceid) | The reference ID of the new progress item         |
| [ProgressCategory.getProgressItemFromReferenceID](../progress-category-container/progress-category/index.md#getprogressitemfromreferenceid) | The reference ID to look up in the category       |
| [ProgressCategoryContainer.getProgressItemFromReferenceID](../progress-category-container/index.md#getprogressitemfromreferenceid) | The reference ID to look up in all categories     |
| [ProgressItem.referenceId](../progress-category-container/progress-item/index.md#referenceid)                                         | Returns the reference ID of the progress item     |
| [ProgressItem.setType](../progress-category-container/progress-item/index.md#settype)                                                 | The type of the progress item                     |

<HorizontalLine />

## Methods

### fromString

Creates a `Guid` object from the string representation of a GUID. Call this class method on `app.Guid`.

Since: **27.0**

#### Parameters

| Name        | Type     | Description                                                 |
| :---------- | :------- | :---------------------------------------------------------- |
| stringValue | _string_ | The GUID as a string, such as `"6f1c2b7e-3d4a-4f5b-9c8d-1e2f3a4b5c6d"` |

#### Returns

[Guid](#guid)

```javascript
const app = require("mediaencoder");
const guid = app.Guid.fromString("6f1c2b7e-3d4a-4f5b-9c8d-1e2f3a4b5c6d");
```

<HorizontalLine />

### toString

Returns the string representation of the GUID. Call this instance method on a `Guid` object.

Since: **27.0**

#### Parameters

none

#### Returns

| Name  | Type     | Description           |
| :---- | :------- | :-------------------- |
| value | _string_ | The GUID as a string  |

```javascript
const app = require("mediaencoder");
const guid = app.Guid.fromString("6f1c2b7e-3d4a-4f5b-9c8d-1e2f3a4b5c6d");
guid.toString(); // "6f1c2b7e-3d4a-4f5b-9c8d-1e2f3a4b5c6d"
```

<HorizontalLine />
