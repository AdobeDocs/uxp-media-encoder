---
title: "Render Queue Instance: Media Encoder API"
description: "Media Encoder's Queue Instance APIs for adding, modifying, and enquing items for render."
id: renderQueue
title: RenderQueue
sidebar_label: RenderQueue
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
---

# Render Queue Instance

The Media Encoder Queue Instance API is the used for up to date methods on the Render Queue.

<InlineAlert variant="info" slots="text"/>

UXP for Adobe Media Encoder is in public beta. This reference is being written, and the supported API surface may change before general availability.

<HorizontalLine />

### getStatus

Provides the current status of the rendering queue, represented as an enumeration.

The possible states are: Stopped = 0, Paused = 1, Running = 2, Stopping = 3, InvalidState = 4

These states can be accessed as enum types using a RenderQueueEvent object.

For example, you can check the render queue status using `renderqueueEventObject.RENDER_QUEUE_RUNNING`

For more information, refer to the RenderQueueEvent scripting API documentation

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
