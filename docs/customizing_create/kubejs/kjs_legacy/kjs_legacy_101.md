---
title: KubeJS Legacy
layout: default
nav_order: 5
grand_parent: Customizing Create
parent: Getting Started with KubeJS
has_children: true
---
{: .important }
This page is for KubeJS on Minecraft 1.18.2. I will not be providing information related to KubeJS on Minecraft 1.16.5.

Are you still on the `server_scripts` folder and have Visual Studio Code open? If so, good.

In the code block before, assume that the output is on the left and usually the first item to read. Ingredients / output are usually the items found on the right side after the comma `,`.

Copy and paste this code block into Visual Studio Code for better viewing. There should be a copy button (looks like a small clipboard) on the top right corner

```js
onEvent('recipes', event => {
    /* 
    to determine if a recipe needs to be superheated or heated, simply type .heated() or .superheated() at the end of a recipe

    this is only applicable to the following recipe methods
    
    .createCompacting([outputs], [ingredients])
    .createMixing([outputs], [ingredients])

    */
    // for compacting syntax this is how you write it.
    // this recipe below uses a fluid ingredient, take note of how it is written
    // if you have multiple ingredients and / or outputs, it is required to put them in [square bracket] groups.
    event.recipes.createCompacting(['minecraft:diamond'], [Item.of('9x minecraft:coal_block'), Fluid.of('minecraft:lava', 250)]).superheated()
    
    // this recipe is basically 
    // toss 9 blocks of coal with 250 mb of lava in a basin, use a mechanical press to compact

    // you do not have to write the script exactly like this, you can actually write it like this 
    // you would most likely only need to use Item.of() in cases where an item has a chance output or has an NBT tag is needed

    // outputs with chance look like this, look at the script below
    // hint: it's the Item.of().withChance(x.xx)
    event.recipes.createCompacting(['minecraft:diamond', Item.of('minecraft:diamond').withChance(0.25)], ['9x minecraft:coal_block', Fluid.of('minecraft:lava', 250)]).superheated

    // here is a create mixing recipe that makes 1 coarse dirt block from mixing 1 dirt block and 1 gravel block 
    event.recipes.createMixing(['minecraft:coarse_dirt'], ['minecraft:dirt', 'minecraft:gravel'])

    // here is the same recipe but outputs 2 instead.
    event.recipes.createMixing(['2x minecraft:coarse_dirt'], ['minecraft:dirt', 'minecraft:gravel'])
    // 
})
```

