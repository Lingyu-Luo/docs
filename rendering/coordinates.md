---
title: "Coordinate and Camera System | Messenger Docs"
source: downloaded_docs\docs\rendering\coordinates
---

On this page

# Coordinate and Camera System

By default Messenger integrates Elm-regl's camera and virtual coordinate system.

The default virtual canvas size is `1920x1080`.

The following is an illustration of the coordinate system:

![](data:image/png;base64,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)

The coordinate increases on the east and south direction.

Note that this is only virtual coordinates used in Messenger, and the actual canvas size may vary based on screen size.

## Camera System[​](#camera-system "Direct link to Camera System")

Messenger provides with a Global Camera that could be set in `globalData.camera` and many Local Cameras that could override the global camera's rule.

A camera setting is defined as:

```
  
{-| Camera settings.  
-}  
type alias Camera =  
    { x : Float  
    , y : Float  
    , zoom : Float  
    , rotation : Float  
    }  

```

The `x` and `y` are the center coordinates of the camera. The camera will capture a canvas in the virtual coordinate system of size specified in virtual canvas size.

By default, `x` and `y` are set to half of the virtual canvas size, which in our case is `960` and `540`.
`zoom` is 1 and `rotation` is 0 by default. The default camera is also called UI camera as it is mainly used for UI drawing.

A great feature of Messenger's camera system is that the global camera setting could be **override** by using `groupWithCamera`.

```
groupWithCamera : Camera -> List Effect -> List Renderable -> Renderable  

```

You may even override the camera inside a `groupWithCamera`:

```
groupWithCamera camera1 [  
    groupWithCamera camera2 [  
        ...  
    ]  
]  

```

You could use the default camera (UI camera) by calling `defaultCamera` from `Messenger.Coordinate.Camera`.

## Manual Coordinate System Transformation[​](#manual-coordinate-system-transformation "Direct link to Manual Coordinate System Transformation")

In some cases, users may want to manually transform a coordinate in world space to view space, or vice versa. Messenger provides two handy functions in `Messenger.Coordinate.Camera`:

```
{-| Tranform a position from the world coordinate system to the view (camera) coordinate system.  
-}  
worldToView : Camera -> ( Float, Float ) -> ( Float, Float )  
worldToView camera ( x, y ) =  
  
{-| Transform a position from the view coordinate system to the world coordinate system.  
  
This is the inverse of `worldToView`.  
  
-}  
viewToWorld : Camera -> ( Float, Float ) -> ( Float, Float )  
viewToWorld camera ( x, y ) =  

```

- [Camera System](#camera-system)
- [Manual Coordinate System Transformation](#manual-coordinate-system-transformation)