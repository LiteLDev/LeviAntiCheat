# Configuring Anti-Xray

> Originally written and maintained by PaperMC project

LeviAntiCheat includes an obfuscation-based Anti-Xray with three modes, configurable on a per dimension basis.

Anti-Xray has three different modes. `engineMode: 0` replaces the specified blocks (`obfuscateBlocks`) with a
"fake" block, `mainBlock` (`minecraft:stone` by default), or `mainBlockMinus` (`minecraft:deepslate` by default)
at y < 0. Set `mainBlock` to `minecraft:netherrack` or `minecraft:end_stone` for the nether or the end. In contrast,
`engineMode: 1` replaces every hidden solid block with a randomly chosen block from `obfuscateBlocks`.
`engineMode: 2` works similarly to `engineMode: 1`, but instead of randomizing every block, it picks the block by
the y level, so all blocks in the same layer get the same fake block.

> Note: A block will be obfuscated only if it is a solid block and all six sides are covered by solid blocks (see
> [Solid blocks](#solid-blocks)). Only blocks below `maxHeight` are obfuscated.

The following images[^1] show how each mode will look for a player using Xray with the recommended
configuration in both the overworld and nether. The images come from PaperMC, whose engine modes 1, 2 and 3
correspond to `engineMode` 0, 1 and 2 here.

[^1]:
    Image design by `Oberfail`, initially posted in the
    [PaperMC Discord](https://discord.gg/papermc).

![Overworld Anti-Xray Comparison](https://github.com/PaperMC/docs/blob/main/src/content/docs/paper/admin/how-to/assets/anti-xray-overworld.png)
![Nether Anti-Xray Comparison](https://github.com/PaperMC/docs/blob/main/src/content/docs/paper/admin/how-to/assets/anti-xray-nether.png)

Especially on the client side, `engineMode: 0` is much less computationally intensive, while
`engineMode: 1` may better prevent Xray. With `engineMode: 0`, only ores that are entirely covered
by solid blocks will be hidden. Ores exposed to air in caves or water from a lake will not be
hidden. With `engineMode: 1`, fake ores obstruct the view of real blocks. `engineMode: 2` makes the
sub-chunks more uniform than `engineMode: 1`, which helps with chunk packet compression.

> # Anti-Xray Bypasses
> 
> **Seed Reversing**: Another attack vector is the deterministic nature of Minecraft's world
> generation. If the client is able to obtain the world seed, it is able to know the real location of
> every generated ore, completely bypassing Anti-Xray. Keep `worldSafety.fakeSeed` enabled.
> 
> **Ores Exposed to Air**: In `engineMode: 0`, `engineMode: 1` and `engineMode: 2`, it is possible for a client
> to view ores that are exposed to air.

## Configuration

Anti-Xray is configured in `cheatPrevention.antiXray` of the [configuration file](README.md#configuration-file).

| Key | Default | Description |
| --- | --- | --- |
| `enable` | `true` | Enable Anti-Xray |
| `maxThreads` | `4` | Worker threads for rewriting chunks, `0` uses the number of CPU threads |
| `debugDump` | `false` | Dump the original and rewritten packets for debugging |
| `autoSolidCheck` | `true` | Detect solid blocks automatically, see [Solid blocks](#solid-blocks) |
| `treatAddonBlocksAsNonSolid` | `true` | Treat blocks that are not in the `minecraft:` namespace as non-solid |
| `solidBlocks` | not set | Optional. Blocks that are treated as solid |
| `nonSolidBlocks` | not set | Optional. Blocks that are never treated as solid |
| `dimensions` | `overworld`, `nether` | Per-dimension settings, keyed by dimension name |

Each entry of `dimensions` has the following keys. An unknown dimension name, engine mode or a `maxHeight` that
is not a multiple of 16 is reported in the log and Anti-Xray is not enabled in that dimension.

| Key | Description |
| --- | --- |
| `enable` | Enable Anti-Xray in this dimension |
| `engineMode` | `0`, `1` or `2`, see above |
| `maxHeight` | Only blocks below this y level are obfuscated. Must be a multiple of 16 |
| `updateRadius` | When a block changes, the real blocks within this radius are sent again |
| `obfuscateBlocks` | `engineMode: 0`: the blocks to hide. `engineMode: 1` and `2`: the fake blocks to show |
| `mainBlock` | `engineMode: 0` only. The fake block at y >= 0, `minecraft:stone` if not set |
| `mainBlockMinus` | `engineMode: 0` only. The fake block at y < 0, `minecraft:deepslate` if not set |

### Solid blocks

With `autoSolidCheck: true`, every full cube block that blocks movement is solid. Blocks in `nonSolidBlocks`,
and blocks from add-ons when `treatAddonBlocksAsNonSolid` is `true`, are never solid. Other blocks listed in
`solidBlocks` are added. With `autoSolidCheck: false`, only the blocks listed in `solidBlocks` are solid.

## Recommended configuration

The recommended configuration for `engineMode: 0`, `engineMode: 1` and `engineMode: 2` is as follows.
Put the entries in `cheatPrevention.antiXray.dimensions`.

### `engineMode: 0`

<details>
  <summary>Overworld Configuration</summary>

```json
"overworld": {
    "enable": true,
    "engineMode": 0,
    "maxHeight": 64,
    "updateRadius": 2,
    "obfuscateBlocks": [
        "minecraft:coal_ore",
        "minecraft:deepslate_coal_ore",
        "minecraft:copper_ore",
        "minecraft:raw_copper_block",
        "minecraft:deepslate_copper_ore",
        "minecraft:diamond_ore",
        "minecraft:deepslate_diamond_ore",
        "minecraft:emerald_ore",
        "minecraft:deepslate_emerald_ore",
        "minecraft:gold_ore",
        "minecraft:deepslate_gold_ore",
        "minecraft:iron_ore",
        "minecraft:raw_iron_block",
        "minecraft:deepslate_iron_ore",
        "minecraft:lapis_ore",
        "minecraft:deepslate_lapis_ore",
        "minecraft:redstone_ore",
        "minecraft:deepslate_redstone_ore"
    ],
    "mainBlock": "minecraft:stone",
    "mainBlockMinus": "minecraft:deepslate"
}
```

</details>

<details>
  <summary>Nether Configuration</summary>

```json
"nether": {
    "enable": true,
    "engineMode": 0,
    "maxHeight": 128,
    "updateRadius": 2,
    "obfuscateBlocks": [
        "minecraft:ancient_debris",
        "minecraft:nether_gold_ore",
        "minecraft:quartz_ore"
    ],
    "mainBlock": "minecraft:netherrack"
}
```

</details>

### `engineMode: 1` and `engineMode: 2`

In these modes every hidden solid block is replaced, so `obfuscateBlocks` only lists the fake blocks to show.

<details>
  <summary>Overworld Configuration</summary>

```json
"overworld": {
    "enable": true,
    "engineMode": 1,
    "maxHeight": 64,
    "updateRadius": 2,
    "obfuscateBlocks": [
        "minecraft:coal_ore",
        "minecraft:deepslate_coal_ore",
        "minecraft:copper_ore",
        "minecraft:raw_copper_block",
        "minecraft:deepslate_copper_ore",
        "minecraft:diamond_ore",
        "minecraft:deepslate_diamond_ore",
        "minecraft:emerald_ore",
        "minecraft:deepslate_emerald_ore",
        "minecraft:gold_ore",
        "minecraft:deepslate_gold_ore",
        "minecraft:iron_ore",
        "minecraft:raw_iron_block",
        "minecraft:deepslate_iron_ore",
        "minecraft:lapis_ore",
        "minecraft:deepslate_lapis_ore",
        "minecraft:redstone_ore",
        "minecraft:deepslate_redstone_ore"
    ]
}
```

</details>

<details>
  <summary>Nether Configuration</summary>

```json
"nether": {
    "enable": true,
    "engineMode": 2,
    "maxHeight": 128,
    "updateRadius": 2,
    "obfuscateBlocks": [
        "minecraft:ancient_debris",
        "minecraft:bone_block",
        "minecraft:glowstone",
        "minecraft:magma",
        "minecraft:nether_brick",
        "minecraft:nether_gold_ore",
        "minecraft:polished_blackstone_bricks",
        "minecraft:quartz_ore"
    ]
}
```

</details>

## FAQ, common pitfalls and support

<details>
  <summary>I can still see (some) ores / use X-ray</summary>

As described above, there are several reasons why you might still see (some) ores even though you
have enabled Anti-Xray:

* The ores are above the configured `maxHeight` value.
* Anti-Xray cannot hide ores exposed to air or other non-solid blocks (in caves for example). In
  principle this is also the case for `engineMode: 1` and `engineMode: 2`, however, usually the fake ores obstruct the
  view of real blocks.
* With `engineMode: 0`, the block type is missing in `obfuscateBlocks`.
* Anti-Xray is not enabled in that dimension. Check the server log for errors about the dimension name,
  `engineMode` or `maxHeight`.

</details>

<details>
  <summary>I have added fake blocks but X-ray doesn't show them</summary>

If you use `engineMode: 1` or `engineMode: 2` and you have added fake blocks to the `obfuscateBlocks` list but you can't
see them in-game using X-ray, this can have the following reasons:

* The block name is wrong. Unknown blocks are reported in the server log and ignored.
* The block is disabled in your client's X-ray mod or not shown by your X-ray resource pack.

With `engineMode: 0`, `obfuscateBlocks` are the blocks to hide, and the fake block is `mainBlock` / `mainBlockMinus`.

</details>

<details>
  <summary>It doesn't work below y = 0 or in certain other places.</summary>

* With `engineMode: 0`, check `mainBlockMinus`, the fake block below y = 0.
* The blocks around the ores are not treated as solid. With `autoSolidCheck: false`, add the blocks such as
  `deepslate`, `tuff` or biome-specific blocks such as `basalt` to `solidBlocks`. Also check `nonSolidBlocks`
  and `treatAddonBlocksAsNonSolid`.
* With `engineMode: 0`, you might also want to check if the `obfuscateBlocks` list includes all important ores and
  their `deepslate` variants.
* If it doesn't work above a certain y-level, check your `maxHeight` setting.

</details>

## Inside the obfuscation engine

<details>
    <summary>Obfuscation engine outline</summary>

* The following code outlines how the engine rewrites each sub-chunk sent to a player.

```cpp
// Called for every sub-chunk of a dimension with Anti-Xray enabled, if yIndex < maxHeight / 16.
// yIndex is the sub-chunk's index (y / 16), negative below y = 0.
void obfuscate(SubChunk& subChunk, int yIndex) {
    for (int y = 0; y < 16; y++) {
        for (int x = 0; x < 16; x++) {
            for (int z = 0; z < 16; z++) {
                auto block = subChunk.getBlock(x, y, z);
                // The block and its six neighbours (also in the neighbouring chunks) must be solid
                if (!isSolid(block) || !allSixNeighboursSolid(x, y, z)) continue;

                switch (engineMode) {
                case 0: // hide obfuscateBlocks behind mainBlock / mainBlockMinus
                    if (obfuscateBlocks.contains(block)) {
                        subChunk.setBlock(x, y, z, yIndex < 0 ? mainBlockMinus : mainBlock);
                    }
                    break;
                case 1: // a random block from obfuscateBlocks
                    subChunk.setBlock(x, y, z, obfuscateBlocks[rand() % obfuscateBlocks.size()]);
                    break;
                case 2: // the same block for the whole layer
                    subChunk.setBlock(x, y, z, obfuscateBlocks[(yIndex * 16 + y) % obfuscateBlocks.size()]);
                    break;
                }
            }
        }
    }
}

// When blocks change (a player starts breaking a block, an explosion, ...), the real solid blocks within
// updateRadius of each change are sent again (in engineMode 0 only those in obfuscateBlocks),
// so that newly exposed blocks show their real type.
```
</details>
