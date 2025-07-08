---
title: "Roadmap | Messenger Docs"
source: downloaded_docs\docs\misc\roadmap
---

On this page

# Roadmap

This section contains some ideas we'd like to implement in future versions of Messenger. We welcome users to post feature requests in our Messenger repository's issues.

## Multi-pass Updater[​](#multi-pass-updater "Direct link to Multi-pass Updater")

Some components may want to do some operations after all other components have finished. This is the **second-pass** updater. We plan to extend this idea further to support **multi-pass** updater. Components may update **any** number of passes in one event update.

## Advanced Component View[​](#advanced-component-view "Direct link to Advanced Component View")

Users might want to have `List (Renderable, Int)` instead of `(Renderable, Int)`. In fact, this is what Reweave does. A use-case is that a component may have some parts behind the player and some other parts in front of the player.

## Unified Custom Element[​](#unified-custom-element "Direct link to Unified Custom Element")

Unify the rendering and the audio system.

## Asset Manager[​](#asset-manager "Direct link to Asset Manager")

Design a better asset manager that helps manage all the assets, including audios, images, and other data.

- [Multi-pass Updater](#multi-pass-updater)
- [Advanced Component View](#advanced-component-view)
- [Unified Custom Element](#unified-custom-element)
- [Asset Manager](#asset-manager)