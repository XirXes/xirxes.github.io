---
layout: post
title:  "GTA San Andreas - Xiyl's Recommended Modlist"
---
[![CJ enjoying an LS sunrise](/assets/img/SA-Modded-small.jpg)](https://www.xiyl.cc/assets/img/SA-Modded-full.jpg)

Modded with the aim of enhanced vanilla gameplay, only fidelity and functionality improvements made. Built around Silent Patch, Widescreen fix, and Ginput. You could have a great experience with just those 3, but this list includes a high quality map fixes patch, Project2DFX for enhanced lighting, quite a few small settings tweaks, improved asset streaming and PAE memory address mapping, with modloader ensuring it all works together. I'm documenting my setup here to preserve my prefered version of the game.

Why not use Definitive Edition? Simply put, I don't like the look. But beyond that, the changes to the game camera bother me, especially the flight camera being stuck without any tilt, always locked on the horizon. A change made for the ancient mobile ports that should have been reversed for the modern releases. The car chase camera is awful too, I'm not a fan of handling drive-by controls that way.

Download the Steam version (NOT DEFINITIVE), and use a tool to downgrade to 1.0 to restore music and ensure mods are compatible.
[GTASA Open Downgrader](https://github.com/xxanqw/gtasa-open-downgrader)
or
[Steam Community Guide](https://steamcommunity.com/sharedfiles/filedetails/?id=3036381821)

When installing the mods, I keep the low level mods out of modloader. This means the base game filesystem will have some extra files for CLEO5, and GInput, see the example filesystem below.


Modlist
-------

- [CLEO5](https://github.com/cleolibrary/CLEO5/releases) - includes Silent ASI Loader
- [Silent ASI Loader](https://silentsblog.com/mods/gta-sa/#asiloader) - just use CLEO5's version
    - alt: [GTAmodding Github](https://github.com/GTAmodding/ASI-Loader)
    - alt: [Ultimate ASI Loader (doesn't work well with modloader IMO)](https://github.com/ThirteenAG/Ultimate-ASI-Loader)
- [Silent Patch 2026](https://silentsblog.com/2026/07/31/silentpatch-2026-update/)
    - [Download](https://silentsblog.com/2026/07/31/silentpatch-2026-update/#download)
        - [Setup Instructions](https://silentsblog.com/setup-instructions/) - includes Proton guidance
- [Modloader](https://github.com/thelink2012/modloader/releases)
- [GInput](https://silentsblog.com/mods/gta-sa/#ginput)
- [Widescreen Fixes](https://fusionfix.io/wfp#gtasa)
    - Click down arrow, choose Developer build (untested)
- [Skip Device Selection Window](https://www.gtagarage.com/mods/show.php?id=27863) - An essential part of a balanced controller only experience
- [Windowed Mode](https://github.com/ThirteenAG/III.VC.SA.WindowedMode) - Prevents alt-tab crashes, improves Linux compatibility
- [Large Address Aware](https://www.mixmods.com.br/2016/09/iii-vc-sa-largeaddress-reconhecer-3-4-gb-de-ram/)
    - alt: [Universal 32bit PAE patcher](https://www.techpowerup.com/forums/threads/large-address-aware.112556/)
- [FramerateVigilante](https://www.mixmods.com.br/2022/08/iii-vc-sa-framerate-vigilante/)
- [MixSets](https://www.mixmods.com.br/2022/03/sa-mixsets/)
- [Project2DFX](https://www.mixmods.com.br/2020/02/sa-project2dfx/) - Widescreen Fix Dev build required for compatibility
- [skygfx](https://www.mixmods.com.br/2024/03/sa-skygfx/)
    - [Original source](https://github.com/aap/skygfx/releases)
- [Improved Streaming](https://www.mixmods.com.br/2026/07/improved-streaming/)
- [Open Limit Adjuster](https://www.mixmods.com.br/2022/10/open-limit-adjuster/)
- [Proper Fixes](https://www.mixmods.com.br/2022/03/sa-proper-fixes/)
    - Requires Modloader, Skygfx (or Proper Shaders, not recommended), Open Limit Adjuster, Improved Streaming, and Large Address patch


Config Changes
--------------

Many of these mods don't need any changes, but I customize a few for the best experience, or to ensure compatibility between mods.

- SilentPatch
`scripts/SilentPatchSA.ini`
```
DirectionalFromSun=0
```

- GInput - change to ControlsSet 2 for modern controls with Gas/Brake on triggers.
`scripts/GInputSA.ini`
```
ControlsSet=2
```

- Widescreen Fix
`scripts/GTASA.WidescreenFix.ini`
```
NoCutsceneBorderAnimation = 1
ReplaceTextShadowWithOutline = 2
```

- Modloader - can be adjusted manually in game. 
`modloader\modloader.ini`
```
[Profiles.Default.Priority]
mixsets = 63
open limit adjuster = 65
proper fixes = 70
silentpatch = 49
skygfx = 80
```
Intended load order
    1. Skygfx
    2. Proper Fixes
    3. Open Limit Adjuster
    4. Mix Sets
    5. Everything Else
    6. Silent Patch - This loads last to ensure it's fixes override other mods.

- MixSets - Most of these are just commenting out settings with a # to enforce the games original behavior. Season to taste.
`modloader\MixSets\MixSets.ini`
```
RandWheelDettach     = 0
#VehBurnEngineBroke   = 1
#NoPedVehDive         = 1
#VehCamHeightOffset   = 0.4
NoPauseWhenUnfocus   = 1
#WheelTurnSpeed       = 0.1
#BrakeMin             = 0.2
HeliRotorSpeed       = 0.22
UseHighPedShadows    = 1
#NoFireCoronas        = 1  
NoVolumetricClouds   = 0
#TaxiLights           = 1
NoMoneyZeros         = 0 
```

- Skygfx - Don't bother with the extra ini, you just need the first one. Must be set for compatibility with Proper Fixes.
`modloader\skygfx\skygfx1.ini`
```
ps2Modulate=2
colorFilter=PS2
doRadiosity=1
neoWaterDrops=0
```


Filesystem list
---------------

Excluding base game files. Steam launches gta-sa.exe

```console
├── bass.dll
├── cleo
│   ├── cleo_modules
│   ├── cleo_plugins
│   │   ├── SA.Audio.cleo
│   │   ├── SA.DebugUtils.cleo
│   │   ├── SA.FileSystemOperations.cleo
│   │   ├── SA.GameEntities.cleo
│   │   ├── SA.IniFiles.cleo
│   │   ├── SA.Input.cleo
│   │   ├── SA.Math.cleo
│   │   ├── SA.MemoryOperations.cleo
│   │   └── SA.Text.cleo
│   ├── cleo_saves
│   │   ├── cs0.sav
│   │   └── cs1.sav
│   └── cleo_text
├── CLEO.asi
├── cleo.log
├── cleo_readme
│   ├── ASI Loader Readme.txt
│   ├── Changelog.html
│   ├── examples
│   │   ├── Audio_Demo.txt
│   │   ├── Check_CLEO_Version.txt
│   │   ├── CLEO_Sound_Button.txt
│   │   ├── Color_Blend.txt
│   │   ├── Free_ID_Lister.txt
│   │   ├── Homie_Help.txt
│   │   ├── Limits_Info.txt
│   │   ├── Mission_Trigger.txt
│   │   ├── Pickup_Shirt.txt
│   │   ├── Screen_Drawing.txt
│   │   ├── Skin_Selector.txt
│   │   ├── Sounds_Browser.txt
│   │   ├── Train_Spawner.txt
│   │   └── Vehicle_Flags.txt
│   └── Readme.html
├── docs
│   ├── cheat_list_ps3.html
│   ├── cheat_list_xbox.html
│   └── GAME CONTROLS FULL LIST.txt
├── eax.dll
├── gta-sa.exe
├── gta_sa.exe
├── gta-sa.exe.bak
├── gta_sa.exe.bak
├── installscript.vdf
├── largeaddress.exe
├── models
│   ├── Mobile_details.txd
│   ├── particle.txd
│   ├── pcbtns.txd
│   ├── player.img
│   ├── ps3btns.txd
│   ├── sixaxis.txd
│   ├── texdb.txt
│   └── x360btns.txd
├── modloader
│   ├── FramerateVigilante
│   │   ├── FramerateVigilante.ini
│   │   └── FramerateVigilante.SA.asi
│   ├── Improved Streaming
│   │   ├── ImprovedStreaming.ini
│   │   ├── ImprovedStreaming.log
│   │   └── ImprovedStreaming.SA.asi
│   ├── MixSets
│   │   ├── MixSets.asi
│   │   ├── MixSets.ini
│   │   └── MixSets.log
│   ├── modloader.ini
│   ├── modloader.log
│   ├── Open Limit Adjuster
│   │   ├── III.VC.SA.LimitAdjuster.asi
│   │   └── III.VC.SA.LimitAdjuster.ini
│   ├── Project2DFX
│   │   ├── SALodLights.asi
│   │   ├── SALodLights.dat
│   │   └── SALodLights.ini
│   ├── Proper Fixes
│   │   ├── Additional Models
│   │   │   ├── Loader.txt
│   │   │   ├── ProperFixes.ide
│   │   │   ├── ProperFixes.ipl
│   │   │   └── Stream
│   │   │       └── ProperFixes.col
│   │   ├── Additional Textures
│   │   │   ├── Loader.txt
│   │   │   ├── lodproperf_country.txd
│   │   │   ├── lodproperf_la.txd
│   │   │   ├── lodproperf_sf.txd
│   │   │   ├── lodproperf_vegas.txd
│   │   │   ├── neontex.txd
│   │   │   ├── pf_nitelites.txd
│   │   │   ├── properf_country.txd
│   │   │   ├── properf_cutscene.txd
│   │   │   ├── properf_dynamic.txd
│   │   │   ├── properf_int.txd
│   │   │   ├── ProperFixesTXDP.ide
│   │   │   ├── properf_la.txd
│   │   │   ├── properf_peds.txd
│   │   │   ├── properf_sf.txd
│   │   │   └── properf_vegas.txd
│   │   ├── Avery and Candy neon and anim
│   │   │   ├── vegascowboy1.dff
│   │   │   ├── vegascowboy3.dff
│   │   │   ├── vegcandysign1.dff
│   │   │   └── vgnfremntsgn.txd
│   │   ├── cutscene.img
│   │   ├── cuts.img
│   │   ├── gta3.img
│   │   ├── gta_int.img
│   │   ├── Increased Vegetation Distance
│   │   │   └── data
│   │   │       ├── maps
│   │   │       │   ├── generic
│   │   │       │   │   ├── procobj.ide
│   │   │       │   │   └── vegepart.ide
│   │   │       │   ├── loader.txt
│   │   │       │   ├── procobj1.ipl
│   │   │       │   ├── procobj2.ipl
│   │   │       │   ├── procobj3.ipl
│   │   │       │   ├── procobj4.ipl
│   │   │       │   ├── procobj5.ipl
│   │   │       │   └── procobj6.ipl
│   │   │       └── procobj.dat
│   │   ├── LOD Vegetation
│   │   │   ├── Loader.txt
│   │   │   ├── LODvegetation.col
│   │   │   ├── LODvegetation.ide
│   │   │   ├── LODvegetation.txd
│   │   │   ├── LOD Vegetation.url
│   │   │   └── original replace
│   │   │       ├── lod_redwoodgrp.dff
│   │   │       └── lod_vbg_fir_co.dff
│   │   ├── Map
│   │   │   └── data
│   │   │       └── maps
│   │   │           ├── country
│   │   │           │   ├── countn2.ide
│   │   │           │   ├── countN2.IPL
│   │   │           │   ├── countrye.ide
│   │   │           │   ├── countryE.ipl
│   │   │           │   ├── countryN.ide
│   │   │           │   ├── countryN.IPL
│   │   │           │   ├── countryS.ide
│   │   │           │   ├── countrys.IPL
│   │   │           │   ├── countryW.ide
│   │   │           │   ├── countryW.IPL
│   │   │           │   └── counxref.ide
│   │   │           ├── cull.ipl
│   │   │           ├── generic
│   │   │           │   ├── barriers.ide
│   │   │           │   ├── dynamic2.ide
│   │   │           │   ├── dynamic.ide
│   │   │           │   ├── multiobj.ide
│   │   │           │   ├── procobj.ide
│   │   │           │   └── vegepart.ide
│   │   │           ├── interior
│   │   │           │   ├── gen_int1.ipl
│   │   │           │   ├── gen_int3.ide
│   │   │           │   ├── gen_int5.ide
│   │   │           │   ├── gen_intb.ide
│   │   │           │   ├── int_LA.ide
│   │   │           │   ├── int_LA.IPL
│   │   │           │   ├── int_sf.ide
│   │   │           │   ├── int_SF.ipl
│   │   │           │   ├── int_veg.ide
│   │   │           │   ├── int_veg.ipl
│   │   │           │   ├── propext.ide
│   │   │           │   ├── props2.ide
│   │   │           │   ├── props.ide
│   │   │           │   ├── stadint.ide
│   │   │           │   └── stadint.ipl
│   │   │           ├── LA
│   │   │           │   ├── LAe2.ide
│   │   │           │   ├── LAe2.IPL
│   │   │           │   ├── LAe.ide
│   │   │           │   ├── LAe.ipl
│   │   │           │   ├── LAhills.ide
│   │   │           │   ├── LAhills.IPL
│   │   │           │   ├── LAn2.ide
│   │   │           │   ├── LAn2.IPL
│   │   │           │   ├── LAn.ide
│   │   │           │   ├── LAn.ipl
│   │   │           │   ├── LAs2.ide
│   │   │           │   ├── LAs2.IPL
│   │   │           │   ├── LAs.ide
│   │   │           │   ├── LAs.IPL
│   │   │           │   ├── LAw2.ide
│   │   │           │   ├── LAw2.ipl
│   │   │           │   ├── LAw.ide
│   │   │           │   ├── LAw.IPL
│   │   │           │   ├── LaWn.ide
│   │   │           │   ├── LAwn.IPL
│   │   │           │   └── LAxref.ide
│   │   │           ├── leveldes
│   │   │           │   ├── levelmap.ide
│   │   │           │   ├── levelmap.ipl
│   │   │           │   └── levelxre.ide
│   │   │           ├── occluint.ipl
│   │   │           ├── occluLA.ipl
│   │   │           ├── occlusf.ipl
│   │   │           ├── occluveg.ipl
│   │   │           ├── SF
│   │   │           │   ├── SFe.ide
│   │   │           │   ├── SFe.IPL
│   │   │           │   ├── SFn.ide
│   │   │           │   ├── SFn.IPL
│   │   │           │   ├── SFSe.ide
│   │   │           │   ├── SFse.IPL
│   │   │           │   ├── SFs.ide
│   │   │           │   ├── SFs.IPL
│   │   │           │   ├── SFw.ide
│   │   │           │   ├── SFw.IPL
│   │   │           │   └── SFxref.ide
│   │   │           └── vegas
│   │   │               ├── vegasE.ide
│   │   │               ├── vegasE.ipl
│   │   │               ├── VegasN.ide
│   │   │               ├── vegasN.IPL
│   │   │               ├── VegasS.ide
│   │   │               ├── vegasS.IPL
│   │   │               ├── VegasW.ide
│   │   │               ├── vegasW.ipl
│   │   │               ├── vegaxref.ide
│   │   │               └── vegaxref.ipl
│   │   ├── Misc
│   │   │   ├── data
│   │   │   │   ├── furnitur.dat
│   │   │   │   ├── object.dat
│   │   │   │   ├── plants.dat
│   │   │   │   ├── procobj.dat
│   │   │   │   └── water.dat
│   │   │   └── Grass Color Fix.url
│   │   ├── Pleasure Domes neon
│   │   │   ├── lodp_sfw35.dff
│   │   │   ├── pdomes_neon.dff
│   │   │   ├── Pleasure Domes neon.ipl
│   │   │   ├── Pleasure Domes neon Loader.txt
│   │   │   └── temp_sfw35.dff
│   │   ├── ProperFixes.asi
│   │   ├── Proper Fixes (latest version).url
│   │   ├── PS2 Grass
│   │   │   └── models
│   │   │       └── grass
│   │   │           ├── grass0_1.dff
│   │   │           ├── grass0_2.dff
│   │   │           ├── grass0_3.dff
│   │   │           ├── grass0_4.dff
│   │   │           ├── grass1_1.dff
│   │   │           ├── grass1_2.dff
│   │   │           ├── grass1_3.dff
│   │   │           ├── grass1_4.dff
│   │   │           ├── grass2_1.dff
│   │   │           ├── grass2_2.dff
│   │   │           ├── grass2_3.dff
│   │   │           ├── grass2_4.dff
│   │   │           ├── grass3_1.dff
│   │   │           ├── grass3_2.dff
│   │   │           ├── grass3_3.dff
│   │   │           ├── grass3_4.dff
│   │   │           └── plant1.dff
│   │   ├── Race maps
│   │   │   └── models
│   │   │       └── txd
│   │   │           ├── LD_RCE1.txd
│   │   │           ├── LD_RCE2.txd
│   │   │           ├── LD_RCE3.txd
│   │   │           ├── LD_RCE4.txd
│   │   │           └── LD_RCE5.txd
│   │   └── SA Optimized Map
│   │       ├── gta.dat.txt
│   │       ├── SA Optimized Map.ide
│   │       └── SA Optimized Map.url
│   └── skygfx
│       ├── data
│       │   └── colorcycle.dat
│       ├── neo
│       │   ├── carTweakingTable.dat
│       │   └── neo.txd
│       ├── skygfx1.ini
│       └── skygfx.asi
├── neo
│   ├── carTweakingTable.dat
│   └── neo.txd
├── ogg.dll
├── scripts
│   ├── GInputSA.asi
│   ├── GInputSA.ini
│   ├── GTASA.WidescreenFix.asi
│   ├── GTASA.WidescreenFix.ini
│   ├── III.VC.SA.WindowedMode.asi
│   ├── III.VC.SA.WindowedMode.ini
│   ├── modloader.asi
│   ├── SilentPatchSA.asi
│   ├── SilentPatchSA.ini
│   └── SkipDeviceSelection.asi
├── vorbis.dll
├── vorbisFile.dll
└── vorbisHooked.dll
```

