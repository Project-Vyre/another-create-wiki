---
title: KubeJS 6.1 Examples
layout: minimal
nav_order: 2
grand_parent: Customizing Create
parent: Getting Started with KubeJS
has_children: false
---

This page contains examples only, with no comments in the code. All examples here are **exact** copies of vanilla Create recipes as they are in-game, with the only difference being that this is implemented with KubeJS. Individual recipes are spaced out only for the sake of legibility.

This was written with KJS 6.1 in mind as of July 24th, 2023.

{% capture code_fence %}
```js
ServerEvents.recipes(event => {
    event.shaped('create:andesite_alloy', [
        'NA',
        'AN'
    ], {
        N: 'minecraft:iron_nugget',
        A: 'minecraft:andesite'
    }).id('create:crafting/materials/andesite_alloy')

    event.shaped('create:andesite_alloy', [
        'NA',
        'AN'
    ], {
        N: 'create:zinc_nugget',
        A: 'minecraft:andesite'
    }).id('create:crafting/materials/andesite_alloy_from_zinc')

    event.recipes.create.sequencedAssembly([
        Item.of('create:precision_mechanism').withChance(120.0),
        Item.of('create:golden_sheet').withChance(8.0),
        Item.of('create:andesite_alloy').withChance(8.0),
        Item.of('create:cogwheel').withChance(5.0),
        Item.of('minecraft:gold_nugget').withChance(3.0),
        Item.of('create:shaft').withChance(2.0),
        Item.of('create:crushed_raw_gold').withChance(2.0),
        'minecraft:iron_ingot',
        'minecraft:clock'
    ], 'create:golden_sheet', [
        event.recipes.create.deploying('create:incomplete_precision_mechanism', ['create:incomplete_precision_mechanism', 'create:cogwheel']),
        event.recipes.create.deploying('create:incomplete_precision_mechanism', ['create:incomplete_precision_mechanism', 'create:large_cogwheel']),
        event.recipes.create.deploying('create:incomplete_precision_mechanism', ['create:incomplete_precision_mechanism', '#forge:nuggets/iron'])
    ]).transitionalItem('create:incomplete_precision_mechanism').loops(3).id('create:sequenced_assembly/precision_mechanism')
})
```
{% endcapture %}
{% assign code_fence = code_fence | markdownify %}
{% include fix_linenos.html code=code_fence %}