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

<InlineAlert variant="warning" slots="heading, text" />

Sample content — pending verification

This page contains sample content that needs to be verified and changed by the engineering team.

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
