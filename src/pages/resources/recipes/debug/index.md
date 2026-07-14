---
title: Debugging Techniques
description: Use console logs and dialog methods to debug your UXP plugin quickly
keywords:
  - debugging
  - console
  - alerts
  - developer tools
contributors:
  - https://github.com/kasivn
---

# Debugging Techniques

Use console logs and dialog methods to debug your plugin quickly

While the [UXP Developer Tool](../../../plugins/index.md) offers a full debugging experience with breakpoints and the Chrome DevTools, these simple techniques can help you quickly troubleshoot issues during development.

## Prerequisites

<InlineAlert variant="info" slots="heading, text"/>

Placeholder — versions to be confirmed

Minimum supported versions for Media Encoder, the UXP Developer Tool, and the manifest schema will be added here once confirmed by the product team.

## Console Logging

The simplest way to debug is to log values to the console. Open the UXP Developer Tool console to view output.

```js
// Basic logging
console.log("Plugin initialized");          // 💡 General information
console.warn("This feature is deprecated"); // ⚠️ Warnings (yellow)
console.error("Failed to load data");       // ❌ Errors (red)

// Log variables and objects
const user = { name: "Jane", role: "Editor" };
console.log("User data:", user);
// Logs: User data: { name: "Jane", role: "Editor" }

// Log multiple values using template literals
const width = 1920;
const height = 1080;
console.log(`Resolution: ${width}x${height}`); // Template literals for formatting
```

## Dialog-based Debugging

For quick checks without switching to the console, use dialog methods to display information or input values directly in the UI.

<InlineAlert variant="error" slots="text"/>

The `alert()`, `confirm()`, and `prompt()` methods are not fully supported in Media Encoder; they will be fixed in a future release.

<InlineAlert variant="info" slots="heading, text"/>

Requires Manifest configuration

To use [`alert()`](../../../uxp-api/index.md), [`confirm()`](../../../uxp-api/index.md), and [`prompt()`](../../../uxp-api/index.md), you must enable the `enableAlerts` feature flag in your [`manifest.json`](../../../plugins/index.md).

<CodeBlock slots="heading, code" repeat="2" languages="JavaScript, JSON" />

#### index.js

```js
// Simple alert dialog
alert("Plugin loaded successfully");

// Confirmation dialog
const confirmed = confirm("Do you want to continue?");
if (confirmed) {
  console.log("User clicked OK");
} else {
  console.log("User clicked Cancel");
}

// Prompt dialog for user input
const userName = prompt("Enter your name:", "Default Name");
console.log(`User entered: ${userName}`);
```

#### manifest.json

```json
{
  "manifestVersion": 5,
  // ...
  "featureFlags": {
    "enableAlerts": true
  }
  // ...
}
```

## Using UXP Developer Tool

For comprehensive debugging using the UXP Developer Tool, please refer to the [Plugin Workflows](../../../plugins/index.md) documentation.

## Reference Material

- [`alert()`](../../../uxp-api/index.md): display simple alert dialogs.
- [`confirm()`](../../../uxp-api/index.md): display confirmation dialogs.
- [`prompt()`](../../../uxp-api/index.md): prompt users for input.
