---
title: "Rendering | Messenger Docs"
source: downloaded_docs\docs\category\rendering
---

# Rendering

[## 📄️ Rendering

As mentioned before, Messenger uses virtual coordinates to render. The transformation from virtual coordinates to real coordinates are mostly done in the shaders.](/docs/rendering/render)

[## 📄️ Coordinate and Camera System

By default Messenger integrates Elm-regl's camera and virtual coordinate system.](/docs/rendering/coordinates)

[## 📄️ Color

Elm-regl uses premultiplied alpha rendering mode in WebGL to create more accurate rendering and compositing.](/docs/rendering/color)

[## 📄️ Global Rendering Options

Elm-regl provides some initialization options:](/docs/rendering/opts)

[## 📄️ Shapes

Elm REGL provides several builtin commands to draw shapes. All those commands are in REGL.BuiltinPrograms.](/docs/rendering/shapes)

[## 📄️ Text

Text rendering is more complex than simple shapes because a single character may need to draw hundreds of triangles based on its shape.](/docs/rendering/text)

[## 📄️ Texture

Before rendering textures in the game, users need to load the texture asset.](/docs/rendering/texture)

[## 📄️ Effects

Effects are some visual effects applied after rendering a REGL.group. For example, we provide gblur effect which applies a Gaussian Blur effect.](/docs/rendering/effects)

[## 📄️ Compositors

As seen before, an effect could be only applied to one renderable. What if I want to render something using multiple renderables?](/docs/rendering/compositors)

[## 📄️ Custom Programs

This is a very advanced usage of the renderer. Do not use this if you are not familiar with shaders (GLSL).](/docs/rendering/custom_programs)