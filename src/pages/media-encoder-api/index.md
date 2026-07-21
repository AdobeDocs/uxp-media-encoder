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
  - https://github.com/karan0207
---

# Media Encoder API DOM Reference

The Media Encoder API is the application layer Media Encoder adds on top of UXP: the encoding queue, presets, jobs, and the scripting hooks you use to automate rendering.

## Overview

The following line allows you access to the Media Encoder DOM via UXP.

```javascript
const app = require("mediaencoder");
```

From here you have access to all the available API methods in Media Encoder.

### Minimum Version

You will now find minimum version information on properties and methods. This version tag corresponds to the version of Media Encoder where the member was introduced or last updated significantly. For properties, you will find a column "MIN VERSION". For methods, the version number appears alongside the documentation for the method.

## Synchronous vs Asynchronous

An important difference between ExtendScript (and CEP) and UXP is that all ExtendScript calls to Media Encoder (and other Adobe apps) were synchronous. This means they blocked the Media Encoder UI while they were executing. In UXP, a method calls are mostly asynchronous, and do not block the UI thread.

For a smooth transition between the ExtendScript DOM and the UXP DOM, all properties (get and set) in the API were designed to be synchronous and do not need to be awaited. It is worth noting that they are, in the background, asynchronous in nature.

## Working with Media Encoder Objects

Media Encoder Application

Through the `app` object, you can access all the API's Media Encoder has to offer.

You can start the Media Encoder queue with:

```javascript
const app = require("mediaencoder");
app.RenderQueue.start();
```

In the next section you can review detailed docs on all public API methods for Media Encoder.
