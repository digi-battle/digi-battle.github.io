---
name: "First Game Project with Easy FPS Editor" 
title: "First Game Project with Easy FPS Editor" 
layout: blogpost
tags: GAME-DEV EFPSE
---

![Gameplay demo of my Spooky's Jump Scare Mansion clone made with EFPSE](https://raw.githubusercontent.com/wiredjohn/EFPSE-Spookys-Jump-Scare-Mansion/main/.github/images/demo.webp)

This month, I finished my first real game project using the engine [EFPSE](https://cg8516.itch.io/easyfpseditor-ce).

I've played around with the editor before and it lives up to the name. It really is easy to have a basic game up and running in minutes. 

Recently I've been inspired to open it up again after watching some YouTube tutorials from [TJ's Creationkit](https://www.youtube.com/@Creationkitnz), [Mikulu Games](https://www.youtube.com/channel/UC1HzDT-eewPYEEFfrKbMYtw) and a number of other developers.

Before planning out a "*real*" project I decided to make a test game to get more familiar with the engine. So I made a clone of [Spooky's Jump Scare Mansion](https://store.steampowered.com/app/356670/Spookys_Jump_Scare_Mansion/).

It's completely open source:
- [Project files on GitHub](https://github.com/wiredjohn/EFPSE-Spookys-Jump-Scare-Mansion).
- [Compiled game .exe on GitHub](https://github.com/wiredjohn/EFPSE-Spookys-Jump-Scare-Mansion/releases/download/v1.0.0/SJM.zip)

I won't talk too much about the project here because I've already written a lot in the project README and the script files are all commented if you're interested in understanding how particular features work.


## Lessons Learned

I like EFPSE a lot. It's simple and flexible enough to implement most features I've thought about for potential projects.

It's just *easy* straight out the box. And with a growing community of game devs making tutorials on YouTube, I expect to see more and more people picking up the engine.

That being said - there are drawbacks.

The engine is no longer being actively developed. I think the original dev handed the project over to the current maintainer, but they are no longer making releases beyond some [bugfixes](https://github.com/CG8516/DumpingGround/tree/main/EFPSE_DEVBUILDS). But they are working on [another engine](https://cg8516.itch.io/ezgb) which could be a good alternative when it's ready.

Because of this, I don't expect any of the problems I faced to be fixed any time soon. Some of the issues can be ignored but others make development not so easy.

I'm going to list them here more for my own reference than anything else:

- Script files for all objects (maps, enemies, decorations) get saved to the same /Scripts folder, which can get ugly quick. I got around this with namespaces. E.g. all maps are prefixed "map_", enemies "enemy_" etc.
- Variable name can't contain the name of another variable, e.g. "player_speed" and "player_speed_slowed" won't work. If "player_speed" = 100, any reference to "player_speed_slowed" will be interpreted as "100_slowed". 
- No way to get entity (enemy/decoration) positions without hardcoding them. Check out my [trigger_specimen2.script](https://github.com/wiredjohn/EFPSE-Spookys-Jump-Scare-Mansion/blob/main/Scripts/trigger_specimen_2.script) to see my full process of trying to work around this.
- Can't set default settings used for all Maps. I made a [script to automate this](https://github.com/wiredjohn/EFPSE-Spookys-Jump-Scare-Mansion/tree/main/_Tools/CreateMapScripts) because it annoyed me.
- Map changes use map index rather than a map name, so projects with lots of maps or non-linear progression get ugly.
- Scripting has no data structures.
- No "else if" statement, only "if" then "else".
- Map "_loop" scripts run as soon as map goto/map next is called, which means it starts running WHILE THE LEVEL TRANSITION IS HAPPENING! (the fade to black on map change). This means any calls to player check position in this window will return the position of the player at the map change trigger, rather than the player at the next maps starting position.
- Running player check position on map.script always returns 0 0 0 - suggesting that the player object hasn't been created in the map when the script runs
- When building, you can't have the Project folder open in Visual Studio. But guessing this is because VS is locking files.


## In Summary

The engine is good, but I'm not expecting it to change much from it's current state. 

I'll definitely consider making another game with it.

Go check out [EFPSE](https://cg8516.itch.io/easyfpseditor-ce) and [play my game](https://github.com/wiredjohn/EFPSE-Spookys-Jump-Scare-Mansion).