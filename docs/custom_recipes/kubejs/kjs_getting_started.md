---
title: Getting Started with KubeJS
layout: default
nav_order: 5
parent: Customizing Create
has_children: true
---

# Introduction to KubeJS Create

First step is to install KubeJS. 

After KubeJS is installed, run the game to generate the `kubejs` folder which is located in your Minecraft instance folder.

It contains the following folders and a `README.txt` file.
- `assets`
  - Here is where you put your custom item, armor, block and fluid textures. 
    - Yes, you can use `.json` files for custom block models.
    - Yes, you can use `.mcmeta` files to change how your block is displayed in-game and make another color variant for deepslate for example.
- `client_scripts`
  - This is where your scripts related to tooltips, JEI modification and other client side things will go.
- `config`
  - This is where you can put `defaultoptions.txt` so you don't have to use DefaultOptions.
  - Setting the Window Title. That's the client name that shows up in the window on the top left corner if you don't know what that means.
  - Setting the client icon. Must be an `.png` file exported in 32-bit, otherwise it will cause a JVM crash.
- `data`
  - Put the `data` folder contents of your datapacks in here. It will not work if you have it like: `kubejs\data\bigcustomdatapack\`
- `exported`
  - You don't really need to worry about it. It's just where data dumps like texture atlases are well... dumped.
- `server_scripts`
  - This is where the recipe magic happens! Remember to `Ctrl + S` to save your recipe once it is finished then type /reload.
  - You can also modify item tags, loot tables, and more in here. For all intents and purposes, the main focus of this tutorial is for adding your own recipes.
- `startup_scripts`
  - Scripts for your custom items, blocks, armor and fluids go in here.
  - This is where you can modify item and armor durability.

{: .important}
KubeJS uses slightly different syntax (way of typing "commands" in layman's terms) depending on which version of Minecraft you are using, specifically 1.19.2+ and 1.18.2. Will be skipping 1.16.5 syntax.