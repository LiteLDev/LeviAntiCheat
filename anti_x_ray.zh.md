# 配置反矿物透视

> 原作者为 PaperMC 项目

LeviAntiCheat 包含基于混淆的反矿物透视功能，有三种模式，可以针对每个世界进行配置。

反矿物透视有三种不同的模式。`engine-mode: 1` 将指定的方块（`hidden-blocks`）替换为其他“假”方块，如石头（在 y < 0 时为深板岩，配置中具体指明）、地狱岩或末地石，取决于所在的维度。相比之下，`engine-mode: 2` 会用随机生成的`hidden-blocks`替换`hidden-blocks`和`replacement-blocks`。`engine-mode: 3` 的工作方式类似于`engine-mode: 2`，但不是随机化每个方块，而是随机化每个区块的每一层。

> 注意：只有当方块的六个面都被 HiddenBlocks 或 ReplacementBlocks 覆盖时，才会对该方块进行混淆。

以下图片[^1]展示了在推荐配置下，对于使用矿物透视的玩家，每种模式在主世界和地狱中的效果。

[^1]:
    图片设计由 `Oberfail` 提供，最初发布在
    [PaperMC Discord](https://discord.gg/papermc)。

![主世界反矿物透视对比](https://github.com/PaperMC/docs/blob/main/docs/paper/admin/how-to/assets/anti-xray-overworld.png)
![地狱反矿物透视对比](https://github.com/PaperMC/docs/blob/main/docs/paper/admin/how-to/assets/anti-xray-nether.png)

特别是在客户端，`engine-mode: 1` 的计算成本更低，而`engine-mode: 2` 可能更能有效防止矿物透视。在`engine-mode: 1`中，只有完全被实心方块覆盖的矿物才会被隐藏。暴露在洞穴空气中或湖泊水中的矿物不会被隐藏。在`engine-mode: 2`中，假矿物会阻碍真实方块的视线。`engine-mode: 3` 可以在加入游戏时减少约一半的网络负载，并有助于区块数据包的压缩。

> # 反矿物透视绕过方法
> 
> **种子反演**：另一种攻击方式是利用 Minecraft 世界生成的确定性特征。如果客户端能够获取到世界种子，就可以知道每个生成矿物的真实位置，完全绕过反矿物透视。
> 
> **暴露在空气中的矿物**：在`engine-mode: 1`、`engine-mode: 2`和`engine-mode: 3`中，客户端可能会看到暴露在空气中的矿物。

## 推荐配置

以下是`engine-mode: 1`、`engine-mode: 2`和`engine-mode: 3`的推荐配置：

### `engine-mode: 1`

<details>
  <summary>默认世界配置</summary>

```json
"overworld": {
    "Enable": true,
    "EngineMode": 1,
    "UpdateRadius": 2.0,
    "MaxBlockHeight": 64,
    "HiddenBlocks": [
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
    "ReplacementBlocks": [
        "minecraft:stone",
        "minecraft:deepslate"
    ],
    "SolidBlocks": [
        "minecraft:calcite",
        "minecraft:oak_planks",
        "minecraft:tuff",
        "minecraft:amethyst_block",
        "minecraft:andesite",
        "minecraft:budding_amethyst",
        "minecraft:gravel",
        "minecraft:deepslate",
        "minecraft:diorite",
        "minecraft:smooth_basalt",
        "minecraft:dirt",
        "minecraft:stone",
        "minecraft:granite"
    ]
}
```

</details>

<details>
  <summary>地狱配置</summary>

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
    ],
    "SolidBlocks": [
        "minecraft:netherrack",
        "minecraft:magma",
        "minecraft:blackstone",
        "minecraft:basalt",
        "minecraft:crimson_nylium",
        "minecraft:warped_nylium",
        "minecraft:gravel"
    ]
}
```


</details>

</details>

### `engine-mode: 2`和`engine-mode: 3`

<details>
  <summary>默认世界配置</summary>

```json
"overworld": {
    "Enable": true,
    "EngineMode": 2,
    "UpdateRadius": 2.0,
    "MaxBlockHeight": 64,
    "HiddenBlocks": [
        "minecraft:copper_ore",
        "minecraft:raw_copper_block",
        "minecraft:deepslate_copper_ore",
        "minecraft:diamond_ore",
        "minecraft:deepslate_diamond_ore",
        "minecraft:gold_ore",
        "minecraft:deepslate_gold_ore",
        "minecraft:iron_ore",
        "minecraft:raw_iron_block",
        "minecraft:deepslate_iron_ore",
        "minecraft:lapis_ore",
        "minecraft:deepslate_lapis_ore",
        "minecraft:redstone_ore",
        "minecraft:deepslate_redstone_ore",
        "minecraft:coal_ore",
        "minecraft:deepslate_coal_ore"
    ],
    "ReplacementBlocks": [
        "minecraft:diamond_ore",
        "minecraft:deepslate_diamond_ore",
        "minecraft:emerald_ore",
        "minecraft:deepslate_emerald_ore",
        "minecraft:coal_ore",
        "minecraft:deepslate_coal_ore",
        "minecraft:iron_ore",
        "minecraft:raw_iron_block",
        "minecraft:deepslate_iron_ore",
        "minecraft:amethyst_block",
        "minecraft:andesite",
        "minecraft:budding_amethyst",
        "minecraft:calcite",
        "minecraft:deepslate",
        "minecraft:diorite",
        "minecraft:dirt",
        "minecraft:granite",
        "minecraft:gravel",
        "minecraft:oak_planks",
        "minecraft:smooth_basalt",
        "minecraft:stone",
        "minecraft:tuff"
    ],
    "SolidBlocks": []
}
```

</details>

<details>
  <summary>地狱配置</summary>

```json
"nether": {
    "Enable": true,
    "EngineMode": 3,
    "UpdateRadius": 2.0,
    "MaxBlockHeight": 128,
    "HiddenBlocks": [
        "minecraft:basalt",
        "minecraft:blackstone",
        "minecraft:gravel",
        "minecraft:soul_soil",
        "minecraft:netherrack",
        "minecraft:soul_sand"
    ],
    "ReplacementBlocks": [
        "minecraft:ancient_debris",
        "minecraft:glowstone",
        "minecraft:bone_block",
        "minecraft:quartz_ore",
        "minecraft:magma_block",
        "minecraft:nether_bricks",
        "minecraft:nether_gold_ore",
        "minecraft:polished_blackstone_bricks"
    ],
    "SolidBlocks": []
}
```


</details>

## 常见问题解答、常见错误及支持

<details>
  <summary>我仍然可以看到（部分）矿物 / 使用透视</summary>

如上所述，即使启用了反矿物透视，仍然可以看到（部分）矿物的原因有以下几个：

* 矿物高于配置的 `max-block-height` 值。
* 反矿物透视无法隐藏暴露在空气中或其他透明方块（例如洞穴中的矿物）的矿物。原则上，这也适用于`engine-mode: 2`和`engine-mode: 3`，但通常情况下，假矿物会阻碍真实方块的视线。要隐藏这些暴露的矿物，需要额外的插件。
* 方块类型在配置的方块列表中缺失。这可能是由于使用了过时的配置文件。

</details>

