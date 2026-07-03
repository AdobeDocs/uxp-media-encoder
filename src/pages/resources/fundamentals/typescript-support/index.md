---
keywords:
  - TypeScript
  - UXP
  - JavaScript
  - tsconfig.json
  - jsconfig.json
  - IntelliSense
  - Type definitions
  - JSDoc
title: TypeScript Support
description: Learn about the TypeScript support in UXP and Media Encoder
contributors:
  - https://github.com/undavide
---

# TypeScript Support

Learn how to use TypeScript in UXP plugins

## Overview

When building UXP plugins for Media Encoder, having accurate autocomplete and type checking will significantly improve your development experience. Whether you prefer plain JavaScript or full TypeScript, you can use the same type definitions that give you IntelliSense, error detection, and inline documentation right in your code editor.

This guide covers two approaches:

1. **[JavaScript with JSDoc](#javascript-intellisense)**: get IntelliSense in existing JavaScript projects without a build step.
2. **[TypeScript projects](#typescript-projects)**: use full TypeScript for compile-time type checking and advanced features.

Both approaches are based on the same Type Definitions for Media Encoder DOM APIs, so you get accurate autocomplete and documentation regardless of which path you choose.

## Media Encoder DOM APIs

### Type Definitions

Complete TypeScript type definitions for all Media Encoder DOM APIs are available as an NPM package [`@adobe/mediaencoder`](https://www.npmjs.com/package/@adobe/mediaencoder). This package includes:

- All Media Encoder classes and their methods (`Queue`, `Job`, `Preset`, etc.)
- Constants and enums (`JobStatus`, `OutputFormat`, etc.)
- Complete method signatures with parameter and return types
- JSDoc comments with descriptions for every API

You can install this package through `npm` or your preferred package manager of choice, for example:
```sh
$ npm install -D @adobe/mediaencoder

# Using yarn
$ yarn add -D @adobe/mediaencoder

# Using pnpm
$ pnpm add -D @adobe/mediaencoder
```

### JavaScript Intellisense

You can get full IntelliSense[^1] in plain JavaScript files **without TypeScript** using JSDoc comments. This approach doesn't require any build step and will work out of the box with your existing JavaScript workflow.

[^1]: IntelliSense is the feature that allows you to get autocomplete and type hints in your code editor.

#### Quick Setup

1. **Install the `@adobe/mediaencoder` package**
2. **Create a `jsconfig.json`[^2] file** in your plugin's root directory:

[^2]: `jsconfig.json` is a configuration file for JavaScript projects.

```json
{
  "compilerOptions": {
    "checkJs": true,
    "target": "ES2020",
    "lib": ["ES2020", "DOM"]
  },
  "include": ["*.js"],
  "exclude": ["node_modules", "dist"]
}
```

3. **Add JSDoc type hints** to your JavaScript code:

```javascript
/** @type {import('@adobe/mediaencoder').mediaencoder} */
const app = require("mediaencoder");

// Now you get full IntelliSense!
app.queue.getActiveJob(); // ✅ Autocomplete works!
```

You may need to restart your code editor to activate IntelliSense.

#### JSDoc Patterns

Here are common patterns for adding type hints to your JavaScript code. The key is to type the main `app` object—from there, types flow automatically through method calls. You only need explicit annotations for function parameters or when you want to add clarity.

**Type hint for the main API:**

```javascript
/** @type {import('@adobe/mediaencoder').mediaencoder} */
const app = require("mediaencoder");

async function example() {
  const queue = app.queue;
  const job = await queue.getActiveJob();

  // Types flow through automatically; job has full IntelliSense!
  const outputCount = await job.getOutputCount();
}
```

**Function parameters and return types:**

```javascript
/**
 * Analyze all outputs in an encoding job
 * @param {import('@adobe/mediaencoder').Job} job - The job to analyze
 * @returns {Promise<void>}
 */
async function analyzeOutputs(job) {
  const outputCount = await job.getOutputCount();

  for (let i = 0; i < outputCount; i++) {
    const output = await job.getOutput(i);
    console.log(`Output ${i}: ${output.name}`);
  }
}
```

**Arrays and complex types:**

```javascript
/**
 * Process multiple queue items
 * @param {import('@adobe/mediaencoder').QueueItem[]} queueItems
 */
async function processQueueItems(queueItems) {
  for (const item of queueItems) {
    // item has full IntelliSense
    const name = await item.getName();
    console.log(name);
  }
}
```

#### Pros and Cons of the JSDoc Approach

The primary advantage of JSDoc is that **it doesn't require any build steps**—your existing development workflow remains unchanged, while gaining **full IntelliSense with autocomplete and type hints** in your editor. Type checking happens as you write code, catching errors before runtime. This approach works with any modern code editor, including VSCode and Cursor.

However, JSDoc has limitations compared to full TypeScript. Type errors appear as **editor warnings rather than compile-time errors** that block execution. You may need to write more explicit type annotations as JSDoc comments throughout your code, whereas TypeScript can infer many types automatically. **Advanced TypeScript features** like generics, utility types, and conditional types **are not available** with JSDoc.

For smaller projects, JSDoc provides a practical, plug-and-play solution. If your plugin grows in complexity, you can always migrate to TypeScript later.

### TypeScript Projects

For larger codebases and development teams, TypeScript has become a standard. It provides **compile-time error checking**, **better refactoring support**, and access to **advanced TypeScript features**.

#### Quick Setup

1. **Install the `@adobe/mediaencoder` package**
2. **Install TypeScript** and create your source folder:

```bash
npm install --save-dev typescript
mkdir src
```

3. **Create a `tsconfig.json` file** in your plugin's root directory:

```json
{
  "compilerOptions": {
    "target": "ES2020",
    "module": "commonjs",
    "lib": ["ES2020", "DOM"],
    "outDir": "./dist",
    "rootDir": "./src",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules", "dist"]
}
```

4. **Move your code to TypeScript**: move `main.js` to `src/main.ts` and update your code to use TypeScript syntax

Your project structure should now look like this:

```text
your-plugin/
    ├── tsconfig.json      # TypeScript config
    ├── package.json
    ├── manifest.json
    ├── index.html
    ├── src/
    │   └── main.ts       # Your TypeScript code
    └── dist/             # Generated JavaScript (after build)
        └── main.js
```

1. **Add build scripts** to your `package.json`:

```json
{
  "scripts": {
    "build": "tsc",
    "watch": "tsc --watch"
  }
}
```

6. **Update your `index.html`** to reference the compiled output:

```html
<script src="dist/main.js"></script>
```

7. **Build your plugin**:

```bash
npm run build
```

#### TypeScript Syntax

With TypeScript, you get cleaner syntax and better type inference:

```typescript
import type { mediaencoder, Job, Output } from '@adobe/mediaencoder';

const app = require("mediaencoder") as mediaencoder;

async function analyzeQueue(): Promise<void> {
  const queue = app.queue;
  if (!queue) return;

  // TypeScript infers types automatically
  const job = await queue.getActiveJob();
  if (!job) return;

  // Full type safety and IntelliSense
  const outputCount: number = await job.getOutputCount();

  for (let i = 0; i < outputCount; i++) {
    const output: Output = await job.getOutput(i);
    console.log(`Output ${i}: ${output.name}`);
  }
}
```

#### Development Workflow

The recommended workflow for TypeScript projects:

1. **Terminal**: run `npm run watch` mode for automatic compilation
2. **Editor**: edit `src/main.ts` with full IntelliSense and type checking
3. **Media Encoder**: reload the plugin via UXP Developer Tool to test changes

#### Pros and Cons of TypeScript

TypeScript provides significant advantages for larger projects. **Compile-time type checking** catches bugs before you run your plugin, while improved type inference offers more accurate autocomplete than JSDoc. **Refactoring becomes safer**—you can rename variables and functions across your entire codebase with confidence. You also gain **access to advanced features** like interfaces, generics, and utility types, along with enhanced debugging and IDE support that these features enable.

However, TypeScript requires **additional setup and tooling**. You must **compile** TypeScript to JavaScript before testing your plugin, which adds a build step to your workflow. There's also a **learning curve** if you're not already familiar with TypeScript syntax and concepts. For complex plugins or teams experienced with TypeScript, these requirements are typically justified by the improved developer experience and code quality.