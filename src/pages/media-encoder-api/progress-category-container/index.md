---
title: "ProgressCategoryContainer: Media Encoder API"
description: "Media Encoder's ProgressCategoryContainer API for accessing and managing progress categories and progress items."
id: progressCategoryContainer
title: ProgressCategoryContainer
sidebar_label: ProgressCategoryContainer
product: mediaencoder
keywords:
  - UXP
  - Adobe Media Encoder
  - Media Encoder API
  - progress
  - ProgressCategoryContainer
  - scripting automation


contributors:
  - https://github.com/justintaylor-dev
  - https://github.com/sukriyeLudwig
---

# ProgressCategoryContainer

<InlineAlert variant="info" slots="text"/>

UXP for Adobe Media Encoder is in public beta. This reference is being written, and the supported API surface may change before general availability.

Since: **26.5**

The Media Encoder `ProgressCategoryContainer` API provides access to progress categories, such as the global render progress exposed via [RenderQueue.PROGRESS_CATEGORY_ID](../render-queue/index.md#progresscategoryid). Use [getOrCreateProgressCategory](#getorcreateprogresscategory) to obtain a [ProgressCategory](./progress-category/index.md), and use that category to create and manage individual [ProgressItem](./progress-item/index.md) objects.

The `ProgressCategoryContainer` class can be accessed from the main app object. Call [getContainer](#getcontainer) to obtain the shared container instance:

```javascript
const app = require("mediaencoder");
const container = app.ProgressCategoryContainer.getContainer();
```

<HorizontalLine />

## Constants

These Constants are used as event IDs with [addEventListener](#addeventlistener) / [removeEventListener](#removeeventlistener) on a `ProgressCategoryContainer` instance. All Constants are class properties, accessed via the `ProgressCategoryContainer` object:

```javascript
const app = require("mediaencoder");
const EVENT_PROGRESS_CATEGORY_ADDED =
  app.ProgressCategoryContainer.EVENT_PROGRESS_CATEGORY_ADDED;
```

### EVENT_PROGRESS_CATEGORY_ADDED

Event ID fired when a new progress category is added. The event carries a `progressCategory` property.

Type: _string_

Since: **26.5**

<HorizontalLine />

### EVENT_PROGRESS_CATEGORY_REMOVED

Event ID fired when a progress category is removed. The event carries a `progressCategory` property.

Type: _string_

Since: **26.5**

<HorizontalLine />

### EVENT_PROGRESS_ITEM_ADDED

Event ID fired when a new progress item is added to a category. The event carries `progressCategory` and `progressItem` properties.

Type: _string_

Since: **26.5**

<HorizontalLine />

### EVENT_PROGRESS_ITEM_REMOVED

Event ID fired when a progress item is removed from a category. The event carries `progressCategory` and `progressItem` properties.

Type: _string_

Since: **26.5**

<HorizontalLine />

## Methods

### getContainer

**Class method.** Gets the shared instance of the `ProgressCategoryContainer` object.

Since: **26.5**

#### Parameters

none

#### Returns

| Name      | Type     | Description                          |
| :-------- | :------- | :-------------------------------------- |
| container | _object_ | A `ProgressCategoryContainer` instance |

```javascript
const app = require("mediaencoder");
const container = app.ProgressCategoryContainer.getContainer();
```

<HorizontalLine />

### getOrCreateProgressCategory

Gets an existing progress category by ID, or creates a new one if it doesn't already exist.

Since: **26.5**

#### Parameters

| Name        | Type                | Description                                            |
| :---------- | :------------------ | :--------------------------------------------------------- |
| inCategoryID | _string_            | The unique ID for the progress category                   |
| inTitle      | _string (optional)_ | The display title for the category, if it needs to be created |

#### Returns

[ProgressCategory](./progress-category/index.md)

```javascript
const app = require("mediaencoder");
const container = app.ProgressCategoryContainer.getContainer();
const category = container.getOrCreateProgressCategory(
  app.RenderQueue.PROGRESS_CATEGORY_ID,
  "My Category",
);
```

<HorizontalLine />

### getAllProgressCategories

Gets all currently registered progress categories.

Since: **26.5**

#### Parameters

none

#### Returns

| Name       | Type       | Description                          |
| :--------- | :--------- | :-------------------------------------- |
| categories | _object[]_ | Array of [ProgressCategory](./progress-category/index.md) objects |

```javascript
const app = require("mediaencoder");
const container = app.ProgressCategoryContainer.getContainer();
const categories = container.getAllProgressCategories();
```

<HorizontalLine />

### removeProgressCategory

Removes the specified progress category from the container.

Since: **26.5**

#### Parameters

| Name             | Type     | Description                                   |
| :---------------- | :------- | :------------------------------------------------ |
| inProgressCategory | _object_ | The [ProgressCategory](./progress-category/index.md) to remove |

#### Returns

| Name   | Type      | Description                          |
| :----- | :-------- | :-------------------------------------- |
| result | _boolean_ | `true` if the category was removed     |

```javascript
const app = require("mediaencoder");
const container = app.ProgressCategoryContainer.getContainer();
container.removeProgressCategory(category);
```

<HorizontalLine />

### getProgressItemFromReferenceID

Retrieves a progress item by its reference ID, across all categories in the container.

Since: **26.5**

#### Parameters

| Name          | Type     | Description                                                 |
| :------------ | :------- | :--------------------------------------------------------------- |
| referenceGuid | _object_ | The reference GUID the item was created with, see [createProgressItemWithReferenceId](./progress-category/index.md#createprogressitemwithreferenceid) |

#### Returns

[ProgressItem](./progress-item/index.md), or `null` if there is no progress item under this reference ID.

```javascript
const app = require("mediaencoder");
const container = app.ProgressCategoryContainer.getContainer();
const item = container.getProgressItemFromReferenceID(referenceGuid);
```

<HorizontalLine />

### subscribeToEvent

Registers a subscription to a specific container-level event.

_Note: addEventListener() is required after a subscribeToEvent() call in order to actually react to an event, the same pattern used by [RenderQueueInstance](../render-queue/render-queue-instance/index.md#subscribetoevent)._

Since: **26.5**

#### Parameters

| Name     | Type     | Description                                                                                                                                          |
| :------- | :------- | :--------------------------------------------------------------------------------------------------------------------------------------------------- |
| eventKey | _string_ | The event ID to subscribe to, one of [EVENT_PROGRESS_CATEGORY_ADDED](#eventprogresscategoryadded), [EVENT_PROGRESS_CATEGORY_REMOVED](#eventprogresscategoryremoved), [EVENT_PROGRESS_ITEM_ADDED](#eventprogressitemadded), [EVENT_PROGRESS_ITEM_REMOVED](#eventprogressitemremoved) |

#### Returns

| Name    | Type      | Description                                   |
| :------ | :-------- | :-------------------------------------------- |
| success | _boolean_ | Returns `true` if subscription was successful |

```javascript
const app = require("mediaencoder");
const container = app.ProgressCategoryContainer.getContainer();
const event = app.ProgressCategoryContainer.EVENT_PROGRESS_CATEGORY_ADDED;
container.subscribeToEvent(event); // true
const callback = (event) => {
  console.log("Progress category added", event.progressCategory);
};
container.addEventListener(event, callback);
```

<HorizontalLine />

### addEventListener

Registers an event handler for the specified event on this `ProgressCategoryContainer`. The event handling follows the W3C DOM Level 2 Events Specification.

Since: **26.5**

#### Parameters

| Name      | Type       | Description                                                 |
| :-------- | :--------- | :--------------------------------------------------------------- |
| eventType | _string_   | The event ID to listen for, see [Constants](#constants)          |
| handler   | _function_ | A function to be triggered when the specified event occurs       |

#### Returns

none

```javascript
const app = require("mediaencoder");
const container = app.ProgressCategoryContainer.getContainer();
const event = app.ProgressCategoryContainer.EVENT_PROGRESS_CATEGORY_ADDED;
container.subscribeToEvent(event);
const callback = (event) => {
  console.log("Progress category added", event.progressCategory);
};
container.addEventListener(event, callback);
```

<HorizontalLine />

### removeEventListener

Unregisters a previously registered event handler for the specified event on this `ProgressCategoryContainer`.

Since: **26.5**

#### Parameters

| Name      | Type       | Description                            |
| :-------- | :--------- | :----------------------------------------- |
| eventType | _string_   | The event ID to stop listening for        |
| handler   | _function_ | The previously registered callback to remove |

#### Returns

none

```javascript
const app = require("mediaencoder");
const container = app.ProgressCategoryContainer.getContainer();
const event = app.ProgressCategoryContainer.EVENT_PROGRESS_CATEGORY_ADDED;
container.removeEventListener(event, callback);
```

<HorizontalLine />

### hasDoneJobs

Checks whether any progress category in the container has completed jobs.

Since: **26.5**

#### Parameters

none

#### Returns

| Name   | Type      | Description                             |
| :----- | :-------- | :------------------------------------------ |
| result | _boolean_ | `true` if there are completed jobs         |

```javascript
const app = require("mediaencoder");
const container = app.ProgressCategoryContainer.getContainer();
container.hasDoneJobs();
```

<HorizontalLine />

### removeDoneJobs

Removes completed progress items across all progress categories in the container.

Since: **26.5**

#### Parameters

none

#### Returns

| Name   | Type      | Description                    |
| :----- | :-------- | :---------------------------------- |
| result | _boolean_ | `true` on success                  |

```javascript
const app = require("mediaencoder");
const container = app.ProgressCategoryContainer.getContainer();
container.removeDoneJobs();
```

<HorizontalLine />

### pauseAllProgressItems

Pauses all progress items across all progress categories in the container.

Since: **26.5**

#### Parameters

none

#### Returns

| Name   | Type      | Description         |
| :----- | :-------- | :---------------------- |
| result | _boolean_ | `true` on success       |

```javascript
const app = require("mediaencoder");
const container = app.ProgressCategoryContainer.getContainer();
await container.pauseAllProgressItems();
```

<HorizontalLine />

### resumeAllProgressItems

Resumes all paused progress items across all progress categories in the container.

Since: **26.5**

#### Parameters

none

#### Returns

| Name   | Type      | Description        |
| :----- | :-------- | :--------------------- |
| result | _boolean_ | `true` on success      |

```javascript
const app = require("mediaencoder");
const container = app.ProgressCategoryContainer.getContainer();
await container.resumeAllProgressItems();
```

<HorizontalLine />
