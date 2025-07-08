---
title: "SOM Calls | Messenger Docs"
source: downloaded_docs\docs\misc\som
---

On this page

# SOM Calls

`SOMMsg`s are low-level APIs (like system calls in OS) that can directly interact with the core. Users can send `SOMMsg` in any general model.

## `SOMChangeScene`[​](#somchangescene "Direct link to somchangescene")

**Definition:** `SOMChangeScene ( Maybe scenemsg ) String`

This message is used to change to another scene. Users need to provide the scene init data and the scene name.

## `SOMPlayAudio`[​](#somplayaudio "Direct link to somplayaudio")

**Definition:** `SOMPlayAudio Int String AudioOption`

This message is used to play an audio. It has three parameters: channel ID, audio name, and audio option. The channel ID is where this audio will be played. There might be multiple audios playing on the same channel. Audio name is what users define in the keys of `allAudio`.

See [Audio Basics](/docs/audio/basics) for more details.

## `SOMStopAudio`[​](#somstopaudio "Direct link to somstopaudio")

**Definition:** `SOMStopAudio AudioTarget`

Stops a playing audio stream.

See [Audio Basics](/docs/audio/basics) for more details.

## `SOMTransformAudio`[​](#somtransformaudio "Direct link to somtransformaudio")

**Definition:** `SOMTransformAudio AudioTarget (Audio -> Audio)`

Transforms the audio on the fly.

See [Audio Transformation](/docs/audio/transform) for more details.

## `SOMAlert`[​](#somalert "Direct link to somalert")

**Definition:** `SOMAlert String`

This message is used to show an alert. The parameter is the content of the alert.

## `SOMPrompt`[​](#somprompt "Direct link to somprompt")

**Definition:** `SOMPrompt String String`

This message is used to show a [prompt](https://developer.mozilla.org/en-US/docs/Web/API/Window/prompt). Users can use this to get text input from the user. The first parameter is the name of the prompt, and the second parameter is the title of the prompt.

When the user clicks the OK button, user code will receive a `Prompt String String` message. The first parameter is the name of the prompt, and the second parameter is the user’s input.

## `SOMSetVolume`[​](#somsetvolume "Direct link to somsetvolume")

**Definition:** `SOMSetVolume Float`

This message is to change the volume. It should be a value in [0,1][0, 1][0,1]. Users could use a larger value but it will sound noisy.

## `SOMSaveGlobalData`[​](#somsaveglobaldata "Direct link to somsaveglobaldata")

**Definition:** `SOMSaveGlobalData`

Save global data (including user data) to local storage.

See [Local Storage](/docs/advanced/localstorage).

## `SOMGCLoad`, `SOMGCUnload`, `SOMCallGC`[​](#somgcload-somgcunload-somcallgc "Direct link to somgcload-somgcunload-somcallgc")

**Definition:** `SOMLoadGC (GlobalComponentStorage userdata scenemsg)`

**Definition:** `SOMUnloadGC GCTarget`

**Definition:** `SOMCallGC (List ( GCTarget, GCMsg ))`

See [Global Component](/docs/advanced/gc).

## `SOMChangeFPS`[​](#somchangefps "Direct link to somchangefps")

**Definition:** `SOMChangeFPS REGL.TimeInterval`

Change FPS on the fly.

## `SOMLoadResource`[​](#somloadresource "Direct link to somloadresource")

**Definition:** `SOMLoadResource String ResourceDef`

Dynamically load a resource at runtime. See [Dynamic Asset Loading](/docs/advanced/assetload).

## Game Configurations[​](#game-configurations "Direct link to Game Configurations")

Users may want to change the settings in `MainConfig.elm` to match their demand. This section explains what each option in that configuration file means.

- `initScene`: The first scene users will see when starting the game
- `initSceneMsg`: The message to start the first scene
- `virtualSize`: The virtual drawing size. Users may use whatever they like but think carefully about the ratio (Support 4:3 or 16:9 screens)
- `debug`: A debug flag. If turned on, users can press `F1` to change to a scene quickly and press `F2` to change volume at any time in the game
- `background`: The background users see. Default is a transparent background
- `timeInterval`: The update strategy. See [Tick Event](/docs/event/tick)
- `initGlobalData` and `saveGlobalData`: See [Local Storage](/docs/advanced/localstorage)
- `fboNum`: Number of FBOs to enable at start.
- `enabledBuiltinPrograms`: Builtin REGL programs enabled at the beginning of the game.

- [`SOMChangeScene`](#somchangescene)
- [`SOMPlayAudio`](#somplayaudio)
- [`SOMStopAudio`](#somstopaudio)
- [`SOMTransformAudio`](#somtransformaudio)
- [`SOMAlert`](#somalert)
- [`SOMPrompt`](#somprompt)
- [`SOMSetVolume`](#somsetvolume)
- [`SOMSaveGlobalData`](#somsaveglobaldata)
- [`SOMGCLoad`, `SOMGCUnload`, `SOMCallGC`](#somgcload-somgcunload-somcallgc)
- [`SOMChangeFPS`](#somchangefps)
- [`SOMLoadResource`](#somloadresource)
- [Game Configurations](#game-configurations)