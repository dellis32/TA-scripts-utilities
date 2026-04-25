
# TotalAgility HTML Control — JS Snippets

---

## `fixLayout`
**Usage**> 
- Use this if an HTML control shows up blank. It sometimes floats content off screen.
- Call from a button event or some other form event

```javascript
var el = document.querySelector('[data-automation-controlname="html1"]');
if (el) {
    el.style.float = "none";  // Remove float
    void el.offsetHeight;      // Force reflow
    el.style.float = "left";   // Reapply float
}
```

---

## `setSandbox`
> Makes a TA iFrame (HTML) control able to be 'active' links work, scripts and buttons can do things etc. 
**NOTE: this does make it less secure**

**Usage:**
- Place this JS action in **Form → After Render**
- The line `iframe.srcdoc = iframe.srcdoc;` will reset your content if it was set at form load — but a more resilient approach is to set the content explicitly **after** this action runs
- **If your HTML control is inside a tab:** call this from the **tab render event** — TA renders/destroys tabs dynamically
- **Update `title="html1"`** if you renamed the HTML control — the selector uses the default name

```javascript
const iframe = document.querySelector('iframe[title="html1"]');
//alert('iframe found: ' + (iframe ? 'YES' : 'NO'));

iframe.sandbox.add('allow-popups', 'allow-scripts', 'allow-same-origin');
iframe.srcdoc = iframe.srcdoc;

//alert('sandbox updated to: ' + iframe.getAttribute('sandbox'));
```

---

## Call a Function Inside the iFrame 
**Usage**
  - the example assumes there are exposed functions in the iframe content document DOM
  - clearEobSessionStorage() and getUpdatedEobData

### `clearEOBSessionData`

```javascript
var iframe = document.querySelector('iframe[title="html1"]');
if (iframe) {
    iframe.contentWindow.clearEobSessionStorage();
}
```

### `getEOBData`

```javascript
var iframe = document.querySelector('iframe[title="html1"]');
if (iframe) {
    const updatedData = iframe.contentWindow.getUpdatedEobData();
}
```
```