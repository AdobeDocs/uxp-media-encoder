---
title: "ProgressItem: Media Encoder API"
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


contributors:
  - https://github.com/justintaylor-dev
  - https://github.com/sukriyeLudwig
---

# ProgressItem

<InlineAlert variant="info" slots="text"/>

UXP for Adobe Media Encoder is in public beta. This reference is being written, and the supported API surface may change before general availability.

Since: **26.5**

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

Since: **26.5**

<HorizontalLine />

### PROGRESS_STATE_PAUSED

Paused progress state.

Type: _number_ (readonly, class)

Since: **26.5**

<HorizontalLine />

### PROGRESS_STATE_RESUMED

Resumed progress state.

Type: _number_ (readonly, class)

Since: **26.5**

<HorizontalLine />

### PROGRESS_STATE_WAITING

Waiting progress state.

Type: _number_ (readonly, class)

Since: **26.5**

<HorizontalLine />

### PROGRESS_STATE_FAILED

Failed progress state.

Type: _number_ (readonly, class)

Since: **26.5**

<HorizontalLine />

### PROGRESS_STATE_CANCELLED

Cancelled progress state.

Type: _number_ (readonly, class)

Since: **26.5**

<HorizontalLine />

### EVENT_PROGRESS_ITEM_VALUE_CHANGED

Event ID fired when the progress item's value changes. The event carries `progressItem`, `status`, and `value` properties.

Type: _string_ (readonly, class)

Since: **26.5**

<HorizontalLine />

### EVENT_PROGRESS_ITEM_CANCELLED

Event ID fired when the progress item is cancelled. The event carries a `progressItem` property.

Type: _string_ (readonly, class)

Since: **26.5**

<HorizontalLine />

### EVENT_PROGRESS_ITEM_TITLE_CHANGED

Event ID fired when the progress item's title changes. The event carries `progressItem` and `title` properties.

Type: _string_ (readonly, class)

Since: **26.5**

<HorizontalLine />

## Properties

### referenceId

The reference ID the item was created with, if any.

Type: _object_ (readonly)

Since: **26.5**

<HorizontalLine />

### creationTime

The time the progress item was created.

Type: _string_ (readonly)

Since: **26.5**

<HorizontalLine />

## Methods

### getValue

Gets the current progress value.

Since: **26.5**

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

Since: **26.5**

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

Since: **26.5**

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

Since: **26.5**

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

Since: **26.5**

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

Since: **26.5**

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

Since: **26.5**

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

Since: **26.5**

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

Since: **26.5**

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

Since: **26.5**

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

Since: **26.5**

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

Since: **26.5**

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

Since: **26.5**

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

Since: **26.5**

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

Since: **26.5**

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

Since: **26.5**

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

Since: **26.5**

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

Since: **26.5**

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

Since: **26.5**

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

Since: **26.5**

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

Since: **26.5**

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

### subscribeToEvent

Registers a subscription to a specific event on this progress item.

_Note: addEventListener() is required after a subscribeToEvent() call in order to actually react to an event, the same pattern used by [RenderQueueInstance](../../render-queue/render-queue-instance/index.md#subscribetoevent)._

Since: **26.5**

#### Parameters

| Name     | Type     | Description                                                                                                                                     |
| :------- | :------- | :------------------------------------------------------------------------------------------------------------------------------------------------- |
| eventKey | _string_ | The event ID to subscribe to, one of [EVENT_PROGRESS_ITEM_VALUE_CHANGED](#eventprogressitemvaluechanged), [EVENT_PROGRESS_ITEM_CANCELLED](#eventprogressitemcancelled), [EVENT_PROGRESS_ITEM_TITLE_CHANGED](#eventprogressitemtitlechanged) |

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
