---
title: Customizing Create
layout: default
nav_order: 5
has_children: true
---
# Customizing Create
If you wanted to add your own recipes and *create* your own experience, then this page is for you.

Currently there are two efficient and global (not per-world) methods of customizing Create in both recipe removal and adding custom recipes. It is also important to note the following things:

- Both are global and do not require managing datapacks.
  - Simply write the recipe script then type the `/reload` command. That's it!
- Both options accelerate the process of writing custom recipes greatly.
- Only one of them can add custom Ponder scenes.

Here's a basic rundown of both solutions.

## KubeJS
[*KubeJS*](https://www.curseforge.com/minecraft/mc-mods/kubejs) by **LatvianModder** is an all in one package where you can do the following:
- Add custom items 
- Add custom blocks
- Add custom recipes
- Add custom fluids
- Remove existing recipes[^1]
- Change the client name
- Set a custom client icon
- Set default keybinds
- Modify the durability of existing items
  - Yes, this includes armor
- Give your own recipes custom `modIDs`
- Hiding items and blocks in JEI
  - A use case scenario for this would be hiding items or blocks that you disabled the recipe for.
- Add custom events that happen in-game, like NPC dialogue
- Loading datapacks globally
  - This comes in handy when using mods like [*Integrated Dungeons and Structures*](https://www.curseforge.com/minecraft/mc-mods/idas) and [*Integrated Stronghold*](https://www.curseforge.com/minecraft/mc-mods/integrated-stronghold), both of which are made by **CraisinLord**
- and much more!

It is perfect for creating your own modpack, whether for personal enjoyment with friends or publishing a modpack on Modrinth or CurseForge. Just don't forget to ship the `kubejs` folder when exporting the profile in your launcher of choice. Just to give you a baseline of how performant KubeJS is, it can load custom recipes in 0.00003 seconds, or less.
  - [*KubeJS Create*](https://www.curseforge.com/minecraft/mc-mods/kubejs-create) (also made by lat) while not mandatory, makes the process of writing recipes ***much*** faster so that you don't have to use `JSON` syntax. **Now supports Create 0.5.1 as of 6/13/2023.**
  - [*PonderJS* by Lytho and originally kotakotik22](https://www.curseforge.com/minecraft/mc-mods/ponder) is what allows you to make custom Ponder scenes. There are no other mods that can do this.
  - Recipes written will automatically appear in JEI. You don't have to do anything else.
  - KubeJS uses JavaScript and as a result has native syntax highlighting in text editors like Visual Studio Code which you can download from here: https://code.visualstudio.com/
  - If a mod does not have a KubeJS addon for it to make writing recipes easier, you can use native JSOn syntax with `event.custom({json goes here in big vertical list})`

## CraftTweaker
[*CraftTweaker*](https://www.curseforge.com/minecraft/mc-mods/crafttweaker) by **jaredlll08** is more focused on:
- Adding custom recipes
- Removing existing recipes[^1]
- Hiding items and blocks in JEI
- Adjusting durability of existing items
  - Yes... this also includes armor.
- ~~There other things I probably don't know about but KubeJS can do more~~

It does have the benefit of being typesafe but requires imports when doing certain things.
 - While not mandatory, [*CreateTweaker*](https://www.curseforge.com/minecraft/mc-mods/createtweaker) (also by jared) makes the process of writing recipes much faster so that you don't have to use JSON syntax. Currently supports compatibility with Create 0.5.1.
 - Uses a scripting language that is only applicable to CraftTweaker related things.

---

[^1]: Not all recipes can be removed if they are auto-generated and hard coded. An example of this is Create's Spout recipes when the `Mekanism` mod is installed. You can't remove the Liquid Hydrogen Bucket recipe from the Create Spout recipe even if you use the recipe ID.