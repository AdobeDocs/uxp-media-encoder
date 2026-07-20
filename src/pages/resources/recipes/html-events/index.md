---
title: HTML Events and Listeners
description: Handle user interactions using event listeners in JavaScript or inline event handlers
keywords:
  - events
  - event listeners
  - click
  - addEventListener
contributors:
  - https://github.com/kasivn
---

# HTML Events and Listeners

<InlineAlert variant="warning" slots="heading, text" />

Sample content — pending verification

This page contains sample content that needs to be verified and changed by the engineering team.

UXP supports standard HTML events for handling user interactions like clicks, input changes, and keyboard actions. The recommended approach is to attach event listeners in JavaScript using `addEventListener()`.

<CodeBlock slots="heading, code" repeat="2" languages="HTML, JavaScript" />

#### index.html

```html
<button id="firstButton">Click me</button>
<button id="secondButton">Click me too</button>
```

#### index.js

```js
// Method 1: addEventListener (recommended)
const firstButton = document.getElementById("firstButton");
firstButton.addEventListener("click", handleClick);

// Method 2: Event handler property
const secondButton = document.getElementById("secondButton");
secondButton.onclick = handleClick;

function handleClick(event) {
  console.log(`Button clicked: ${event.target.id}`);
}
```
