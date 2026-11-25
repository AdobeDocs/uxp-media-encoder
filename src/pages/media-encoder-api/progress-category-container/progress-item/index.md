---
title: ProgressItem Media Encoder API
description: "Media Encoder's ProgressItem API for reading and updating an individual progress item's value, status, and state."
id: progressItem
title: ProgressItem
sidebar_label: ProgressItem
product: mediaencoder
keywords:
  - UXP
  - Adobe Media Encoder
  - Media Encoder API
  - progress
  - ProgressItem
  - scripting automation
  - setType


contributors:
  - https://github.com/justintaylor-dev
  - https://github.com/sukriyeLudwig
---

# ProgressItem

<InlineAlert variant="info" slots="text"/>

UXP for Adobe Media Encoder is in public beta. This reference is being written, and the supported API surface may change before general availability.

Since: **27.0**

A `ProgressItem` represents a single item of progress within a [ProgressCategory](../progress-category/index.md), such as one render job's progress within the global render category. `ProgressItem` instances are not constructed directly; obtain one from [ProgressCategory.createProgressItem](../progress-category/index.md#createprogressitem), [createProgressItemWithReferenceId](../progress-category/index.md#createprogressitemwithreferenceid), or [getProgressItemFromReferenceID](../index.md#getprogressitemfromreferenceid).

```javascript
const app = require("mediaencoder");
const item = category.createProgressItem("Encoding job 1");
```

<HorizontalLine />

## Constants

### PROGRESS_STATE_NORMAL

Normal progress state. Returned by [getProgressState](#getprogressstate) and accepted by [setProgressState](#setprogressstate) / [pauseOrResumeProgress](#pauseorresumeprogress).

Type: _number_ (readonly, class)

Since: **27.0**

<HorizontalLine />

### PROGRESS_STATE_PAUSED

Paused progress state.

Type: _number_ (readonly, class)

Since: **27.0**

<HorizontalLine />

### PROGRESS_STATE_RESUMED

Resumed progress state.

Type: _number_ (readonly, class)

Since: **27.0**

<HorizontalLine />

### PROGRESS_STATE_WAITING

Waiting progress state.

Type: _number_ (readonly, class)

Since: **27.0**

<HorizontalLine />

### PROGRESS_STATE_FAILED

Failed progress state.

Type: _number_ (readonly, class)

Since: **27.0**

<HorizontalLine />

### PROGRESS_STATE_CANCELLED

Cancelled progress state.

Type: _number_ (readonly, class)

Since: **27.0**

<HorizontalLine />

### EVENT_PROGRESS_ITEM_VALUE_CHANGED

Event ID fired when the progress item's value changes. The listener receives a `ProgressItemValueChangedEvent` object with the following properties:

| Name         | Type                       | Description                                                                                         |
| :----------- | :------------------------- | :-------------------------------------------------------------------------------------------------- |
| progressItem | [ProgressItem](./index.md) | The progress item whose value changed                                                            |
| status       | _string_                   | The status message of the progress item                                                             |
| value        | _string_                   | The new progress value as a string. Convert it with `Number(event.value)` and compare it with [getMaxValue](#getmaxvalue) |

Type: _string_ (readonly, class)

Since: **27.0**

<HorizontalLine />

### EVENT_PROGRESS_ITEM_CANCELLED

Event ID fired when the progress item is cancelled. The listener receives a `ProgressItemCancelledEvent` object with the following property:

| Name         | Type                          | Description                          |
| :----------- | :---------------------------- | :----------------------------------- |
| progressItem | [ProgressItem](./index.md) | The progress item that was cancelled |

Type: _string_ (readonly, class)

Since: **27.0**

<HorizontalLine />

### EVENT_PROGRESS_ITEM_TITLE_CHANGED

Event ID fired when the progress item's title changes. The listener receives a `ProgressItemTitleChangedEvent` object with the following properties:

| Name         | Type                          | Description                              |
| :----------- | :---------------------------- | :--------------------------------------- |
| progressItem | [ProgressItem](./index.md) | The progress item whose title changed    |
| title        | _string_                      | The new title                            |

Type: _string_ (readonly, class)

Since: **27.0**

<HorizontalLine />

## Properties

### referenceId

The reference ID of the progress item. For an item created with [createProgressItemWithReferenceId](../progress-category/index.md#createprogressitemwithreferenceid), this is the reference ID you passed. Otherwise, Media Encoder generates a unique ID. If the progress item no longer exists, this is the all-zero GUID `00000000-0000-0000-0000-000000000000`.

Type: [Guid](../../guid/index.md) (readonly)

Since: **27.0**

<HorizontalLine />

### creationTime

The time the progress item was created.

Type: _string_ (readonly)

Since: **27.0**

<HorizontalLine />

## Methods

### getValue

Gets the current progress value.

Since: **27.0**

#### Parameters

none

#### Returns

| Name  | Type     | Description             |
| :---- | :------- | :--------------------------- |
| value | _number_ | The current progress value  |

```javascript
const app = require("mediaencoder");
item.getValue();
```

<HorizontalLine />

### getMaxValue

Gets the maximum progress value.

Since: **27.0**

#### Parameters

none

#### Returns

| Name     | Type     | Description               |
| :------- | :------- | :---------------------------- |
| maxValue | _number_ | The maximum progress value   |

```javascript
const app = require("mediaencoder");
item.getMaxValue();
```

<HorizontalLine />

### getStatusMessage

Gets the current status message.

Since: **27.0**

#### Parameters

none

#### Returns

| Name          | Type     | Description         |
| :------------ | :------- | :--------------------- |
| statusMessage | _string_ | The current status message |

```javascript
const app = require("mediaencoder");
item.getStatusMessage();
```

<HorizontalLine />

### getTitle

Gets the title of the progress item.

Since: **27.0**

#### Parameters

none

#### Returns

| Name  | Type     | Description               |
| :---- | :------- | :---------------------------- |
| title | _string_ | The title of the progress item |

```javascript
const app = require("mediaencoder");
item.getTitle();
```

<HorizontalLine />

### getProgressState

Gets the current progress state.

Since: **27.0**

#### Parameters

none

#### Returns

| Name  | Type     | Description                                                     |
| :---- | :------- | :---------------------------------------------------------------- |
| state | _number_ | One of the `PROGRESS_STATE_*` constants                          |

```javascript
const app = require("mediaencoder");
item.getProgressState();
```

<HorizontalLine />

### isComplete

Checks whether the progress item is complete.

Since: **27.0**

#### Parameters

none

#### Returns

| Name   | Type      | Description                     |
| :----- | :-------- | :----------------------------------- |
| result | _boolean_ | `true` if the item is complete       |

```javascript
const app = require("mediaencoder");
item.isComplete();
```

<HorizontalLine />

### isInProgress

Checks whether the progress item is currently in progress.

Since: **27.0**

#### Parameters

none

#### Returns

| Name   | Type      | Description                       |
| :----- | :-------- | :------------------------------------- |
| result | _boolean_ | `true` if the item is in progress      |

```javascript
const app = require("mediaencoder");
item.isInProgress();
```

<HorizontalLine />

### isIndeterminateProgress

Checks whether the progress item has been configured as unknown (indeterminate) progress.

Since: **27.0**

#### Parameters

none

#### Returns

| Name   | Type      | Description                            |
| :----- | :-------- | :------------------------------------------ |
| result | _boolean_ | `true` if the item reports unknown progress |

```javascript
const app = require("mediaencoder");
item.isIndeterminateProgress();
```

<HorizontalLine />

### isPending

Checks whether the progress item is pending.

Since: **27.0**

#### Parameters

none

#### Returns

| Name   | Type      | Description                   |
| :----- | :-------- | :---------------------------------- |
| result | _boolean_ | `true` if the item is pending       |

```javascript
const app = require("mediaencoder");
item.isPending();
```

<HorizontalLine />

### supportsCancellation

Checks if the progress item can be cancelled.

Since: **27.0**

#### Parameters

none

#### Returns

| Name   | Type      | Description                                 |
| :----- | :-------- | :------------------------------------------------ |
| result | _boolean_ | `true` if the item supports cancellation           |

```javascript
const app = require("mediaencoder");
item.supportsCancellation();
```

<HorizontalLine />

### supportsPauseAndResume

Checks if the progress item can be paused and resumed.

Since: **27.0**

#### Parameters

none

#### Returns

| Name   | Type      | Description                                    |
| :----- | :-------- | :--------------------------------------------------- |
| result | _boolean_ | `true` if the item supports pause and resume          |

```javascript
const app = require("mediaencoder");
item.supportsPauseAndResume();
```

<HorizontalLine />

### cancelProgress

Cancels this progress item.

Since: **27.0**

#### Parameters

none

#### Returns

| Name   | Type      | Description       |
| :----- | :-------- | :--------------------- |
| result | _boolean_ | `true` on success      |

```javascript
const app = require("mediaencoder");
await item.cancelProgress();
```

<HorizontalLine />

### pauseOrResumeProgress

Pauses or resumes this progress item.

Since: **27.0**

#### Parameters

| Name           | Type     | Description                                              |
| :-------------- | :------- | :------------------------------------------------------------ |
| inProgresState | _number_ | One of `PROGRESS_STATE_PAUSED` / `PROGRESS_STATE_RESUMED`     |

#### Returns

| Name   | Type      | Description       |
| :----- | :-------- | :--------------------- |
| result | _boolean_ | `true` on success      |

```javascript
const app = require("mediaencoder");
await item.pauseOrResumeProgress(app.ProgressItem.PROGRESS_STATE_PAUSED);
```

<HorizontalLine />

### setProgressStatus

Sets the current progress value and max value.

Since: **27.0**

#### Parameters

| Name     | Type     | Description             |
| :------- | :------- | :---------------------------- |
| value    | _number_ | The current progress value    |
| maxValue | _number_ | The maximum progress value    |

#### Returns

| Name   | Type      | Description       |
| :----- | :-------- | :--------------------- |
| result | _boolean_ | `true` on success      |

```javascript
const app = require("mediaencoder");
await item.setProgressStatus(50, 100);
```

<HorizontalLine />

### setProgressStatusAndToolTip

Sets the current progress value, max value, status message, and tooltip.

Since: **27.0**

#### Parameters

| Name          | Type     | Description             |
| :------------ | :------- | :---------------------------- |
| value         | _number_ | The current progress value    |
| maxValue      | _number_ | The maximum progress value    |
| statusMessage | _string_ | The status message to display |
| toolTip       | _string_ | The tooltip to display        |

#### Returns

| Name   | Type      | Description       |
| :----- | :-------- | :--------------------- |
| result | _boolean_ | `true` on success      |

```javascript
const app = require("mediaencoder");
await item.setProgressStatusAndToolTip(50, 100, "Encoding...", "Job 1 of 4");
```

<HorizontalLine />

### setUnknownProgress

Marks the progress item as having unknown (indeterminate) progress.

Since: **27.0**

#### Parameters

| Name          | Type     | Description         |
| :------------ | :------- | :--------------------- |
| statusMessage | _string_ | The status message to display |

#### Returns

| Name   | Type      | Description       |
| :----- | :-------- | :--------------------- |
| result | _boolean_ | `true` on success      |

```javascript
const app = require("mediaencoder");
await item.setUnknownProgress("Analyzing...");
```

<HorizontalLine />

### setToolTip

Sets the tooltip for the progress item.

Since: **27.0**

#### Parameters

| Name    | Type     | Description        |
| :------ | :------- | :---------------------- |
| toolTip | _string_ | The tooltip to display  |

#### Returns

| Name   | Type      | Description       |
| :----- | :-------- | :--------------------- |
| result | _boolean_ | `true` on success      |

```javascript
const app = require("mediaencoder");
await item.setToolTip("Job 1 of 4");
```

<HorizontalLine />

### setStatusMessage

Sets the status message for the progress item.

Since: **27.0**

#### Parameters

| Name          | Type     | Description         |
| :------------ | :------- | :--------------------- |
| statusMessage | _string_ | The status message to display |

#### Returns

| Name   | Type      | Description       |
| :----- | :-------- | :--------------------- |
| result | _boolean_ | `true` on success      |

```javascript
const app = require("mediaencoder");
await item.setStatusMessage("Encoding...");
```

<HorizontalLine />

### setTitle

Sets the title of the progress item.

Since: **27.0**

#### Parameters

| Name  | Type     | Description         |
| :---- | :------- | :---------------------- |
| title | _string_ | The new title to set    |

#### Returns

| Name   | Type      | Description       |
| :----- | :-------- | :--------------------- |
| result | _boolean_ | `true` on success      |

```javascript
const app = require("mediaencoder");
await item.setTitle("Encoding job 1 (retry)");
```

<HorizontalLine />

### setProgressState

Sets the progress state.

Since: **27.0**

#### Parameters

| Name  | Type     | Description                             |
| :---- | :------- | :------------------------------------------ |
| state | _number_ | One of the `PROGRESS_STATE_*` constants     |

#### Returns

| Name   | Type      | Description       |
| :----- | :-------- | :--------------------- |
| result | _boolean_ | `true` on success      |

```javascript
const app = require("mediaencoder");
await item.setProgressState(app.ProgressItem.PROGRESS_STATE_CANCELLED);
```

<HorizontalLine />

### setCancelToolTip

Sets the tooltip shown for the cancel action on this progress item.

Since: **27.0**

#### Parameters

| Name    | Type     | Description                    |
| :------ | :------- | :---------------------------------- |
| toolTip | _string_ | The tooltip to display for cancel  |

#### Returns

| Name   | Type      | Description       |
| :----- | :-------- | :--------------------- |
| result | _boolean_ | `true` on success      |

```javascript
const app = require("mediaencoder");
await item.setCancelToolTip("Cancel this job");
```

<HorizontalLine />

### setType

Sets the type of the progress item. The type is a GUID that your plugin defines, so that you can tell your own kinds of progress items apart.

Since: **27.0**

#### Parameters

| Name | Type                         | Description                                                                                      |
| :--- | :--------------------------- | :----------------------------------------------------------------------------------------------- |
| type | [Guid](../../guid/index.md) | The type of the progress item, created with [Guid.fromString](../../guid/index.md#fromstring)   |

#### Returns

| Name    | Type      | Description                                                                 |
| :------ | :-------- | :-------------------------------------------------------------------------- |
| success | _boolean_ | Returns `true` if the type was set, `false` if the progress item no longer exists |

```javascript
const app = require("mediaencoder");
const item = category.createProgressItem("Uploading renders");
await item.setType(app.Guid.fromString("6f1c2b7e-3d4a-4f5b-9c8d-1e2f3a4b5c6d")); // true
```

<HorizontalLine />

### subscribeToEvent

Registers a subscription to a specific event on this progress item.

_Note: addEventListener() is required after a subscribeToEvent() call in order to actually react to an event, the same pattern used by [RenderQueueInstance](../../render-queue/render-queue-instance/index.md#subscribetoevent)._

Since: **27.0**

#### Parameters

| Name     | Type     | Description                                                                                                                                     |
| :------- | :------- | :------------------------------------------------------------------------------------------------------------------------------------------------- |
| eventKey | _string_ | The event ID to subscribe to, one of [EVENT_PROGRESS_ITEM_VALUE_CHANGED](#event_progress_item_value_changed), [EVENT_PROGRESS_ITEM_CANCELLED](#event_progress_item_cancelled), [EVENT_PROGRESS_ITEM_TITLE_CHANGED](#event_progress_item_title_changed) |

#### Returns

| Name    | Type      | Description                                   |
| :------ | :-------- | :-------------------------------------------- |
| success | _boolean_ | Returns `true` if subscription was successful |

```javascript
const app = require("mediaencoder");
const event = app.ProgressItem.EVENT_PROGRESS_ITEM_VALUE_CHANGED;
item.subscribeToEvent(event); // true
const callback = (event) => {
  console.log("Progress value changed", event.value);
};
item.addEventListener(event, callback);
```

<HorizontalLine />
