---
title: "Keyboard Event | Messenger Docs"
source: downloaded_docs\docs\event\keyboard
---

On this page

# Keyboard Event

## `KeyDown`[​](#keydown "Direct link to keydown")

**Definition:** `KeyDown Int`

Triggered when a key is pressed.

## `KeyUp`[​](#keyup "Direct link to keyup")

**Definition:** `KeyUp Int`

Triggered when a key is released.

Both events share the same parameter, which represents the [keyCode](https://developer.mozilla.org/en-US/docs/Web/API/KeyboardEvent/keyCode) property of the keyboard event. The `keyCode` values of common keys can be found in `Messenger.Misc.KeyCode` (available in `messenger-extra`).

note

Users can use `globalData.pressedKeys` to get the current pressed keys.

- [`KeyDown`](#keydown)
- [`KeyUp`](#keyup)