---
title: "Media Encoder API: Reference for UXP Plugins"
description: "Reference for the Adobe Media Encoder APIs your UXP plugin calls: the encoding queue, presets, jobs, and scripting automation."
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

# Media Encoder API DOM Reference

The Media Encoder API is the host-specific layer Media Encoder adds on top of UXP: render queues, presets, jobs, watch folders, progress reporting, and the scripting hooks used to automate encoding. For file system access, networking, storage, HTML, CSS, and UI components, use the shared [UXP API reference](https://developer-stage.adobe.com/uxp/uxp-api/?aio_external).

## Access the API

Load the Media Encoder module from your plugin. From `app`, you can reach every public Media Encoder API surface. For example, start the render queue with:

```javascript
const app = require("mediaencoder");
const success = await app.RenderQueue.start();
```

## Browse the API

| Area | Use it to |
| --- | --- |
| [Render Queue](render-queue/index.md) | Add sources, inspect jobs, start or stop rendering, and subscribe to queue events |
| [Render Options](render-options/index.md) | Choose presets, output paths, and work-area settings |
| [Watch Folder](watch-folder/index.md) | Inspect and manage automatic encoding folders |
| [TickTime](tick-time/index.md) | Represent precise time values used by render jobs and options |
| [Progress Category Container](progress-category-container/index.md) | Group progress categories and report progress from a plugin |
| [C2PAService](c2pa-service/index.md) | Work with Content Credentials settings and manifest locations |

## Minimum Version Tags

Properties and methods show the minimum Media Encoder version where the member was introduced or changed significantly. For properties, look for the **MIN VERSION** column. For methods, the version appears alongside the method documentation.

## Synchronous and Asynchronous Access

ExtendScript and CEP calls to Media Encoder were synchronous and could block the application UI. In UXP, most Media Encoder methods are asynchronous and do not block the UI thread. Await methods that return a Promise, or chain them with `.then()`.

Property getters and setters are exposed synchronously for a smoother transition from the ExtendScript DOM and do not need to be awaited.

## See the API in a Plugin

The [Render Queue Panel sample](../get-started/samples/render-queue-panel/index.md) uses `async` and `await` across a working TypeScript plugin. Use it to connect reference entries to real UI actions and queue behavior.
