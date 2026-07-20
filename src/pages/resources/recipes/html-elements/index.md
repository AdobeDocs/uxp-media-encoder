---
title: Creating HTML Elements
description: Build user interfaces using HTML markup or JavaScript DOM methods
keywords:
  - HTML
  - DOM
  - UI
  - createElement
  - dialog
contributors:
  - https://github.com/kasivn
---

# Creating HTML Elements

<InlineAlert variant="warning" slots="heading, text" />

Sample content — pending verification

This page contains sample content that needs to be verified and changed by the engineering team.

UXP lets you create UI elements in two ways: **define them in HTML** or **create them dynamically with JavaScript**.

<CodeBlock slots="heading, code" repeat="3" languages="HTML, JavaScript, CSS" />

#### index.html

```html
<button id="showDialog">Show Dialog</button>

<dialog id="sampleDialog">
  <div>
    <h1>Hello! 👋</h1>
    <p>A dialog built using HTML tags</p>
  </div>
</dialog>
```

#### index.js

```js
const showDialogBtn = document.getElementById("showDialog");
showDialogBtn.addEventListener("click", () => {
  const dialog = document.getElementById("sampleDialog");
  dialog.show();

  dialog.addEventListener("cancel", () => {
    console.log("Dialog dismissed");
  });
});
```

#### styles.css

```css
#sampleDialog > div {
  display: flex;
  flex-direction: column;
  height: 300px;
  width: 400px;
  align-items: center;
  color:#DDD;
}

h1 { color: #FFF; }

#sampleDialog > div > p {
  margin-top: 30px;
}

```
