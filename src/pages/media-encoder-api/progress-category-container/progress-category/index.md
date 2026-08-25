---
title: "ProgressCategory: Media Encoder API"
description: "Media Encoder's ProgressCategory API for managing a category of progress items."
id: progressCategory
title: ProgressCategory
sidebar_label: ProgressCategory
product: mediaencoder
keywords:
  - UXP
  - Adobe Media Encoder
  - Media Encoder API
  - progress
  - ProgressCategory
  - scripting automation


contributors:
  - https://github.com/justintaylor-dev
  - https://github.com/sukriyeLudwig
---

# ProgressCategory

<InlineAlert variant="info" slots="text"/>

UXP for Adobe Media Encoder is in public beta. This reference is being written, and the supported API surface may change before general availability.

Since: **26.5**

A `ProgressCategory` represents a category of progress items, such as the global render progress category. `ProgressCategory` instances are not constructed directly; obtain one from [ProgressCategoryContainer.getOrCreateProgressCategory](../index.md#getorcreateprogresscategory) or [getAllProgressCategories](../index.md#getallprogresscategories).

```javascript
const app = require("mediaencoder");
const container = app.ProgressCategoryContainer.getContainer();
const category = container.getOrCreateProgressCategory(
  app.RenderQueue.PROGRESS_CATEGORY_ID,
  "My Category",
);
```

<HorizontalLine />

## Properties

### id

The unique category ID.

Type: _string_ (readonly)

Since: **26.5**

<HorizontalLine />

## Methods

### createProgressItem

Creates a new [ProgressItem](../progress-item/index.md) with the given title.

Since: **26.5**

#### Parameters

| Name  | Type     | Description                     |
| :---- | :------- | :---------------------------------- |
| title | _string_ | The title for the new progress item |

#### Returns

[ProgressItem](../progress-item/index.md), or `null` if the category is no longer valid.

```javascript
const app = require("mediaencoder");
const item = category.createProgressItem("Encoding job 1");
```

<HorizontalLine />

### createProgressItemWithReferenceId

Creates a new [ProgressItem](../progress-item/index.md) with the given title and reference ID, so it can be looked up later via [getProgressItemFromReferenceID](#getprogressitemfromreferenceid).

Since: **26.5**

#### Parameters

| Name        | Type     | Description                                |
| :----------- | :------- | :---------------------------------------------- |
| title       | _string_ | The title for the new progress item             |
| referenceId | _object_ | A GUID object used to look the item up later    |

#### Returns

[ProgressItem](../progress-item/index.md), or `null` if the category is no longer valid.

```javascript
const app = require("mediaencoder");
const item = category.createProgressItemWithReferenceId(
  "Encoding job 1",
  referenceGuid,
);
```

<HorizontalLine />

### getProgressItems

Gets all the progress items in this progress category.

Since: **26.5**

#### Parameters

none

#### Returns

| Name  | Type       | Description                                       |
| :---- | :--------- | :----------------------------------------------------- |
| items | _object[]_ | Array of [ProgressItem](../progress-item/index.md) objects |

```javascript
const app = require("mediaencoder");
const items = category.getProgressItems();
```

<HorizontalLine />

### getProgressItemFromReferenceID

Retrieves a progress item by its reference ID.

Since: **26.5**

#### Parameters

| Name          | Type     | Description                             |
| :------------ | :------- | :----------------------------------------- |
| referenceGuid | _object_ | The reference GUID the item was created with |

#### Returns

[ProgressItem](../progress-item/index.md), or `null` if there is no progress item under this reference ID.

```javascript
const app = require("mediaencoder");
const item = category.getProgressItemFromReferenceID(referenceGuid);
```

<HorizontalLine />

### getOverallProgressItem

Gets a progress item that represents all the progress in this category, encapsulated as a single item.

Since: **26.5**

#### Parameters

none

#### Returns

[ProgressItem](../progress-item/index.md)

```javascript
const app = require("mediaencoder");
const overall = category.getOverallProgressItem();
```

<HorizontalLine />

### getTitle

Gets the title of the progress category.

Since: **26.5**

#### Parameters

none

#### Returns

| Name  | Type     | Description                                                |
| :---- | :------- | :---------------------------------------------------------------- |
| title | _string_ | The category title, or an empty string if the category is no longer valid |

```javascript
const app = require("mediaencoder");
category.getTitle();
```

<HorizontalLine />

### getTotalJobs

Counts all progress items registered in this category.

Since: **26.5**

#### Parameters

none

#### Returns

| Name  | Type     | Description                        |
| :---- | :------- | :-------------------------------------- |
| total | _number_ | The total number of progress items     |

```javascript
const app = require("mediaencoder");
category.getTotalJobs();
```

<HorizontalLine />

### getValue

Gets the cumulative progress value of the progress category.

Since: **26.5**

#### Parameters

none

#### Returns

| Name  | Type     | Description               |
| :---- | :------- | :---------------------------- |
| value | _number_ | The cumulative progress value |

```javascript
const app = require("mediaencoder");
category.getValue();
```

<HorizontalLine />

### getIcon

Gets the icon of the progress category as a base64-encoded SVG.

Since: **26.5**

#### Parameters

none

#### Returns

| Name | Type     | Description                                                   |
| :--- | :------- | :------------------------------------------------------------------ |
| icon | _string_ | The base64-encoded SVG string, or an empty string if none          |

```javascript
const app = require("mediaencoder");
category.getIcon();
```

<HorizontalLine />

### hasPendingJobs

Checks if the progress category has any pending jobs.

Since: **26.5**

#### Parameters

none

#### Returns

| Name   | Type      | Description                 |
| :----- | :-------- | :------------------------------ |
| result | _boolean_ | `true` if there are pending jobs |

```javascript
const app = require("mediaencoder");
category.hasPendingJobs();
```

<HorizontalLine />

### hasDoneJobs

Checks if the progress category has any completed progress items.

Since: **26.5**

#### Parameters

none

#### Returns

| Name   | Type      | Description                  |
| :----- | :-------- | :-------------------------------- |
| result | _boolean_ | `true` if there are completed jobs |

```javascript
const app = require("mediaencoder");
category.hasDoneJobs();
```

<HorizontalLine />

### isIndeterminateProgress

Checks whether the progress category has a progress item that has been configured as unknown (indeterminate) progress.

Since: **26.5**

#### Parameters

none

#### Returns

| Name   | Type      | Description                                    |
| :----- | :-------- | :------------------------------------------------- |
| result | _boolean_ | `true` if all jobs report unknown progress         |

```javascript
const app = require("mediaencoder");
category.isIndeterminateProgress();
```

<HorizontalLine />

### supportsCancellation

Checks if the progress category can be cancelled.

Since: **26.5**

#### Parameters

none

#### Returns

| Name   | Type      | Description                             |
| :----- | :-------- | :------------------------------------------- |
| result | _boolean_ | `true` if the category supports cancellation |

```javascript
const app = require("mediaencoder");
category.supportsCancellation();
```

<HorizontalLine />

### cancelProgress

Cancels all jobs being reported under this progress category.

Since: **26.5**

#### Parameters

none

#### Returns

| Name   | Type      | Description       |
| :----- | :-------- | :--------------------- |
| result | _boolean_ | `true` on success      |

```javascript
const app = require("mediaencoder");
await category.cancelProgress();
```

<HorizontalLine />

### removeDoneJobs

Removes the completed progress items from the progress category.

Since: **26.5**

#### Parameters

none

#### Returns

| Name   | Type      | Description       |
| :----- | :-------- | :--------------------- |
| result | _boolean_ | `true` on success      |

```javascript
const app = require("mediaencoder");
category.removeDoneJobs();
```

<HorizontalLine />

### removeCancelledJobs

Removes the cancelled and failed progress items from the progress category.

Since: **26.5**

#### Parameters

none

#### Returns

| Name   | Type      | Description       |
| :----- | :-------- | :--------------------- |
| result | _boolean_ | `true` on success      |

```javascript
const app = require("mediaencoder");
category.removeCancelledJobs();
```

<HorizontalLine />

### removeProgressItem

Removes the specified progress item from the progress category.

Since: **26.5**

#### Parameters

| Name            | Type     | Description                              |
| :--------------- | :------- | :--------------------------------------------- |
| inProgressItem  | _object_ | The [ProgressItem](../progress-item/index.md) to remove |

#### Returns

| Name   | Type      | Description                  |
| :----- | :-------- | :------------------------------- |
| result | _boolean_ | `true` if the item was removed   |

```javascript
const app = require("mediaencoder");
category.removeProgressItem(item);
```

<HorizontalLine />

### showOnlyStatusColumn

Indicates that this progress category will only show the status column.

Since: **26.5**

#### Parameters

none

#### Returns

| Name   | Type      | Description                                                    |
| :----- | :-------- | :------------------------------------------------------------------ |
| result | _boolean_ | `true` if the category is configured to show only the status column |

```javascript
const app = require("mediaencoder");
category.showOnlyStatusColumn();
```

<HorizontalLine />

### showInHeaderBar

Indicates that this progress category will be shown in the header bar progress panel.

Since: **26.5**

#### Parameters

none

#### Returns

| Name   | Type      | Description                                  |
| :----- | :-------- | :------------------------------------------------ |
| result | _boolean_ | `true` if the category is shown in the header bar |

```javascript
const app = require("mediaencoder");
category.showInHeaderBar();
```

<HorizontalLine />
