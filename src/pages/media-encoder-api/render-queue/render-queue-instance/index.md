---
title: "Render Queue Instance: Media Encoder API"
description: "Media Encoder's Queue Instance APIs for adding, modifying, and enquing items for render."
id: renderQueueInstance
title: RenderQueueInstance
sidebar_label: RenderQueueInstance
product: mediaencoder
keywords:
  - UXP
  - Adobe Media Encoder
  - Media Encoder API
  - encoding queue
  - presets
  - jobs
  - scripting automation


contributors:
  - https://github.com/justintaylor-dev
  - https://github.com/sukriyeLudwig
---

# Render Queue Instance

The Media Encoder Queue Instance API is the used for up to date methods on the Render Queue.

<InlineAlert variant="info" slots="text"/>

UXP for Adobe Media Encoder is in public beta. This reference is being written, and the supported API surface may change before general availability.

<HorizontalLine />

### getStatus

Provides the current status of the rendering queue, represented as an enumeration.

The possible states are: Stopped = 0, Paused = 1, Running = 2, Stopping = 3, InvalidState = 4

Compare the returned status against the [`RENDER_QUEUE_*` constants](../index.md#constants) on `RenderQueue`, for example `app.RenderQueue.RENDER_QUEUE_RUNNING`.

Since: **26.5**

#### Parameters

none

#### Returns

| Name   | Type  | Description                                                          |
| :----- | :---- | :------------------------------------------------------------------- |
| status | _int_ | Stopped = 0, Paused = 1, Running = 2, Stopping = 3, InvalidState = 4 |

```javascript
const app = require("mediaencoder");
const status = app.RenderQueue.getInstance().getStatus();
status; // 0 | 1 | 2 | 3 | 4
```

<HorizontalLine />

### subscribeToEvent

Registers a subscription to a specific application event on a render queue instance object.

_Note: addEventLister() is required after a subscribeToEvent() call in order to actually react to an event_

Since: **26.5**

#### Parameters

| Name    | Type     | Description                                                                                                                                                                                                                                                                                    |
| :------ | :------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| eventId | _string_ | The event ID to subscribe to. Can include [RENDER_QUEUE_STATUS_CHANGED](../index.md#renderqueuestatuschanged), [AUDIO_PREPROGRESS_VALUE_CHANGED](../index.md#audiopreprogressvaluechanged), [WATCH_FOLDER_ENCODER_STATUS_CHANGED](../../watch-folder/index.md#watchfolderencoderstatuschanged) |
|         |

#### Returns

| Name    | Type      | Description                                   |
| :------ | :-------- | :-------------------------------------------- |
| success | _boolean_ | Returns `true` if subscription was successful |

```javascript
const app = require("mediaencoder");
const instance = app.RenderQueue.getInstance();
const event = app.RenderQueue.AUDIO_PREPROGRESS_VALUE_CHANGED;
// First Subscribe to the Event
instance.subscribeToEvent(event); // true
const callback = (value) => {
  console.log("Audio Preprogress Value Changed", value);
};
// Then Add an Event Listener to the Event
instance.addEventListener(event, callback, false);
```

<HorizontalLine />

### addEventListener

Listens for an application-level events and triggers a callback.

_Note: subscribeToEvent() is required at least once for each event time before running addEventListener()_

Since: **26.5**

#### Parameters

| Name     | Type       | Description                                                                                                                                                                                                                                                                                     |
| :------- | :--------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| eventId  | _string_   | The event ID to subscribe to. Can include: [RENDER_QUEUE_STATUS_CHANGED](../index.md#renderqueuestatuschanged), [AUDIO_PREPROGRESS_VALUE_CHANGED](../index.md#audiopreprogressvaluechanged), [WATCH_FOLDER_ENCODER_STATUS_CHANGED](../../watch-folder/index.md#watchfolderencoderstatuschanged) |
| callback | _function_ | A function to be triggered on when the specified event occurs                                                                                                                                                                                                                                   |
| unkown   | _boolean_  | TODO                                                                                                                                                                                                                                                                                            |

#### Returns

none

```javascript
const app = require("mediaencoder");
const instance = app.RenderQueue.getInstance();
const event = app.RenderQueue.AUDIO_PREPROGRESS_VALUE_CHANGED;
// First Subscribe to the Event
instance.subscribeToEvent(event); // true
const callback = (value) => {
  console.log("Audio Preprogress Value Changed", value);
};
// Then Add an Event Listener to the Event
instance.addEventListener(event, callback, false);
```

<HorizontalLine />

### removeEventListener

Removes an event listener from an application-level event.

Since: **26.5**

#### Parameters

| Name     | Type       | Description                                                                                                                                                                                                                                                                                    |
| :------- | :--------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| eventId  | _string_   | The event ID to subscribe to. Can include [RENDER_QUEUE_STATUS_CHANGED](../index.md#renderqueuestatuschanged), [AUDIO_PREPROGRESS_VALUE_CHANGED](../index.md#audiopreprogressvaluechanged), [WATCH_FOLDER_ENCODER_STATUS_CHANGED](../../watch-folder/index.md#watchfolderencoderstatuschanged) |
| callback | _function_ | A function to be removed from the event listener                                                                                                                                                                                                                                               |

#### Returns

none

```javascript
const app = require("mediaencoder");
const instance = app.RenderQueue.getInstance();
const event = app.RenderQueue.AUDIO_PREPROGRESS_VALUE_CHANGED;
// First Subscribe to the Event
instance.subscribeToEvent(event); // true
const callback = (value) => {
  console.log("Audio Preprogress Value Changed", value);
};
// Then Add an Event Listener to the Event
instance.addEventListener(event, callback, false);
// Finally Remove the Event Listener
instance.removeEventListener(event, callback);
```

<HorizontalLine />
