---
title: Media Encoder DOM APIs
description: Media Encoder DOM APIs and way to mount it.
keywords:
  - DOM Versions 
  - Media Encoder DOM
---

# Media Encoder DOM APIs

Media Encoder APIs (aka Document Object Model DOM or OMV) are used to create and modify the application document and content.

<InlineAlert variant="info" slots="text1, text2" />

Media Encoder DOM is available only as a JavaScript module and should be retrieved on a need basis using `require()`.

To access the Media Encoder DOM APIs, use

```js
const app = require("mediaencoder");
```

## DOM version

The minimum DOM version needed for UXP development is the same as the minimum required version of Media Encoder that supports UXP development.