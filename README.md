# Easter Egg

A tiny browser demo that watches the DOM and refuses to stay deleted.

Open DevTools, delete the protected element, and watch it come back — with a message that gets cheekier the more you try.

## The idea

Most easter eggs hide behind konami codes or secret clicks. This one lives where developers already poke around: the Elements panel.

If someone inspects the page and deletes `#protected-box`, a [`MutationObserver`](https://developer.mozilla.org/en-US/docs/Web/API/MutationObserver) notices the removal, logs a styled “Nice try” in the console, and puts the element back after a short delay. Keep trying and the copy escalates:

1. Nice try  
2. Nice try (again)  
3. Persistent, aren't you  

It’s a playful reminder that the live DOM isn’t a one-way street — scripts can react to structural changes in real time.

## How it works

```text
User deletes #protected-box in DevTools
        ↓
MutationObserver fires (childList on the parent)
        ↓
Detect removed node by id
        ↓
Bump attempt count + show message
        ↓
Recreate and append the box after ~400ms
```

The observer watches `#demo-parent` for child list changes. When a removed node is `#protected-box` (or contains it), the page rebuilds the element and appends it again. No frameworks — just plain HTML, CSS, and a few lines of JavaScript.

## Try it

1. Open `easter-egg-test.html` in a browser.
2. Open DevTools (`F12` or `Cmd+Opt+I`).
3. In the Elements panel, find `#protected-box`.
4. Right-click → **Delete element**, or select it and press Delete.
5. Watch it return. Check the console for the styled log.

## Files

| File | Purpose |
|------|---------|
| `easter-egg-test.html` | Self-contained demo page |

## Why this is useful beyond a joke

`MutationObserver` is the same API you’d use for:

- Reacting when third-party widgets inject or remove nodes  
- Guarding critical UI that shouldn’t disappear unexpectedly  
- Building lightweight “self-healing” DOM behavior without a full framework  

Here it’s just for fun — but the pattern is real.

## License

Use it, fork it, or hide it in your own site. Have fun.
