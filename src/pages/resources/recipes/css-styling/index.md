---
title: CSS Styling
description: Style your plugin's user interface using CSS classes, inline styles, or JavaScript
keywords:
  - CSS
  - styling
  - UI
  - Spectrum
contributors:
  - https://github.com/kasivn
---

# CSS Styling

<InlineAlert variant="warning" slots="heading, text" />

Sample content — pending verification

This page contains sample content that needs to be verified and changed by the engineering team.

UXP supports standard CSS for styling your plugin's interface. You can apply styles using **CSS classes**, **inline styles**, or **JavaScript**.

<CodeBlock slots="heading, code" repeat="3" languages="HTML, JavaScript, CSS" />

#### index.html

```html
<!-- 1. Using CSS classes -->
<div class="green-background">
  <h1>Styled with CSS class</h1>
</div>

<!-- 2. Using inline styles -->
<div style="background-color: yellow;">
  <h1>Styled inline</h1>
</div>

<!-- 3. Using JavaScript -->
<div id="exampleDiv">
  <h1>Styled with JavaScript</h1>
</div>
```

#### index.js

```js
// Apply styles via JavaScript
const exampleDiv = document.getElementById("exampleDiv");
exampleDiv.style.backgroundColor = "orange";
```

#### styles.css

```css
/* Define styles in a stylesheet */
.green-background {
  background-color: green;
}
```
