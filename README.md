# DSP Mods
Repo with source code for my mods. Also contains a mini guide on custom machine meshes and animations; registering custom items, recipes, etc; adding custom UI.

If you want to support my work you can [donate](https://paypal.me/kremnev8).

Check [Registry Tool](https://github.com/kremnev8/DSP-Mods/tree/master/Mods/Tools) out. It is useful to quickly create new items, recipes, techs, etc.

In the [Unity](https://github.com/kremnev8/DSP-Mods/tree/master/Unity) folder you can find needed scripts and files to create your own buildings, and custom UI. 

Scripts:
* ExportAssetBundles script is used to force unity to build asset bundles. 
* BetterMeshDataAsset makes sure that if you open MeshDataAsset in inspector nothing will break(Also is used to bake mesh data from Mesh object). 
* AnimationBakerWindow is the baker.
* EditorObjExporter can export unity meshes to obj file(Optional)
* FixPrefabMeshes can POTENTIALLY(Always have a backup, just in case) fix some prefabs to be useful for baking animations. You will need to have all meshes used in game with their names intact imported in your project. Also you might need to fix prefab a bit after that. Unfortunately, it VERY likely will crash unity, so make sure to save everything before that happens.(Optional)
* AssetRiddanceHelper script removes and adds textures, font, etc to help share prefabs without sharing ingame assets. Uses AssetMemory class to store its data.

Shaders and materials:
* text-alpha and widget-alpha shaders. These shaders were reverse engineered from original shaders and are used to make certain text and images glow. They only have only a few parameters: `_Multiplier`(default 5), `_AlphaPower`(default 2.2), `_Sharp`(default 1). I'm not particularly certain what these parameters do.

Prefabs:
* template prefab contains a bunch of different UI elements that are used frequently in ingame UIs. In order to use it you will need to use asset reasigner(Window->DSP Tools->Reassign assets). Make sure you imported all needed assets in your project. This prefab also uses some custom textures make by me(Find them in unity folder). Note that out of these elements dropdown is not from game, I made it completely from scratch since no machines ingame used a dropdown.

## How to start creating and importing custom assets into DSP
This guide assumes you know BepInEx and have a working project for it. If you don't first do [this](https://bepinex.github.io/bepinex_docs/master/articles/dev_guide/plugin_tutorial/index.html#sidetoggle).
1. Create unity project and import Assembly-CSharp into your project to be able to reference DSP code in scripts. You can also try [ThunderKit](https://github.com/PassivePicasso/ThunderKit) to automate some steps. Please note that using ThunderKit is not mandatory
3. Open Assembly-CSharp in inspector and make sure that is does NOT use auto reference 
4. Extract or create needed assets(Models, animations, prefabs, etc)
5. Fix extracted prefab so that there is no missing scripts and all meshes and materials(Although i'm still unable to compile ingame's shaders) are there
6. If you intent to use prefab ingame you also need to properly setup all needed description scripts(Like BuildConditionConfig, SlotConfig, etc). Game uses these scripts to figure out what is what and where. If you are unsure how to set them up, try using [RuntimeUnityEditor](https://github.com/ManlyMarco/RuntimeUnityEditor) and [LDBTool](https://dsp.thunderstore.io/package/xiaoye97/LDBTool/)'s utility to explore Proto definitions.
7. Make sure that animation clip works, by dragging fixed prefab into preview window(It should animate it)
8. Open baker (Window->DSP Tools->Verta Animation Baker) and select prefabs root, enter name and hit bake. You will get MeshDataAsset and .verta file. Both are needed to make this work
9. Make sure you correctly define names and references to two created files in LODModelDesc script
10. Create new Aseet Bundle and add all needed assets to it(You cannot add .verta file, becuse it won't let you). Then build Asset Bundle (Window->DSP Tools->Build AssetBundle)
11. Write code and import everything in. You can see examples of how to do that in this repo

Project view:

![Project view](https://i.imgur.com/RULexSP.png)

UI Template prefab:

![Template](https://i.imgur.com/WqDMmfF.png)

## Installation of example mod
1. Download and unpack [BepInEx](https://github.com/BepInEx/BepInEx/releases) into game root directory
2. Download and install [LDBTool](https://dsp.thunderstore.io/package/xiaoye97/LDBTool/)
3. Download and install [DSP_CustomBuildings](https://github.com/kremnev8/DSP_CustomBuildings/releases)
