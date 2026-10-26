# 配置反矿物透视

> 原作者为 PaperMC 项目

LeviAntiCheat 包含基于混淆的反矿物透视功能，有三种模式，可以针对每个维度进行配置。

反矿物透视有三种不同的模式。`engineMode: 0` 将指定的方块（`obfuscateBlocks`）替换为“假”方块 `mainBlock`（默认为 `minecraft:stone`），在 y < 0 时替换为 `mainBlockMinus`（默认为 `minecraft:deepslate`）。在下界或末地中，可将 `mainBlock` 设为 `minecraft:netherrack` 或 `minecraft:end_stone`。相比之下，`engineMode: 1` 会把每个被隐藏的实心方块替换为从 `obfuscateBlocks` 中随机选出的方块。`engineMode: 2` 的工作方式类似于 `engineMode: 1`，但不是随机化每个方块，而是按 y 坐标选择方块，同一层的方块都会被替换为同一种假方块。

> 注意：只有当方块本身是实心方块，且六个面都被实心方块覆盖时（见[实心方块](#实心方块)），才会对该方块进行混淆。只有 `maxHeight` 以下的方块会被混淆。

以下图片[^1]展示了在推荐配置下，对于使用矿物透视的玩家，每种模式在主世界和下界中的效果。图片来自 PaperMC，其引擎模式 1、2、3 分别对应这里的 `engineMode` 0、1、2。

[^1]:
    图片设计由 `Oberfail` 提供，最初发布在
    [PaperMC Discord](https://discord.gg/papermc)。

![主世界反矿物透视对比](https://github.com/PaperMC/docs/blob/main/src/content/docs/paper/admin/how-to/assets/anti-xray-overworld.png)
![下界反矿物透视对比](https://github.com/PaperMC/docs/blob/main/src/content/docs/paper/admin/how-to/assets/anti-xray-nether.png)

特别是在客户端，`engineMode: 0` 的计算成本更低，而 `engineMode: 1` 可能更能有效防止矿物透视。在 `engineMode: 0` 中，只有完全被实心方块覆盖的矿物才会被隐藏。暴露在洞穴空气中或湖泊水中的矿物不会被隐藏。在 `engineMode: 1` 中，假矿物会阻碍真实方块的视线。`engineMode: 2` 生成的子区块比 `engineMode: 1` 更规整，有助于区块数据包的压缩。

> # 反矿物透视绕过方法
> 
> **种子反演**：另一种攻击方式是利用 Minecraft 世界生成的确定性特征。如果客户端能够获取到世界种子，就可以知道每个生成矿物的真实位置，完全绕过反矿物透视。请保持 `worldSafety.fakeSeed` 开启。
> 
> **暴露在空气中的矿物**：在 `engineMode: 0`、`engineMode: 1` 和 `engineMode: 2` 中，客户端可能会看到暴露在空气中的矿物。

## 配置

反矿物透视在[配置文件](README.zh.md#配置文件)的 `cheatPrevention.antiXray` 中配置。

| 键 | 默认值 | 说明 |
| --- | --- | --- |
| `enable` | `true` | 是否启用反矿物透视 |
| `maxThreads` | `4` | 改写区块的工作线程数，`0` 表示使用 CPU 线程数 |
| `debugDump` | `false` | 导出改写前后的数据包用于调试 |
| `autoSolidCheck` | `true` | 自动判断实心方块，见[实心方块](#实心方块) |
| `treatAddonBlocksAsNonSolid` | `true` | 将不在 `minecraft:` 命名空间中的方块视为非实心方块 |
| `solidBlocks` | 未设置 | 可选。视为实心方块的方块 |
| `nonSolidBlocks` | 未设置 | 可选。始终不视为实心方块的方块 |
| `dimensions` | `overworld`、`nether` | 各维度的配置，键为维度名称 |

`dimensions` 中的每一项包含以下键。若维度名称或引擎模式无法识别，或 `maxHeight` 不是 16 的倍数，会在日志中报错，该维度不会启用反矿物透视。

| 键 | 说明 |
| --- | --- |
| `enable` | 是否在该维度启用反矿物透视 |
| `engineMode` | `0`、`1` 或 `2`，见上文 |
| `maxHeight` | 只混淆此 y 坐标以下的方块，必须是 16 的倍数 |
| `updateRadius` | 方块发生变化时，重新发送此半径内的真实方块 |
| `obfuscateBlocks` | `engineMode: 0`：要隐藏的方块。`engineMode: 1` 和 `2`：要显示的假方块 |
| `mainBlock` | 仅用于 `engineMode: 0`。y >= 0 处的假方块，未设置时为 `minecraft:stone` |
| `mainBlockMinus` | 仅用于 `engineMode: 0`。y < 0 处的假方块，未设置时为 `minecraft:deepslate` |

### 实心方块

当 `autoSolidCheck` 为 `true` 时，所有阻挡移动的完整立方体方块都是实心方块。`nonSolidBlocks` 中的方块，以及 `treatAddonBlocksAsNonSolid` 为 `true` 时来自附加包的方块，始终不是实心方块。`solidBlocks` 中列出的其他方块会被额外视为实心方块。当 `autoSolidCheck` 为 `false` 时，只有 `solidBlocks` 中列出的方块是实心方块。

## 推荐配置

以下是 `engineMode: 0`、`engineMode: 1` 和 `engineMode: 2` 的推荐配置，请将这些条目放入 `cheatPrevention.antiXray.dimensions` 中。

### `engineMode: 0`

<details>
  <summary>主世界配置</summary>

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
  <summary>下界配置</summary>

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

### `engineMode: 1` 和 `engineMode: 2`

这两种模式会替换每个被隐藏的实心方块，因此 `obfuscateBlocks` 只需列出要显示的假方块。

<details>
  <summary>主世界配置</summary>

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
  <summary>下界配置</summary>

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

## 常见问题解答、常见错误及支持

<details>
  <summary>我仍然可以看到（部分）矿物 / 使用透视</summary>

如上所述，即使启用了反矿物透视，仍然可以看到（部分）矿物的原因有以下几个：

* 矿物高于配置的 `maxHeight` 值。
* 反矿物透视无法隐藏暴露在空气中或其他非实心方块旁（例如洞穴中）的矿物。原则上，这也适用于 `engineMode: 1` 和 `engineMode: 2`，但通常情况下，假矿物会阻碍真实方块的视线。
* 使用 `engineMode: 0` 时，该方块类型不在 `obfuscateBlocks` 中。
* 该维度没有启用反矿物透视。请检查服务器日志中有关维度名称、`engineMode` 或 `maxHeight` 的错误。

</details>

<details>
  <summary>我添加了假方块，但透视看不到它们</summary>

如果你使用 `engineMode: 1` 或 `engineMode: 2`，并在 `obfuscateBlocks` 列表中添加了假方块，但在游戏中用透视看不到它们，可能有以下原因：

* 方块名称有误。无法识别的方块会在服务器日志中报告并被忽略。
* 该方块在你客户端的透视模组中被禁用，或没有被你的透视资源包显示。

使用 `engineMode: 0` 时，`obfuscateBlocks` 是要隐藏的方块，假方块是 `mainBlock` / `mainBlockMinus`。

</details>

<details>
  <summary>在 y = 0 以下或某些其他位置不起作用</summary>

* 使用 `engineMode: 0` 时，检查 y = 0 以下的假方块 `mainBlockMinus`。
* 矿物周围的方块没有被视为实心方块。当 `autoSolidCheck` 为 `false` 时，请将 `deepslate`、`tuff` 等方块或 `basalt` 等生物群系特有的方块加入 `solidBlocks`。另请检查 `nonSolidBlocks` 和 `treatAddonBlocksAsNonSolid`。
* 使用 `engineMode: 0` 时，你可能还需要检查 `obfuscateBlocks` 列表是否包含所有重要的矿物及其 `deepslate` 变种。
* 如果在某个 y 坐标以上不起作用，请检查 `maxHeight` 设置。

</details>

## 混淆引擎内部

<details>
    <summary>混淆引擎概要</summary>

* 以下代码概述了引擎如何改写发送给玩家的每个子区块。

```cpp
// 对启用了反矿物透视的维度中、yIndex < maxHeight / 16 的每个子区块调用。
// yIndex 是子区块的序号（y / 16），在 y = 0 以下为负数。
void obfuscate(SubChunk& subChunk, int yIndex) {
    for (int y = 0; y < 16; y++) {
        for (int x = 0; x < 16; x++) {
            for (int z = 0; z < 16; z++) {
                auto block = subChunk.getBlock(x, y, z);
                // 方块本身及其六个相邻方块（包括相邻区块中的方块）都必须是实心方块
                if (!isSolid(block) || !allSixNeighboursSolid(x, y, z)) continue;

                switch (engineMode) {
                case 0: // 用 mainBlock / mainBlockMinus 隐藏 obfuscateBlocks
                    if (obfuscateBlocks.contains(block)) {
                        subChunk.setBlock(x, y, z, yIndex < 0 ? mainBlockMinus : mainBlock);
                    }
                    break;
                case 1: // 从 obfuscateBlocks 中随机选一个方块
                    subChunk.setBlock(x, y, z, obfuscateBlocks[rand() % obfuscateBlocks.size()]);
                    break;
                case 2: // 同一层使用同一个方块
                    subChunk.setBlock(x, y, z, obfuscateBlocks[(yIndex * 16 + y) % obfuscateBlocks.size()]);
                    break;
                }
            }
        }
    }
}

// 方块发生变化时（玩家开始破坏方块、爆炸等），会重新发送每处变化周围 updateRadius 范围内的
// 真实实心方块（engineMode 0 下只发送 obfuscateBlocks 中的方块），让新暴露的方块显示真实类型。
```
</details>
