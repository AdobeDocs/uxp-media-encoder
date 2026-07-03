---
title: Understanding UXP APIs
description: The difference between UXP core and host-specific APIs
keywords:
  - APIs
  - UXP core
  - DOM APIs
  - Media Encoder APIs
contributors:
  - https://github.com/padmkris123
  - https://github.com/undavide
---

# Understanding UXP APIs

Learn about the two types of APIs available in UXP and when to use each one

## Overview

Now that you have successfully built your first [plugin](../../../plugins/index.md), you're ready to tackle more complex tasks. The key to building useful plugins is understanding which APIs to use and when.

The UXP platform provides two complementary sets of APIs:

1. **UXP Core APIs**: for building user interfaces, file operations, network calls, and general functionality.
2. **Media Encoder APIs**: for interacting with and modifying Media Encoder encoding jobs and the queue.

Most often than not, you will need to use both APIs together to create the functionality you want. Let's explore each one and see how they work.

## UXP Core APIs

UXP Core APIs provide the fundamental building blocks for your plugin's functionality, and are **shared** across all Adobe Creative Cloud applications that support UXP. These APIs let you:

- **Create user interfaces** using HTML, CSS, and JavaScript
- **Access the file system** to read and write files
- **Make network requests** to communicate with external services
- **Handle clipboard operations** for copy/paste functionality
- **Work with system utilities** like shell commands and OS information

### Accessing UXP APIs

The way you access UXP APIs depends on the specific API itself.

[**Global APIs**](../../../uxp-api/index.md) are available immediately without any import. For example:

```javascript
// Crypto API is globally available
const hash = crypto.randomUUID();

// Document API is globally available
const button = document.createElement("sp-button");
```

[**Module-based APIs**](../../../uxp-api/index.md) require importing with `require()`. For example:

```javascript
// Parent UXP module
const uxp = require("uxp");

// File system access
const fs = require("fs");

// Operating system utilities
const os = require("os");
```

**Permission-based APIs** also need to be allow-listed in your plugin's `manifest.json`. For example, to use the file system or make network requests, you must declare the appropriate permissions. Learn more about permissions in the [Manifest guide](../../../plugins/index.md).

## Media Encoder APIs

Media Encoder APIs, also interchangeably called **DOM APIs** (Document Object Model) or **Media Encoder DOM APIs**, give you direct access to Media Encoder's application model. These APIs let you, among other things, to:

- **Access and modify encoding jobs** — queue items, presets, and output settings
- **Work with media** — import files, manage project items
- **Control the queue** — start, pause, and monitor encoding jobs
- **Apply presets** — assign encoding presets and format settings to jobs
- **Export content** — configure and trigger exports

The entry point to Media Encoder APIs is the `app` object, that you `require()` from the `"mediaencoder"` module.

```javascript
const app = require("mediaencoder");
```

You'll learn how to access and use Media Encoder APIs in the [Working with Media Encoder APIs](../dom-apis/index.md) section and by browsing the [Media Encoder API reference](../../../media-encoder-api/index.md).

<InlineAlert variant="warning" slots="heading, text" />

Don't confuse the two DOMs

The **Media Encoder DOM** controls the Media Encoder application state (queue, presets, output settings). The **HTML DOM** controls your plugin's user interface (buttons, inputs, panels). They are completely separate systems.

### Unified JavaScript Engine

As the platform's name [suggests](../../../index.md), UXP provides a _unified_ JavaScript engine that has **direct access to both the Media Encoder APIs and the UXP Core APIs**. This is a big advantage over the previous extensibility technology (CEP), where the communication between the extension logic and the host application happened through a bridge (CSInterface) that passed messages back and forth between the two runtimes.

With UXP, everything runs natively in the same environment, and you just need to `require()` the appropriate modules to access the APIs you need.

## Practical Example

Let's see how both API types work together. Imagine you want to build a plugin that:

1. Reads a list of file paths from a text file on the user's computer
2. Adds each file to the Media Encoder queue
3. Applies a specific encoding preset to each queued item

Here's which APIs you would use for each step:

**Step 1: Read file content** — Use UXP's `fs` module

```javascript
const fs = require("fs");
const file = await fs.getFileForOpening();
const content = await file.read();
```

**Step 2: Add file to the queue** — Use Media Encoder APIs

```javascript
const app = require("mediaencoder");
const queue = app.queue;
// Add file to the encoding queue
```

**Step 3: Apply a preset** — Use both APIs

```javascript
// Media Encoder APIs to apply the preset to the queued item
// UXP APIs to show progress in your plugin's UI
```

This demonstrates how UXP Core APIs handle the infrastructure, while Media Encoder APIs handle the encoding job manipulation.

## API Versioning and Compatibility

Both UXP and Media Encoder APIs are actively evolving, with new capabilities added in each release. It's important to understand how versioning works to ensure your plugin functions correctly.

### Host Application and UXP

- **Media Encoder version** (v26.5): determines which Media Encoder DOM APIs are available.
- **UXP version** (v8.1): determines which UXP Core APIs are available.

Each Media Encoder release integrates a specific UXP version. For example, Media Encoder v26.5 includes UXP v8.1.

<InlineAlert variant="info" slots="heading, text, text2" />

Handling Version Mismatches

If your plugin relies on an API introduced in UXP v8.2, but the user is running Media Encoder v26.5 (which only includes UXP v8.1), it will throw errors and fail to run. The same applies if your plugin depends on APIs added in Media Encoder v26.6 but the user is still on v26.5.

To avoid compatibility issues, make sure to target APIs common to both versions, or implement fallback logic for older releases when possible.

### Checking Versions

You can determine the UXP version in several ways:

#### 1. In the UXP Developer Tool

Once Media Encoder is running and appears under "Connected apps", you'll see both the Media Encoder version and UXP version displayed.

![UXP version in the UXP Developer Tool](./img/apis-udt.png)

If you only see the host application version (as in the case of Photoshop in the screenshot above), please click the arrow next to the product icon to expand the details.

#### 2. Programmatically in your plugin

```javascript
const { host, version } = require("uxp");
console.log(`Media Encoder ${host.version}`); // Media Encoder 26.5.0
console.log(`UXP ${versions.uxp}`);          // UXP uxp-8.1.0-local
```

See the [host info recipe](../../recipes/host-info/index.md) for a complete example.

#### 3. In the documentation

Refer to the [Media Encoder API reference](../../../media-encoder-api/index.md) for the UXP version supported by each Media Encoder release, along with new features, changes, and fixes.

## Next Steps

Now that you understand the two types of APIs available, you're ready to:

- Explore practical [code recipes](../../recipes/index.md) that demonstrate common tasks
- Learn how to [work with Media Encoder APIs](../dom-apis/index.md) in depth
- Browse the complete [UXP API reference](../../../uxp-api/index.md) and [Media Encoder API reference](../../../media-encoder-api/index.md)