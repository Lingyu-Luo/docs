---
title: "Compositors | Messenger Docs"
source: downloaded_docs\docs\rendering\compositors
---

On this page

# Compositors

As seen before, an effect could be only applied to one renderable. What if I want to render something using multiple renderables?

The simplest example is `dstOverSrc`:

```
{-| Draw the dst renderable over the src renderable.  
-}  
dstOverSrc : Renderable -> Renderable -> Renderable  
dstOverSrc src dst =  

```

This is the default behavior when you list renderables in `REGL.group`. For example, `REGL.group [] [A, B, C]` is the same as `dstOverSrc (dstOverSrc A B) C`.

Commands like `dstOverSrc` are called compositors. They accept multiple renderables as inputs and output a renderable.

Compositors may also be nested.

## Built-in Compositors[​](#built-in-compositors "Direct link to Built-in Compositors")

### `dstOverSrc`[​](#dstoversrc "Direct link to dstoversrc")

```
{-| Draw the dst renderable over the src renderable.  
-}  
dstOverSrc : Renderable -> Renderable -> Renderable  
dstOverSrc src dst =  

```

### `maskBySrc`[​](#maskbysrc "Direct link to maskbysrc")

```
{-| Draw the dst renderable masked by the src renderable.  
-}  
maskBySrc : Renderable -> Renderable -> Renderable  
maskBySrc src dst =  

```

### `imgFade`[​](#imgfade "Direct link to imgfade")

```
{-| Fading effect using a mask image.  
  
Mask image is a gradient image, similar to [this](https://github.com/linsyking/elm-regl/blob/main/docs/asset/mask.jpg).  
  
-}  
imgFade : String -> Float -> Bool -> Renderable -> Renderable -> Renderable  
imgFade mask t invert src dst =  

```

### `linearFade`[​](#linearfade "Direct link to linearfade")

```
{-| Linear fading effect.  
-}  
linearFade : Float -> Renderable -> Renderable -> Renderable  
linearFade t src dst =  

```

- [Built-in Compositors](#built-in-compositors)
  - [`dstOverSrc`](#dstoversrc)
  - [`maskBySrc`](#maskbysrc)
  - [`imgFade`](#imgfade)
  - [`linearFade`](#linearfade)