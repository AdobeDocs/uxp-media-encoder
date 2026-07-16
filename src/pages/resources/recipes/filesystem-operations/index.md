---
title: Filesystem Operations
description: Learn how to read, write, and manage files & folders in UXP plugins
keywords:
  - localFileSystem
  - FS API
  - fullAccess
  - file permissions
  - sandbox
contributors:
  - https://github.com/kasivn
---

# Filesystem Operations

<InlineAlert variant="warning" slots="heading, text" />

Sample content — pending verification

This page contains sample content that needs to be verified and changed by the engineering team.

UXP provides APIs for reading, writing, creating, and deleting files. Access to the sandbox (your plugin's own installation, data, and temporary folders) requires the `"plugin"` `localFileSystem` permission level in `manifest.json`.

<CodeBlock slots="heading, code" repeat="2" languages="JavaScript, JSON" />

#### index.js

```js
const { localFileSystem } = require('uxp').storage;

async function accessPluginDataFolder() {
    // Access the plugin's data folder
    try {
        const dataFolder = await localFileSystem.getEntryWithUrl("plugin-data:/");
        console.log(`Data folder path: ${dataFolder.nativePath}`);

        // List all files in the data folder
        const entries = await dataFolder.getEntries();
        console.log(`Found ${entries.length} items in data folder`);

        for (const entry of entries) {
            console.log(`- ${entry.name} (${entry.isFile ? 'file' : 'folder'})`);
        }
    } catch (e) {
        console.error("Failed to access data folder:", e);
    }
}
```

#### manifest.json

```json
{
  "manifestVersion": 5,
  // ...
  "requiredPermissions": {
    "localFileSystem": "plugin"
  }
  // ...
}
```
