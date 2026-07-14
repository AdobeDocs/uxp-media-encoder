---
title: Media Encoder DOM APIs
description: Working with the Media Encoder DOM APIs and how to access them from a plugin
keywords:
  - DOM Versions
  - Media Encoder DOM
contributors:
  - https://github.com/kasivn
---

# Media Encoder DOM APIs

Media Encoder DOM APIs (Document Object Model) are used to create and modify Media Encoder's application state—the encoding queue, jobs, presets, and output settings. This is the same "Media Encoder APIs" layer introduced in [Understanding UXP APIs](../apis/index.md#media-encoder-apis).

<InlineAlert variant="info" slots="text1, text2" />

The Media Encoder DOM is available only as a JavaScript module and should be retrieved on a need basis using `require()`.

To access the Media Encoder DOM APIs, use

```js
const app = require("mediaencoder");
```

<InlineAlert variant="info" slots="heading, text" />

Content pending

This page is a placeholder. A complete walkthrough of the Media Encoder DOM object model—covering the queue, jobs, presets, and outputs—will be added once the API surface is finalized. In the meantime, see the [Media Encoder API reference](../../../media-encoder-api/index.md) for the authoritative list of available classes and methods.

## DOM version

The minimum DOM version needed for UXP development tracks the minimum Media Encoder version that supports UXP development; see the [Media Encoder API reference](../../../media-encoder-api/index.md) for the version supported by each release.