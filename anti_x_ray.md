# Configuring Anti-Xray

> Originally written and maintained by PaperMC project

LeviAntiCheat includes an obfuscation-based Anti-Xray with three modes, configurable on a per world basis.

Anti-Xray has three different modes. `engine-mode: 1` replaces specified blocks (`hidden-blocks`) with
other "fake" blocks, `stone` (`deepslate` at y < 0, specific in config), `netherrack`, or `end_stone` based on the
dimension. In contrast, `engine-mode: 2` will replace both `hidden-blocks` and `replacement-blocks`
with randomly generated `hidden-blocks`. `engine-mode: 3` works similarly to `engine-mode: 2`, but instead of
randomizing every block, it randomizes the block for each layer of a chunk.

The following images[^1] show how each mode will look for a player using Xray with the recommended
configuration in both the overworld and nether.

[^1]:
    Image design by `Oberfail`, initially posted in the
    [PaperMC Discord](https://discord.gg/papermc).

![Overworld Anti-Xray Comparison](https://github.com/PaperMC/docs/blob/main/docs/paper/admin/how-to/assets/anti-xray-overworld.png)
![Nether Anti-Xray Comparison](https://github.com/PaperMC/docs/blob/main/docs/paper/admin/how-to/assets/anti-xray-nether.png)

Especially on the client side, `engine-mode: 1` is much less computationally intensive, while
`engine-mode: 2` may better prevent Xray. With `engine-mode: 1`, only ores that are entirely covered
by solid blocks will be hidden. Ores exposed to air in caves or water from a lake will not be
hidden. With `engine-mode: 2`, fake ores obstruct the view of real blocks. If `air` is added to
`hidden-blocks`, `engine-mode: 2` will effectively hide all ores, even those exposed to air. `engine-mode: 3` can reduce network load when joining by a factor of ~2 and helps with chunk packet compression.

> # Anti-Xray Bypasses
> 
> **Seed Reversing**: Another attack vector is the deterministic nature of Minecraft's world
> generation. If the client is able to obtain the world seed, it is able to know the real location of
> every generated ore, completely bypassing Anti-Xray.
> 
> **Ores Exposed to Air**: In `engine-mode: 1`, `engine-mode: 2` and `engine-mode: 3`, it is possible for a client
> to view ores that are exposed to air.

## Recommended configuration

The recommended configuration for `engine-mode: 1`, `engine-mode: 2` and `engine-mode: 3` is as follows:

### `engine-mode: 1`

<details>
  <summary>Default World Configuration</summary>

```json
"overworld": {
    "Enable": true,
    "EngineMode": 1,
    "UpdateRadius": 2.0,
    "MaxBlockHeight": 64,
    "HiddenBlocks": [
        "minecraft:coal_ore",
        "minecraft:raw_copper_block",
        "minecraft:deepslate_coal_ore",
        "minecraft:copper_ore",
        "minecraft:deepslate_copper_ore",
        "minecraft:emerald_ore",
        "minecraft:raw_iron_block",
        "minecraft:diamond_ore",
        "minecraft:deepslate_diamond_ore",
        "minecraft:deepslate_emerald_ore",
        "minecraft:redstone_ore",
        "minecraft:gold_ore",
        "minecraft:deepslate_gold_ore",
        "minecraft:iron_ore",
        "minecraft:deepslate_iron_ore",
        "minecraft:lapis_ore",
        "minecraft:deepslate_lapis_ore",
        "minecraft:deepslate_redstone_ore"
    ],
    "ReplacementBlocks": [
        "minecraft:stone",
        "minecraft:deepslate"
    ]
}
```

</details>

<details>
  <summary>Nether Configuration</summary>

```json
"nether": {
    "Enable": true,
    "EngineMode": 1,
    "UpdateRadius": 2.0,
    "MaxBlockHeight": 128,
    "HiddenBlocks": [
        "minecraft:ancient_debris",
        "minecraft:nether_gold_ore",
        "minecraft:quartz_ore"
    ],
    "ReplacementBlocks": [
        "minecraft:netherrack"
    ]
}
```


</details>

</details>

### `engine-mode: 2` and `engine-mode: 3`

<details>
  <summary>Default World Configuration</summary>

```json
"overworld": {
    "Enable": true,
    "EngineMode": 2,
    "UpdateRadius": 2.0,
    "MaxBlockHeight": 64,
    "HiddenBlocks": [
        "minecraft:copper_ore",
        "minecraft:deepslate_copper_ore",
        "minecraft:raw_copper_block",
        "minecraft:diamond_ore",
        "minecraft:deepslate_diamond_ore",
        "minecraft:gold_ore",
        "minecraft:iron_ore",
        "minecraft:deepslate_gold_ore",
        "minecraft:deepslate_iron_ore",
        "minecraft:raw_iron_block",
        "minecraft:lapis_ore",
        "minecraft:deepslate_lapis_ore",
        "minecraft:redstone_ore",
        "minecraft:deepslate_redstone_ore"
    ],
    "ReplacementBlocks": [
        "minecraft:amethyst_block",
        "minecraft:andesite",
        "minecraft:deepslate",
        "minecraft:calcite",
        "minecraft:deepslate_emerald_ore",
        "minecraft:oak_planks",
        "minecraft:tuff",
        "minecraft:budding_amethyst",
        "minecraft:gravel",
        "minecraft:coal_ore",
        "minecraft:deepslate_coal_ore",
        "minecraft:diorite",
        "minecraft:smooth_basalt",
        "minecraft:dirt",
        "minecraft:stone",
        "minecraft:emerald_ore",
        "minecraft:granite"
    ]
}
```

</details>

<details>
  <summary>Nether Configuration</summary>

```json
"nether": {
    "Enable": true,
    "EngineMode": 3,
    "UpdateRadius": 2.0,
    "MaxBlockHeight": 128,
    "HiddenBlocks": [
        "minecraft:ancient_debris",
        "minecraft:glowstone",
        "minecraft:bone_block",
        "minecraft:quartz_ore",
        "minecraft:magma_block",
        "minecraft:nether_bricks",
        "minecraft:nether_gold_ore",
        "minecraft:polished_blackstone_bricks"
    ],
    "ReplacementBlocks": [
        "minecraft:basalt",
        "minecraft:blackstone",
        "minecraft:gravel",
        "minecraft:soul_soil",
        "minecraft:netherrack",
        "minecraft:soul_sand"
    ]
}
```


</details>

## FAQ, common pitfalls and support

<details>
  <summary>I can still see (some) ores / use X-ray</summary>

As described above, there are several reasons why you might still see (some) ores even though you
have enabled Anti-Xray:

* The ores are above the configured `max-block-height` value.
* Anti-Xray cannot hide ores exposed to air or other transparent blocks (in caves for example). In
  principle this is also the case for `engine-mode: 2` and `engine-mode: 3`, however, usually the fake ores obstruct the
  view of real blocks. Hiding those exposed ores too requires additional plugins.
* The block type is missing in the configured block lists. This can be the result of using an
  outdated configuration file.

</details>

<details>
  <summary>I have added fake blocks but X-ray doesn't show them</summary>

If you use `engine-mode: 2` or `engine-mode: 3` and you have added fake blocks to the `hidden-blocks` list but you can't
see them in-game using X-ray, this can have the following reasons:

* The added block types are tile entities. Anti-Xray can hide (replace) tile entities (such as
  chests), provided that they are not exposed to air or other transparent blocks. However, Anti-Xray
  can't place tile entities as fake blocks into the chunk.
* The block is disabled in your client's X-ray mod or not shown by your X-ray resource pack.

</details>

<details>
  <summary>It doesn't work below y = 0 or in certain other places.</summary>

* Your configuration file is probably outdated and missing important blocks in the
  `replacement-blocks` list, such as `deepslate` or biome-specific blocks, such as `basalt`. You
  might also want to check if the `hidden-blocks` list includes all important ores and their
  `deepslate` variants.
* If it doesn't work above a certain y-level, check your `max-block-height` setting.

</details>
