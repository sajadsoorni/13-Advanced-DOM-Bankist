# JavaScript Event Capturing and Bubbling

This document explains, in simple terms, how JavaScript events flow through the DOM (capturing and bubbling) with a practical example.

---

## What Are Capturing and Bubbling Phases?

When you click an element on a webpage, the event goes through three steps:

1. **Capturing Phase**

   - The event starts at the top of the DOM tree (`document`) and travels **down** through every parent element until it reaches the element you clicked.
   - Example: `document` → `<html>` → `<body>` → `<section>` → `<p>` → `<a>`

2. **Target Phase**

   - The event reaches the **exact element** you clicked (the target).
   - Any event listeners on this element run here.

3. **Bubbling Phase**
   - After the target, the event travels **back up** through all parent elements to the top.
   - Any parent with an event listener will also react.

---

## Why Is This Important?

- A single event (like a click) can be handled by the target and all its parent elements.
- This enables patterns like **event delegation** (handling events for many children with one parent listener).
- By default, JavaScript event listeners run in the **bubbling phase** (as the event goes up).
- You can set listeners for the capturing phase, but this is less common.
- Most events bubble and capture.

---

## Example: Event Bubbling

### HTML

```html
<section>
  <button>Click me</button>
</section>
```

```js
// Listen for click on the section (parent)
document.querySelector('section').addEventListener('click', function () {
  alert('Section clicked!');
});

// Listen for click on the button (child)
document.querySelector('button').addEventListener('click', function () {
  alert('Button clicked!');
});
```

### How It Works

- **Click the button:**

  - You will see two alerts:
    - "Button clicked!"
    - "Section clicked!" (because the event bubbles up from button to section)

- **Click inside the section but NOT on the button:**
  - You’ll only see "Section clicked!"

---

### Why Is This Useful?

- **Event Delegation:** Handle events from many child elements with one parent listener.
- **Cleaner code:** Less repetition and easier maintenance.

---

### Summary

- Event moves **down** the tree (capturing)
- Runs on the element you clicked (target)
- Moves **back up** (bubbling)
- Any event listeners along the way can react
