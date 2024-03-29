---
title: Getting Started with KubeJS 5.5
layout: default
nav_order: 2
parent: Customizing Create
has_children: true
---

# Introduction to KubeJS 5.5
Some KubeJS documentation with a focus on Create modification.
{: .fs-6 .fw-300 }

{: .important }
This page is far from finished. In addition, the contents of this page and the nested sub-pages are referring to KubeJS 5.5 for MC 1.18.2. Documentation for 1.16.5 and below will not be written. Use CraftTwewaker for older versions of Minecraft.

First step is to install the following:
- [Visual Studio Code](https://code.visualstudio.com/)
  - I highly recommend using the GitHub theme. You can install it by clicking the button that looks like a 2x2 rubik's cube and the corner piece has been taken out on the left hand side of the VSCode window then searching up GitHub theme.
- [KubeJS](https://www.curseforge.com/minecraft/mc-mods/kubejs)
- [KubeJS Create](https://www.curseforge.com/minecraft/mc-mods/kubejs-create)

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
  - You can also modify item tags, loot tables, and more in here. 
- `startup_scripts`
  - Scripts for your custom items, blocks, armor and fluids go in here.
  - This is where you can modify item and armor durability.

{: .warning }
DO NOT use an existing modID in your recipeID.

{: .important }
KubeJS uses slightly different syntax (way of typing "commands" in layman's terms) depending on which version of Minecraft you are using, specifically 1.19.2+ and 1.18.2. I will be skipping 1.16.5 syntax, go bother someone else.

For all intents and purposes, the main focus of this tutorial is for adding and removing your own recipes.

Open up Visual Studio Code and click `Open Folder` and navigate to the `kubejs` folder. 

Click it, then click the `Select Folder` button on the bottom right corner. If a prompt says "Do you want to trust the authors of these files?" click yes. 

In the `server_scripts` folder, there should already be a `script.js` file. Open that via the VSCode Explorer panel where you can see all the kubejs folders. Personally I would organize scripts by mod if you want to easily transfer your scripts without having to delete and remove certain lines of code.

Here is something that you should know: The word `event` is simply something that happens. When it comes to being inside the main `ServerEvent` / `onEvent` class, the word `event` can be changed to `e` to keep it short. Just ensure that it matches so that your `events` can be fired and be registered in-game.

If you are on 1.18.2 the code below applies.

{% capture code_fence %}
```js
onEvent('recipes', event => {
    // type your recipe scripts here
    event.recipes.createHaunting([outputs], [input])
})

// alternatively can be written as
onEvent('recipes', e => {
    // type your recipe scripts here
    e.recipes.createHaunting([outputs], [input])
})
```
{% endcapture %}
{% assign code_fence = code_fence | markdownify %}
{% include fix_linenos.html code=code_fence %}

Please note that I will be using **1.18.2** syntax from here, but the nested code inside `(events => { the code inside here })` should still function. I would still check the official KubeJS Discord and Wiki for up-to-date information, however.
{: .note }

In both cases, did you notice how both begin with `(event => {` and then end with `})`? It is important to keep your scripts in that "group" / region of the code, otherwise it may not load.

You can also set variables like this to help with typing less.

{% capture code_fence %}
```js
// the variable iron is read as the item iron nugget so you don't have to keep typing it over
// and over and over and over and over you get the point?
let iron = 'minecraft:iron_ingot'

onEvent('recipes', events => {
    event.shaped('minecraft:iron_sword', [
        'I',
        'I',
        'H'
    ], {
        I: iron,
        H: 'minecraft:stick' 
    })
    event.shaped('minecraft:shears', [
      ' I',
      'I '
    ], {
      I: iron,
    })
})

```
{% endcapture %}
{% assign code_fence = code_fence | markdownify %}
{% include fix_linenos.html code=code_fence %}

Both of these shaped crafting table recipes are recreations of the vanilla recipe for the Iron Sword and Shears.

The letters between the single quotation marks are the "keys" which are then defined by the letter key definitions you provide below between the `{}` brackets after the crafting grid `[]` brackets. 

Spaces in the single quotation mark grid [] equal empty space.

Also some code can exceed the width of the code block below, just wanted to make you aware of that.

{% capture code_fence %}
```js
// priority: 0
// priority is how to get this script file to load before the others

// a lot of things can be written in a single 
ServerEvents.recipes(event => {
    // For starters, you can add a single line comment with two forward slashes like at the beginning of THIS comment

    /*
    To add multi-line comments, use the / and * keys like so on the line above and below.
    Also the spaces in the code is just there to improve readability and is not mandatory
    */

    /* You can also do multiline text like this
    adsl;fkajs;dlkfjas;dflkjas;dlfkjasdf;lkasjdf;lkasdjds
    aaaaaaaaaaaaaaaaaaaaa;slkdfj;aslkdfj;adlkfj;asdlkfja;sldkfj;asldkfjasdlkfdajsdasf just make it readable */

    // Note: Ensure all items here are base Create and vanilla! You can use items from other mods, but this is just focused on Create
    // recipes removal
    event.remove({id: 'create_sa:netherrack_recipe' }) // this is how you remove specific recipes by their recipeid
    event.remove({id: 'create_sa:obsidian_haunting' })
    event.remove({id: 'create:crushing/gravel' }) // some recipe ids contain modid:recipetype/slashes
    event.remove({id: 'create:crushing/netherrack' })

    // note that the recipeid can also be the itemid, so be sure to press F3 + H to enable Advanced tooltips.

    event.remove({}) // whatever you do, do NOT use this, EVER. This removes ALL recipes that can be removed.

    event.remove({output: 'minecraft:wooden_pickaxe' }) // if you want to remove all recipes that output a specific item, this is how you do it.

    event.remove({output: '#minecraft:planks' }) // if you wanted to remove all recipes that output all items with a specific tag

    event.remove({mod: 'extendedcrafting' }) // if you wanted to remove all recipes from a specific mod
    event.remove({mod: 'farmersdelight' })
    event.remove({mod: 'create' }) 

    event.remove({})
})
```
{% endcapture %}
{% assign code_fence = code_fence | markdownify %}
{% include fix_linenos.html code=code_fence %}

