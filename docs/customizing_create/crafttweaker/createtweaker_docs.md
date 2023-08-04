---
title: CreateTweaker
layout: default
nav_order: 1
grand_parent: Customizing Create
parent: Getting Started with CraftTweaker
has_children: false
---

REEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEE

So, how do you set up items?

`<item:minecraft:stone>`

Okay, so how do you set up chanced outputs? Simple.

`[<item:minecraft:basalt> % 100]`


## Compacting

- Supports the following constants to determine if no heating is required, heated or superheated.
  - `<constant:create:heat_condition:none>`
  - `<constant:create:heat_condition:heated>`
  - `<constant:create:heat_condition:superheated>`
- Outputs on left `[]` and ingredients on `[]` right with fluids `[]` also on the right, they are all separated by commas.

{% capture code_fence %}
```css
import mods.create.CompactingManager;
// Remember, output is always the first [] on the very left! Ingredients are grouped on the right side.
// copy any of the lines below for your respective renewable materials
<recipetype:create:compacting>.addRecipe("renewable_basalt", <constant:create:heat_condition:none>, [<item:minecraft:basalt> % 100], [<item:minecraft:blue_ice> * 1], [<fluid:minecraft:lava> * 500], 100);
<recipetype:create:compacting>.addRecipe("renewable_coal", <constant:create:heat_condition:heated>, [<item:minecraft:coal>], [<item:minecraft:dried_kelp_block> * 9], [<fluid:minecraft:lava> * 25]);
<recipetype:create:compacting>.addRecipe("renewable_diamond", <constant:create:heat_condition:superheated>, [<item:minecraft:diamond>], [<item:minecraft:coal_block> * 9], [<fluid:minecraft:lava> * 1000]);
```
{% endcapture %}
{% assign code_fence = code_fence | markdownify %}
{% include fix_linenos.html code=code_fence %}

## Mixing

## Crushing
Processing time is set by being the last number at the very end as can be seen below. You can also see clearly where the output items are.

{% capture code_fence %}
```css
import mods.createtweaker.CrushingRecipe;
<recipetype:create:crushing>.addRecipe("netherrack_crushing", [<item:create:cinder_flour>, <item:create:cinder_flour> % 50, <item:minecraft:netherite_scrap> % 0.002], <item:minecraft:netherrack>, 250);
```
{% endcapture %}
{% assign code_fence = code_fence | markdownify %}
{% include fix_linenos.html code=code_fence %}

## Encased Fan Recipes

{% capture code_fence %}
```css
import mods.createtweaker.HauntingManager;
// Haunting - Crying Obsidian
<recipetype:create:haunting>.addRecipe("obsidian_haunting", [<item:minecraft:crying_obsidian>], <item:minecraft:obsidian>);
```
{% endcapture %}
{% assign code_fence = code_fence | markdownify %}
{% include fix_linenos.html code=code_fence %}

## Mechanical Crafting
This is a recipe taken out of my modpack, just to perfectly demonstrate the issue with ZenScript's method of writing a recipe for Mechanical Crafters. It does get hard keeping track of where ingredients are positioned on the crafting grid.

{% capture code_fence %}
```css
import mods.create.MechanicalCrafterManager;
// MechanicalCrafterManager.addRecipe(name as string, output as IItemStack, ingredients as IIngredient[][]) as void
<recipetype:create:mechanical_crafting>.addRecipe("zen_electron_tube_singularity", (<item:extendedcrafting:singularity>.withTag({Id: "extendedcrafting:electron_tube"}) * 1), [
    [<item:minecraft:air>, <item:minecraft:crying_obsidian>, <item:minecraft:crying_obsidian>, <item:minecraft:crying_obsidian>, <item:minecraft:crying_obsidian>, <item:minecraft:crying_obsidian>, <item:minecraft:crying_obsidian>, <item:minecraft:crying_obsidian>, <item:minecraft:air>], 
    [<item:minecraft:crying_obsidian>, <item:minecraft:crying_obsidian>, <item:minecraft:crying_obsidian>, <item:create:electron_tube>, <item:create:electron_tube>, <item:create:electron_tube>, <item:minecraft:crying_obsidian>, <item:minecraft:crying_obsidian>, <item:minecraft:crying_obsidian>], 
    [<item:minecraft:crying_obsidian>, <item:minecraft:crying_obsidian>, <item:create:electron_tube>, <item:create:electron_tube>, <item:create:electron_tube>, <item:create:electron_tube>, <item:create:electron_tube>, <item:minecraft:crying_obsidian>, <item:minecraft:crying_obsidian>],
    [<item:minecraft:crying_obsidian>, <item:create:electron_tube>, <item:create:electron_tube>, <item:create:electron_tube>, <item:create:electron_tube>, <item:create:electron_tube>, <item:create:electron_tube>, <item:create:electron_tube>, <item:minecraft:crying_obsidian>,],
    [<item:minecraft:crying_obsidian>, <item:create:electron_tube>, <item:create:electron_tube>, <item:create:electron_tube>, <item:create:electron_tube>, <item:create:electron_tube>, <item:create:electron_tube>, <item:create:electron_tube>, <item:minecraft:crying_obsidian>,],
    [<item:minecraft:crying_obsidian>, <item:create:electron_tube>, <item:create:electron_tube>, <item:create:electron_tube>, <item:create:electron_tube>, <item:create:electron_tube>, <item:create:electron_tube>, <item:create:electron_tube>, <item:minecraft:crying_obsidian>,],
    [<item:minecraft:crying_obsidian>, <item:minecraft:crying_obsidian>, <item:create:electron_tube>, <item:create:electron_tube>, <item:create:electron_tube>, <item:create:electron_tube>, <item:create:electron_tube>, <item:minecraft:crying_obsidian>, <item:minecraft:crying_obsidian>],
    [<item:minecraft:crying_obsidian>, <item:minecraft:crying_obsidian>, <item:minecraft:crying_obsidian>, <item:create:electron_tube>, <item:create:electron_tube>, <item:create:electron_tube>, <item:minecraft:crying_obsidian>, <item:minecraft:crying_obsidian>, <item:minecraft:crying_obsidian>], 
    [<item:minecraft:air>, <item:minecraft:crying_obsidian>, <item:minecraft:crying_obsidian>, <item:minecraft:crying_obsidian>, <item:minecraft:crying_obsidian>, <item:minecraft:crying_obsidian>, <item:minecraft:crying_obsidian>, <item:minecraft:crying_obsidian>, <item:minecraft:air>], 
    ]);
```
{% endcapture %}
{% assign code_fence = code_fence | markdownify %}
{% include fix_linenos.html code=code_fence %}

For a comparison with KubeJS's method of writing a Mechanical Crafting recipe with the exact same recipe shown above.

{% capture code_fence %}
```js
ServerEvents.recipes(event => {
    event.recipes.createMechanicalCrafting(Item.of('extendedcrafting:singularity', '{Id:"extendedcrafting:electron_tube"}'), [
        ' LLLLLLL ',
        'LLLEEELLL',
        'LLEEEEELL',
        'LEEEEEEEL',
        'LEEEEEEEL',
        'LEEEEEEEL',
        'LLEEEEELL',
        'LLLEEELLL',
        ' LLLLLLL '
    ], {
        L: 'minecraft:crying_obsidian',
        E: 'create:electron_tube'
    }).id('finality:electron_tube_singularity')
})
```
{% endcapture %}
{% assign code_fence = code_fence | markdownify %}
{% include fix_linenos.html code=code_fence %}

However, it can also be written like this. (Says ashley)

{% capture code_fence %}
```css
import mods.create.MechanicalCrafterManager;
var O as IIngredient = <item:minecraft:crying_obsidian>;
var E as IIngredient = <item:create:electron_tube>;
var A as IIngredient = <item:minecraft:air>;
// MechanicalCrafterManager.addRecipe(name as string, output as IItemStack, ingredients as IIngredient[][]) as void
<recipetype:create:mechanical_crafting>.addRecipe("zen_electron_tube_singularity", (<item:extendedcrafting:singularity>.withTag({Id: "extendedcrafting:electron_tube"}) * 1), [
    [A, O, O, O, O, O, O, O, A],
    [O, O, O, E, E, E, O, O, O],
    [O, O, E, E, E, E, E, O, O],
    [O, E, E, E, E, E, E, E, O],
    [O, E, E, E, E, E, E, E, O],
    [O, E, E, E, E, E, E, E, O],
    [O, O, E, E, E, E, E, O, O],
    [O, O, O, E, E, E, O, O, O],
    [A, O, O, O, O, O, O, O, A]
]);
```
{% endcapture %}
{% assign code_fence = code_fence | markdownify %}
{% include fix_linenos.html code=code_fence %}

## Sequenced Assembly
The code below is actually very self explanatory. You also do not have to restate the transitional item which is located in `.transitionTo(<>)`.

{% capture code_fence %}
```css
<recipetype:create:sequenced_assembly>.addRecipe(<recipetype:create:sequenced_assembly>.builder("seq_blue_ice_singularity")
                                      .transitionTo(<item:extendedcrafting:singularity>)
                                      .require(<item:minecraft:blue_ice>)
                                      .loops(16)
                                      .addOutput(<item:extendedcrafting:singularity>.withTag({Id: "extendedcrafting:blue_ice"}) * 1, 100)
                                      .addStep<mods.createtweaker.FillingRecipe>((rb) => rb.require(<fluid:minecraft:water> * 25))
                                      .addStep<mods.createtweaker.DeployerApplicationRecipe>((rb) => rb.require(<item:minecraft:blue_ice>))
                                      .addStep<mods.createtweaker.PressingRecipe>((rb) => rb.require(<item:extendedcrafting:singularity>))
                                      .addStep<mods.createtweaker.PressingRecipe>((rb) => rb.require(<item:extendedcrafting:singularity>))
                                      .addStep<mods.createtweaker.PressingRecipe>((rb) => rb.require(<item:extendedcrafting:singularity>)));
```
{% endcapture %}
{% assign code_fence = code_fence | markdownify %}
{% include fix_linenos.html code=code_fence %}