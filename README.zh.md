# LeviAntiCheat

[![English](https://img.shields.io/badge/English-informational?style=for-the-badge)](README.md)
![中文](https://img.shields.io/badge/简体中文-inactive?style=for-the-badge)

为LeviLamina提供强大的反作弊支持

## 安装

```bash
lip install github.com/LiteLDev/LeviAntiCheat
```

## 使用

### 命令

`/lac ban <玩家> [原因] [时长(分钟)]` 手动封禁玩家  
`/lac unban <玩家>` 手动解封玩家

## 特性

### 修复错误

- 修复UI物品复制问题
- 修复床超传问题
- 折跃门刷掉落方块的问题

### 客户端作弊

- 防止矿物透视
- 防止使用Toolbox
- 防止连点器
- 防止长臂猿
- 防止假名
- 防止原地生成经验球
- 防止刷经验

### 物品栏

- 检查铁砧附魔
- 防止自动选择工具
- 防止无效物品
- 防止无效nbt物品
- 封禁非法物品
- 检查附魔等级
- 防止无效堆叠
- 防止某些资源包作弊

### 移动

- 防止在移动时与容器互动
- 防止非法移动，如飞行、加速、穿墙
- 防止停止发包
- 防止Timer（通过调整客户端速度的另一种加速作弊，也称变速齿轮）

### 互动

- 防止非法交易
- 防止物品名称标签过长
- 防止刷屏（包括选择器刷屏、命令刷屏等）

### 安全

- 防止Login泛洪攻击
- 修复空包刷屏

### 世界

- 伪造种子
- 防止非法破坏
- 修复离线模式玩家背包丢失问题

### 配置文件

有关AntiXray子模块的详细说明，请参照[此文档](anti_x_ray.md).

```jsonc
{
    "version": 4,
    "consoleLog": true,
    "worldSafety": {
        "fakeSeed": {
            "enable": true,
            "randomSeed": false,
            "seed": 0
        },
        "offlineInventoryProtection": false,
        "illegalBreakingCheck": true
    },
    "cheatPrevention": {
        "antiXray": {
            "enable": true,
            "DimensionConfigs": {
                "overworld": {
                    "Enable": true,
                    "EngineMode": 2,
                    "UpdateRadius": 2.0,
                    "MaxBlockHeight": 64,
                    "HiddenBlocks": [
                        "minecraft:copper_ore",
                        "minecraft:raw_copper_block",
                        "minecraft:deepslate_coal_ore",
                        "minecraft:deepslate_copper_ore",
                        "minecraft:diamond_ore",
                        "minecraft:deepslate_diamond_ore",
                        "minecraft:gold_ore",
                        "minecraft:iron_ore",
                        "minecraft:deepslate_gold_ore",
                        "minecraft:raw_iron_block",
                        "minecraft:deepslate_iron_ore",
                        "minecraft:lapis_ore",
                        "minecraft:deepslate_lapis_ore",
                        "minecraft:redstone_ore",
                        "minecraft:deepslate_redstone_ore",
                        "minecraft:coal_ore"
                    ],
                    "ReplacementBlocks": [
                        "minecraft:raw_iron_block",
                        "minecraft:emerald_ore",
                        "minecraft:diamond_ore",
                        "minecraft:deepslate_emerald_ore",
                        "minecraft:deepslate_diamond_ore",
                        "minecraft:coal_ore",
                        "minecraft:deepslate_coal_ore",
                        "minecraft:iron_ore",
                        "minecraft:deepslate_iron_ore",
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
                    ],
                    "SolidBlocks": []
                },
                "nether": {
                    "Enable": true,
                    "EngineMode": 1,
                    "UpdateRadius": 1.0,
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
                },
                "the end": {
                    "Enable": false,
                    "EngineMode": 1,
                    "UpdateRadius": 2.0,
                    "MaxBlockHeight": 0,
                    "HiddenBlocks": [],
                    "ReplacementBlocks": [],
                    "SolidBlocks": []
                },
                "nether(engine mode 2 or 3 example)": {
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
                    ],
                    "SolidBlocks": []
                }
            }
        },
        "antiToolbox": true,
        "antiFakeName": true,
        "antiSpawnXpOrbs": true,
        "antiXpHack": true,
        "antiBadPacket": true
    },
    "bugFixes": {
        "uiItemDuplicateFix": true,
        "sleepTeleportFix": true,
        "gatewayCopyFix": true,
        "decoratedPotLootTableFix": true
    },
    "inventoryManagement": {
        "antiAutoOffhand": true,
        "rectifyUiItemDrop": true,
        "invalidItemDetection": true,
        "anvilEnchantLimits": true,
        "invalidStackDetection": true,
        "antiInvalidNbtItem": true,
        "banItem": {
            "enable": true,
            "blacklist": []
        },
        "enchantCheck": {
            "enable": false,
            "maxEnchantLevel": {
                "example_enchant": 5
            }
        }
    },
    "playerInteractions": {
        "illegallyTradeRestrictions": true,
        "antiSpam": {
            "enable": true,
            "maxChatLength": 300,
            "maxRate": 5,
            "disableSelector": true
        },
        "itemNameLengthCheck": {
            "enable": true,
            "maxStringLength": 90
        }
    },
    "movement": {
        "illegalMovementCheck": {
            "enable": true,
            "maxMismatchDistance": 1.0,
            "triggerReplayDistance": 2.0,
            "detectLevel": 2
        },
        "timerCheck": {
            "enable": true,
            "maxPacketSpeed": 24,
            "detectLevel": 15
        },
        "noPacketCheck": {
            "enable": true,
            "maxNoPacketTime": 5
        }
    },
    "combat": {
        "autoClickCheck": {
            "enable": true,
            "maxCps": 10,
            "detectLevel": 10
        },
        "reachDistanceCheck": {
            "enable": true,
            "detectLevel": 5
        }
    },
    "securityMeasures": {
        "antiLoginFloodCheck": false
    },
    "punish": {
        "enable": true,
        "enableBanWave": true,
        "kickVL": 100,
        "banVL": -1,
        "banDuration": 0
    }
}
```

## 拓展

请参考 [LeviPenalizeCheat](https://github.com/LiteLDev/LeviPenalizeCheat) 了解事件的外部处理与拓展功能方式

## 贡献

通过创建Issue提问。

由于该项目是闭源的，您无法直接对代码进行贡献。但是如果你有很棒的点子或想法，欢迎与我们联系。

## 许可证

版权所有 © LiteLDev

未经LiteLDev事先书面同意，用户不得实施下列行为：

1. 反编译（de-compile）、反汇编（disassemble）和任何方式修改LeviAnticheat的全部或部分内容，或对LeviAntiCheat任何功能或程序进行反向工程（reverse engineering）。

1. 出租、销售LeviAntiCheat。
