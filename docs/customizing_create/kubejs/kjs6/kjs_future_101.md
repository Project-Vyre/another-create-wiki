---
title: KubeJS 1.19.2
layout: default
nav_order: 1
grand_parent: Customizing Create
parent: Getting Started with KubeJS 6.1
has_children: false
---

# KubeJS
{: .no_toc }

## Page Contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

{: .note }
If you have not seen the note on the Wiki's home page, this is still a work in progress.

If you want access to the full documentation of KubeJS Legacy, here is a button to direct you to lat's site.

[KubeJS Book]{: .btn .btn-purple .mr-2 }

Otherwise, you may proceed and read below for purely Create focused methods with some vanilla MC classes mixed in.

{: .important }
This page is for KubeJS on Minecraft 1.19.2 and higher. Use `ServerEvents.recipes(event => {})` and do not use item quantifiers in `Item.of()`

{: .highlight }
Also here is a cool shortcut key that you can use... Press and hold `Ctrl` then `F` to activate your browser's Find tool then start typing. Your browser will try to find where that text or letter is located on the entire web page. This also works in-game with [Just Enough Items (JEI)](https://www.curseforge.com/minecraft/mc-mods/jei) as long as you have the inventory pulled up without the vanilla search bar.

## Vanilla Shaped and Shapeless Recipes
These recipes below are exact JS rewrites of vanilla items. Spacing is only for visual purposes, but everything can be nested under one `ServerEvents.recipes()` so you don't have to make separate files.
{% capture code_fence %}
```js
ServerEvents.recipes(event => {
    event.shaped('minecraft:diamond_sword', [
        'D',
        'D',
        'S'
    ], {
        D: 'minecraft:diamond',
        S: 'minecraft:stick'
    }).id('minecraft:diamond_sword')
    
    event.shaped('minecraft:chest', [
        'WWW',
        'W W',
        'WWW'
    ], {
        W: '#minecraft:planks'
    }).id('minecraft:chest')

    // shapeless
    event.shapeless('4x minecraft:oak_planks', ['#minecraft:oak_log']).id('minecraft:oak_planks')
    /* 
    The # symbol determines if an item is a tag ingredient or not.
    Also, if you have JEI installed the information below is really useful.
    PLEASE have advanced tooltips already enabled by pressing F3 + H on your keyboard! It really helps.
    Hovering over an item in the crafting grid will say "Accepts any:" if applicable.
    */
    event.shapeless('minecraft:netherite_ingot', [
        '4x minecraft:netherite_scrap',
		'4x minecraft:gold_ingot'
    ]).id('minecraft:netherite_ingot')
    // can also be written as...
    event.shapeless('minecraft:netherite_ingot', ['4x minecraft:netherite_scrap', '4x minecraft:gold_ingot']).id('minecraft:netherite_ingot')
    // can also be written as but obviously not really recommended because it's hard to keep track of things.
    event.shapeless('minecraft:netherite_ingot', [
        'minecraft:netherite_scrap',
        'minecraft:netherite_scrap',
        'minecraft:netherite_scrap',
        'minecraft:netherite_scrap',
        'minecraft:gold_ingot',
        'minecraft:gold_ingot',
        'minecraft:gold_ingot',
        'minecraft:gold_ingot'
    ]).id('minecraft:netherite_ingot')
})
```
{% endcapture %}
{% assign code_fence = code_fence | markdownify %}
{% include fix_linenos.html code=code_fence %}

## Compacting
Copy and paste this code block into Visual Studio Code for better viewing. There should be a copy button (looks like a small clipboard) on the top right corner of the code block.

Just a reminder you don't need to keep typing `ServerEvents.recipes` for each codeblock. All lines that start with `event.recipes` can all be nested under a single `onEvent('recipes', event => {})`.

{% capture code_fence %}
```js
ServerEvents.recipes(event => {
    /* 
    to determine if a recipe needs to be superheated or heated, simply type .heated() or .superheated() at the end of a recipe

    this is only applicable to compacting and mixing

    if you have multiple ingredients and / or outputs, it is required to put them in [square bracket] groups
    like so

    event.recipes.createCompacting([outputs], [ingredients])

    for singles you write it like so
    event.recipes.createCompacting('modid:itemid', 'modid:itemid')
    */

    // this recipe below uses a fluid ingredient, take note of how it is written
    event.recipes.createCompacting(['minecraft:diamond'], [Item.of('minecraft:coal_block', 9), Fluid.of('minecraft:lava', 250)]).superheated()
    /*
    this recipe is basically toss 9 blocks of coal with 250 mb of lava in a basin, use a mechanical press to compact

    you do not have to write the script exactly like this, you can actually write it like this 
    you would most likely only need to use Item.of() in cases where an item has a chance output or has an NBT tag is needed

    outputs with chance look like this, look at the script below
    hint: it's the Item.of().withChance(x.xx)
    */
    event.recipes.createCompacting(['minecraft:diamond', Item.of('minecraft:diamond').withChance(0.25)], ['9x minecraft:coal_block', Fluid.of('minecraft:lava', 250)]).superheated()

    // now of course you can write the recipes like to make it visually easier and not have to side scroll for miles you have a lot of outputs or ingredients
    event.recipes.createCompacting(
        ['minecraft:diamond', Item.of('minecraft:diamond').withChance(0.25)],
        ['9x minecraft:coal_block', Fluid.of('minecraft:lava', 250)]
    ).superheated()

    /* just going to state this again
    event.recipes.createCompacting([outputs], [ingredients])
    accepts .heated() and .superheated()
    accepts .withChance(x.xx) on output[]
    */
})
```
{% endcapture %}
{% assign code_fence = code_fence | markdownify %}
{% include fix_linenos.html code=code_fence %}

## Mixing 
Just a reminder you don't need to keep typing onEvent for each codeblock. All lines that start with `event.recipes` can all be nested under a single `onEvent('recipes', event => {})`.

{% capture code_fence %}
```js
ServerEvents.recipes(event => {
    /*
    event.recipes.createMixing([outputs], [ingredients])
    accepts .heated() and .superheated()
    accepts .withChance(x.xx) on output[]
    */
    // here is a create mixing recipe that makes 1 coarse dirt block from mixing 1 dirt block and 1 gravel block 
    event.recipes.createMixing(['minecraft:coarse_dirt'], ['minecraft:dirt', 'minecraft:gravel'])

    // here is the same recipe but outputs 2 instead.
    event.recipes.createMixing(['2x minecraft:coarse_dirt'], ['minecraft:dirt', 'minecraft:gravel'])
})
```
{% endcapture %}
{% assign code_fence = code_fence | markdownify %}
{% include fix_linenos.html code=code_fence %}

## Crushing
Just a reminder you don't need to keep typing onEvent for each codeblock. All lines that start with `event.recipes` can all be nested under a single `onEvent('recipes', event => {})`.

{% capture code_fence %}
```js
ServerEvents.recipes(event => {
    /*
    event.recipes.createCrushing([outputs], [ingredients])
    accepts .withChance(x.xx) on output[]
    technically requires .processingTime() so your recipes do not get instantly processed
    */
    event.recipes.createCrushing(['create:cinder_flour', Item.of('create:cinder_flour').withChance(0.50), Item.of('minecraft:netherite_scrap').withChance(0.002)],['minecraft:netherrack']).processingTime(250).id('put_modpack_name_here:recipe_name_here')

    // can also be written as this for easier output [] and input [] reading
    event.recipes.createCrushing(
        ['create:cinder_flour', Item.of('create:cinder_flour').withChance(0.50), Item.of('minecraft:netherite_scrap').withChance(0.002)], // output
        ['minecraft:netherrack'] // input
    ).processingTime(250).id('put_modpack_name_here:recipe_name_here')

    // if you wish to write in JSON use event.custom({}) instead
    event.custom({
        type: 'create:crushing',
        ingredients: [
            { item: 'minecraft:glow_ink_sac' }
        ],
        processingTime: 250,
        results: [
            { item: 'minecraft:ink_sac' },
            { item: 'minecraft:glowstone', chance: 0.1 }
        ]
    }).id('putyourmodpacknamehere:create/jsoncrushing/ink_sac_refinement')
})
```
{% endcapture %}
{% assign code_fence = code_fence | markdownify %}
{% include fix_linenos.html code=code_fence %}

## Mechanical Crafting
Just a reminder you don't need to keep typing onEvent for each codeblock. All lines that start with `event.recipes` can all be nested under a single `onEvent('recipes', event => {})`.

{: .warning }
The maximum grid size for a shaped recipe (not fireworks) is 9 x 9.

{: .note }
KubeJS will mirror and shrink recipes. *By default KubeJS will mirror and shrink recipes, which makes things like UU-Matter crafting (from ic2) harder to do as you have less shapes.You can use `noMirror()` and `noShrink()` to stop this behaviour.* - From the [KubeJS Legacy Wiki](https://wiki.latvian.dev/books/kubejs-legacy/page/recipeeventjs)

{% capture code_fence %}
```js
ServerEvents.recipes(event => {
    // here is an exact rewrite of the curshing wheels recipe in base create
    // your output item is the first thing to be defined
    // the arrangement of items is determined by using a letter key grid using capital letters
    event.recipes.createMechanicalCrafting('2x create:crushing_wheels', [
        ' AAA ',
        'AAWAA',
        'AWSWA',
        'AAWAA',
        ' AAA '
    ], { // below is how each letter is defined
        A: 'create:andesite_alloy',
        W: '#minecraft:planks',
        S: '#forge:stone'
    })
})
```
{% endcapture %}
{% assign code_fence = code_fence | markdownify %}
{% include fix_linenos.html code=code_fence %}

## Encased Fan Recipe Types
Just a reminder you don't need to keep typing onEvent for each codeblock. All lines that start with `event.recipes` can all be nested under a single `ServerEvents.recipes(event => {})`.

{% capture code_fence %}
```js
ServerEvents.recipes(event => {
    // remember output is the first [] that shows up, ingredients or inputs are on the right []
    event.recipes.createHaunting('minecraft:deepslate', 'minecraft:andesite')
    event.recipes.createHaunting('minecraft:crying_obsidian', 'minecraft:obsidian')

    // here is a recipe rewrite of gravel washing in base create, modify it to your liking
    event.recipes.createSplashing([Item.of('minecraft:flint').withChance(0.25), Item.of('minecraft:iron_nugget')], 'minecraft:gravel')
})
```
{% endcapture %}
{% assign code_fence = code_fence | markdownify %}
{% include fix_linenos.html code=code_fence %}


---

[KubeJS Book]: https://wiki.latvian.dev/books/kubejs