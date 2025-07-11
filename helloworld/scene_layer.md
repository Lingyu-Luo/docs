---
title: "Scenes and Layers | Messenger Docs"
source: downloaded_docs\docs\helloworld\scene_layer
---

On this page

# Scenes and Layers

## Scenes[​](#scenes "Direct link to Scenes")

A scene is a period of time in the game. Users could interact with the users and even implement the whole logic in one scene.

Every scene has its own common data, message types that share among all layers or components in the scene.

Usually when we design games we need at least three scenes:

- Starting scene
- Game level
- Ending scene

Each scene has completely different data and effects so it is useful to have different scenes.

tip

If there are more game levels and all of them are similar, [scene prototype](/docs/sproto) is the best choice.

### Raw Scene[​](#raw-scene "Direct link to Raw Scene")

There are two builtin types of scene: *raw scene* and *layered scene*.

A raw scene, as the name suggests, is literally a scene with no layers and no components (you could add them afterwards).

```
type alias Data =  
    {}  
  
init : RawSceneInit Data UserData SceneMsg  
init env msg =  
    {}  
  
update : RawSceneUpdate Data UserData SceneMsg  
update env msg data =  
    ( data, [], env )  
  
view : RawSceneView UserData Data  
view env data =  
    REGL.empty  

```

To define the model of a raw scene, users only need to specify the data and three main functions (`init`, `update` and `view`).

### Layered Scene[​](#layered-scene "Direct link to Layered Scene")

A layered scene is a raw scene with layers as its data. Layers could help users separate logic from different components.
The rule of thumb is to divide a scene into several **independent** (or at least mostly independent) parts. For example, the game objects have little to do with the settings panel. They have mostly independent logic.

Messenger will generate a layered scene model like this:

```
commonDataInit : Env () UserData -> Maybe SceneMsg -> SceneCommonData  
commonDataInit _ _ =  
    {}  
  
init : LayeredSceneInit SceneCommonData UserData LayerTarget LayerMsg SceneMsg  
init env msg =  
    let  
        cd =  
            commonDataInit env msg  
  
        envcd =  
            addCommonData cd env  
    in  
    { renderSettings = []  
    , commonData = cd  
    , layers =  
        []  
    }  
  
settings : LayeredSceneEffectFunc SceneCommonData UserData LayerTarget LayerMsg SceneMsg  
settings _ _ _ =  
    []  

```

The main configuration here is the `layer` field in the `init` function. We will see how to add a layer to a scene later.

## Layers[​](#layers "Direct link to Layers")

Messenger will generate a template for layer like this:

```
type alias Data =  
    {}  
  
init : LayerInit SceneCommonData UserData LayerMsg Data  
init env initMsg =  
    {}  
  
update : LayerUpdate SceneCommonData UserData LayerTarget LayerMsg SceneMsg Data  
update env evt data =  
    ( data, [], ( env, False ) )  
  
updaterec : LayerUpdateRec SceneCommonData UserData LayerTarget LayerMsg SceneMsg Data  
updaterec env msg data =  
    ( data, [], env )  
  
view : LayerView SceneCommonData UserData Data  
view env data =  
    REGL.empty  

```

This is very similar to the raw scene except that the `update` function returns an additional boolean value which is a `block` value.
See [event](/docs/event) to learn how to use it.

Later in the tutorials users will learn the components. A layer may contain many components just like a scene may contain many layers. When users decide to use layers with components, the generated model will be slightly rivised to make it easier for users to manage components.

Users may need to handle `Parent` messages from components in a layer. Messenger provides a handy function `handleComponentMsgs` which is defined in `Messenger.Layer.Layer`, to help users handle those messages. Users need to provide a `MsgBase` handler, for example:

```
handleComponentMsg : Handler Data SceneCommonData UserData Target LayerMsg SceneMsg ComponentMsg  
handleComponentMsg env compmsg data =  
    case compmsg of  
        SOMMsg som ->  
            ( data, [ Parent <| SOMMsg som ], env )  
  
        OtherMsg _ ->  
            ( data, [], env )  
  
        _ ->  
            ( data, [], env )  

```

Then users can combine it with `updateComponents` to define the `update` function in layers (provided in the Messenger template):

```
update : LayerUpdate SceneCommonData UserData LayerTarget LayerMsg SceneMsg Data  
update env evt data =  
    let  
        ( comps1, msgs1, ( env1, block1 ) ) =  
            updateComponents env evt data.components  
  
        ( data1, msgs2, env2 ) =  
            handleComponentMsgs env1 msgs1 { data | components = comps1 } [] handleComponentMsg  
    in  
    ( data1, msgs2, ( env2, block1 ) )  

```

tip

At this stage, components are not necessarily required, so don’t worry if this seems confusing. The interaction between layers and components will be explained in detail in later chapters.

## Hello World[​](#hello-world "Direct link to Hello World")

Now, create a new layered scene and add a layer in that scene:

```
# Open our project directory  
cd helloworld  
# Create a new scene  
messenger scene Home  
# Create a new layer called MainLayer  
messenger layer Home MainLayer  

```

note

If the scene name is not "Home", change the scene name in `initScene` in `MainConfig.elm` (which defines which scene to start), as it is set to "Home" by default.

note

It is fine to use lowercase letters like `home` and `mainLayer`. The Messenger CLI will automatically convert these to appropriate names.

tip

By default, a scene is a `LayeredScene`. To create a `RawScene` without any layers, add the `--raw` argument when creating a scene. A raw scene doesn't include `SceneBase.elm` when created. However, if users try to add a component or a layer to a raw scene later, that file will automatically be created.

Similarly, layers are created without the use of components by default. To generate a layer with components, add the `-c` or `--with-component` argument when creating the layer. If no components exist in the scene, a `Components/` directory containing the `ComponentBase.elm` file will be created automatically.

The functionality of each Elm file created by the template will be explained later.

- [Scenes](#scenes)
  - [Raw Scene](#raw-scene)
  - [Layered Scene](#layered-scene)
- [Layers](#layers)
- [Hello World](#hello-world)