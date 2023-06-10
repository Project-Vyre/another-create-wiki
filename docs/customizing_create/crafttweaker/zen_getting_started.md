---
title: Getting Started with CraftTweaker
layout: default
nav_order: 2
parent: Customizing Create
has_children: true
---
For CraftTweaker, the syntax has not changed much between `1.19.2` and `1.18.2`. Well, at least only for writing recipes. The other functions of CraftTweaker can be found on the official documentation site which is currently missing a search bar, soooo yeah.

[CraftTweaker Documentation](https://docs.blamejared.com/){: .btn .btn-blue .fs-4 .mr-2 }

Here are some perquisites to make using `ZenScript` *cough* ***tolerable*** *cough* because there is no built-in syntax highlighting or intellisense[^1] soooo yeah.
- Visual Studio Code
- Some syntax highlighting help...
  - Mrthomas20121.zenscript (that's the vscode extension ID)

However, CT does have better support for MC versions below 1.16.

JSON syntax is supported for mods that don't support CraftTweaker natively, but the solution is not as elegant as with KubeJS, so I won't be going over it as in-depth. This is what a haunting recipe looks like in pure JSON.

{% capture code_fence %}
```css
<recipetype:create:haunting>.addJsonRecipe("deepslate", {
  "type": "create:haunting",
  "ingredients": [
    {
      "item": "minecraft:andesite"
    }
  ],
  "results": [
    {
      "item": "minecraft:deepslate"
    }
  ]
});
```
{% endcapture %}
{% assign code_fence = code_fence | markdownify %}
{% include fix_linenos.html code=code_fence %}

For comparison's sake, here's the same exact recipe in KubeJS.

{% capture code_fence %}
```js
ServerEvents.recipes(event => {
    event.custom({
        type: 'create:haunting',
        ingredients: [
            { item: 'minecraft:andesite' }
        ],
        results: [
            { item: 'minecraft:deepslate' }
        ]
    })
})
```
{% endcapture %}
{% assign code_fence = code_fence | markdownify %}
{% include fix_linenos.html code=code_fence %}

Anyway, here are some things you should definitely know.

- Casting an array requires imports.
  - What does this mean? It means you have to always type a certain line at the very top while accounting each different recipe type.
- You ***have*** to end each script with `);`
  - Each script is also "indepdentent" unlike in JS where everything has to be nested under `ServerEvents.recipes(e => {})`

## Recipe Removal

{% capture code_fence %}
```css
recipes.removeByName("minecraft:bucket") // is how you remove recipes by recipe ID.
```
{% endcapture %}
{% assign code_fence = code_fence | markdownify %}
{% include fix_linenos.html code=code_fence %}

## Shaped Recipes
Instead of using a letter key, it is literal. Where you type the <item> is where that item will be defined in the crafting grid.
Each row will also be defined by a `[]` group inside the `[]` group. So it will be like `[gridcontainer[gridarrangement]]`
{% capture code_fence %}
```css
craftingTable.addShaped("recipenamegoeshere_nocustom_mod_id", <item:minecraft:bucket>, [
    [<item:minecraft:iron_ingot>, <item:minecraft:air>, <item:minecraft:iron_ingot>],
    [<item:minecraft:air>, <item:minecraft:iron_ingot>, <item:minecraft:air>]
]);
```
{% endcapture %}
{% assign code_fence = code_fence | markdownify %}
{% include fix_linenos.html code=code_fence %}

## Shapeless Recipes

{% capture code_fence %}
```css
// I am sorry but the code block can't display the entire code block.
craftingTable.addShapeless("recipename", <item:minecraft:netherite_scrap>, [<item:minecraft:netherite_scrap>, <item:minecraft:netherite_scrap>, <item:minecraft:netherite_scrap>, <item:minecraft:netherite_scrap>, <item:minecraft:gold_ingot>, <item:minecraft:gold_ingot>, <item:minecraft:gold_ingot>, <item:minecraft:gold_ingot>]);
```
{% endcapture %}
{% assign code_fence = code_fence | markdownify %}
{% include fix_linenos.html code=code_fence %}

---

[^1]: Basically smart speak for autocompletion / autocorrect but for coding.