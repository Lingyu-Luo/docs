---
title: "Effects | Messenger Docs"
source: downloaded_docs\docs\rendering\effects
---

On this page

# Effects

Effects are some visual effects applied after rendering a `REGL.group`. For example, we provide `gblur` effect which applies a [Gaussian Blur](https://en.wikipedia.org/wiki/Gaussian_blur) effect.

```
import REGL  
import REGL.Effects as E  
  
view = REGL.group [ ] [  
    A,  
    REGL.group (E.gblur 3) [  
        C, D  
    ],  
    B  
]  

```

In this example, A and B are two other renderables. A will be rendered first on the main "palette", C and D will be rendered using another new palette. The new palette will be applied with a `gblur` effect. C and D will be affected, A and B will not be affected.
Then the new palette will be rendered to the main palette. Finally B will be rendered.

## Multiple Effects[​](#multiple-effects "Direct link to Multiple Effects")

Multiple effects could be used together. The order matters.

```
REGL.group [  
    A,  
    B,  
    C  
]  

```

A effect will be applied before B, while B effect will be applied before C.

## Nested Effects[​](#nested-effects "Direct link to Nested Effects")

Nested effects are also supported.

```
REGL.group [ A ] [  
    REGL.group [ B ] [  
        C  
    ]  
]  

```

Here C will be first applied with effect B, then applied with effect A.

## Built-in Effects[​](#built-in-effects "Direct link to Built-in Effects")

`Elm-REGL` provides several builtin effects.

### `blur`[​](#blur "Direct link to blur")

Simple blur effects.

```
blur : Float -> List Effect  
blur radius =  

```

### `alphamult`[​](#alphamult "Direct link to alphamult")

Multiply the alpha of the renderable with `a`.

```
alphamult : Float -> Effect  
alphamult a =  

```

warning

Using this effect to set the alpha of a single renderable may be slow. Use rendering commands with `alpha` to set alpha for texture rendering.

### `colormult`[​](#colormult "Direct link to colormult")

Multiply the color of the renderable with `rgba`.

```
alphamult : Float -> Float -> Float -> Float -> Effect  
alphamult r g b a =  

```

### `fxaa`[​](#fxaa "Direct link to fxaa")

Applies Fast approximate anti-aliasing (FXAA) to the renderable.

```
fxaa : Effect  
fxaa =  

```

### `gblur`[​](#gblur "Direct link to gblur")

Applies Gaussian Blur.

```
gblur : Float -> List Effect  
gblur sigma =  

```

### `crt`[​](#crt "Direct link to crt")

Applies the CRT effect. Must be applied outermost. `count` is the number of scan lines.

```
crt : Float -> Effect  
crt count =  

```

### `pixilation`[​](#pixilation "Direct link to pixilation")

Applies the pixilation effect. `ps` is the number of pixels that will be considered as a same pixel on the screen.

```
{-| Apply pixilation effect to a renderable.  
-}  
pixilation : Float -> Effect  
pixilation ps =  

```

tip

You could also write your custom effects using shaders. See [Custom Programs](/docs/rendering/custom_programs).

- [Multiple Effects](#multiple-effects)
- [Nested Effects](#nested-effects)
- [Built-in Effects](#built-in-effects)
  - [`blur`](#blur)
  - [`alphamult`](#alphamult)
  - [`colormult`](#colormult)
  - [`fxaa`](#fxaa)
  - [`gblur`](#gblur)
  - [`crt`](#crt)
  - [`pixilation`](#pixilation)