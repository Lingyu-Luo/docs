---
title: "Getting Started | Messenger Docs"
source: downloaded_docs\docs\helloworld\getstart
---

# Getting Started

First, determine the `UserData` and `SceneMsg`, which respectively represent the data that can be accessed or modified at any time and the message to be sent to the scene when switching scenes.

Next, prepare `userConfig` and a list containing all the scenes as inputs. The `userConfig` is a record that includes the basic configurations needed by Messenger core. This is automatically wrapped in `Main.elm`, so only the options in `MainConfig.elm` need to be modified.

An initial global data is also needed, but it is not necessary to provide the full global data. Instead, users only need to provide a subset that does not include any Messenger internal data.

Since this is a hello world project, only one scene is needed, so customizing `UserData` and `SceneMsg` can be skipped.

By default, Messenger does not add user layers to a scene automatically because it does not know how the layers will be initialized. It is a good practice to add layers to the scene immediately after creating them.

First, open `Scenes/Home/Model.elm` and import layer:

```
import Scenes.Home.MainLayer.Model as MainLayer  

```

Second, add the layer to `init` function:

```
init env msg =  
    ...  
    , layers =  
        [ MainLayer.layer NullLayerMsg envcd  
        ]  

```

Now open `Scenes/Home/MainLayer/Model.elm`. Change the `view` function:

```
import REGL.BuiltinPrograms as P  
import Color  
...  
view : LayerView SceneCommonData UserData Data  
view env data =  
    P.textbox ( 0, 0 ) 100 "Hello World" "consolas" Color.black  

```

tip

This view will render a textbox at the left-top corner with size 100.

note

"consolas" is the builtin font in REGL JS. If you use the minimal REGL JS version, there is no such font and you need to load your own font.

`LayerView` is a type sugar to represent the `view` type of layer.

```
type alias LayerView cdata userdata data =  
    Env cdata userdata -> data -> Renderable  

```

It will expand to

```
Env SceneCommonData UserData -> Data -> Renderable  

```

`Env` is a type that represents the *environment*. Layers and components can not only update its own data, it can also view and update the environment (aka. *side effects*).

Its definition is:

```
type alias Env common userdata =  
    { globalData : GlobalData userdata  
    , commonData : common  
    }  

```

`GlobalData` is a type that Messenger keeps track of all the time. It has some key information Messenger needs to use like the screen size.

`commonData` is the data shared among all the layers in a scene. It is defined in `Scenes/Home/SceneBase.elm:SceneCommonData`.
Users could customize it for each scene.

Let's take a closer look at `GlobalData`.

```
type alias GlobalData userdata =  
    { internalData : InternalData  
    , sceneStartTime : Float  
    , globalStartTime : Float  
    , globalStartFrame : Int  
    , sceneStartFrame : Int  
    , currentTimeStamp : Float  
    , windowVisibility : Visibility  
    , mousePos : ( Float, Float )  
    , pressedMouseButtons : Set Int  
    , pressedKeys : Set Int  
    , extraHTML : Maybe (Html WorldEvent)  
    , canvasAttributes : List (Html.Attribute WorldEvent)  
    , volume : Float  
    , userData : userdata  
    , currentScene : String  
    }  

```

Global data won't be reset if users change the scene.

- `globalStartFrame` records the past frames number since the game started
- `globalStartTime` records the past time since the game started, in milliseconds
- `sceneStartFrame` records the past frames number since this scene started
- `sceneStartTime` records the past time since this scene started, in milliseconds
- `userdata` records the data that users set to save
- `extraHTML` is used to render extra HTML tags. Be careful to use this
- `windowVisibility` records whether users stay in this tab/window
- `pressedKeys` records the keycodes that are be pressed now
- `pressedMouseButtons` records the mouse buttons that are pressed now
- `volume` records the volume of the game
- `currentScene` records the current scene name
- `mousePos` records the mouse position, in virtual coordinate

tip

Since the `globalStartTime` and `sceneStartTime` are float numbers, please use a range rather than a specific time point when judging the time.

Now, run `make` to build the game, and use `elm reactor` or other static file hosting tools (If you use VS Code, you can try using the [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer)), but **DO NOT** directly open the HTML file in the browser because assets won’t be loaded due to [CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS).

We use coordinate `(0, 0)` to render the text instead of using HTML tags. This coordinate is not the real pixels on the screen, but the **virtual coordinate** in the game.

The virtual resolution is 1920×10801920 \times 10801920×1080 by default, and the real resolution is determined by the browser window size. The virtual size is defined in `MainConfig.elm`, users may change it to whatever they like.

`P.textbox` uses a builtin REGL program that renders the text.