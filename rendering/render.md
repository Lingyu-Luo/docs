---
title: "Rendering | Messenger Docs"
source: downloaded_docs\docs\rendering\render
---

On this page

# Rendering

As mentioned before, Messenger uses *virtual coordinates* to render. The transformation from virtual coordinates to real coordinates are mostly done in the shaders.
The virtual coordinate system is supported by elm-regl, which makes the rendering process simpler for Messenger.

It also has a simple camera system that is able to transform, rotate and zoom the objects.
Users could also implement their own camera if needed.

The drawing style of Messenger is rather *declarative*. Declarative rendering has many benefits:

- Simple to read, debug and understand
- Allow transparent abstraction of layers

A famous example of declarative drawing API is SVG. However, SVG is only for vector graphics and it performs bad.

Messenger's rendering backend, elm-regl, uses a custom declarative language called **DRDL** (Declarative REGL Drawing Language). The elm-regl library generates DRDL from the elm side and passes it to elm REGL JS port.
The elm REGL JS will handle it and renders.

Users do not need to touch the low-level DRDL. Instead, elm-regl library provides the abstraction.

## Basic concepts[​](#basic-concepts "Direct link to Basic concepts")

Elm-regl defines a basic type `Renderable`. Renderable is an abstraction of some drawings on the screen.

A REGL command is a function that generates a renderable.

For example, the command to draw a triangle is defined as:

REGL/BuiltinPrograms.elm

```
triangle : ( Float, Float ) -> ( Float, Float ) -> ( Float, Float ) -> Color -> Renderable  

```

The commands like `triangle` does not really draw a triangle when you call it. The command internally genrates a call to a registerd REGL program. The call will be triggered to run the associated program during rendering after the update logic.

Users need to provide three coordinates and a color to draw a triangle. Remember that the `view` function of Messenger general model accepts a renderable, so it is very easy to draw anything in Messenger.

## Structural Drawing[​](#structural-drawing "Direct link to Structural Drawing")

The most important feature of declarative drawing is *structural drawing*. It allows users to group a list of renderables:

REGL.elm

```
group : List Effect -> List Renderable -> Renderable  

```

The first argument is a list of effects users want to apply for all the renderables. See [effects](/docs/rendering/effects) for more details.

`group [] [a, b]` draws `a` first, then draws `b`. Elm REGL does not enable depth test so the order of rendering determines which is on the top.

Structural drawing allows users to divide a big scene into several "layers" and render them in different groups.

tip

To render nothing, please use `REGL.empty` instead of `REGL.group [] []`.

- [Basic concepts](#basic-concepts)
- [Structural Drawing](#structural-drawing)