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
`/lac reload` 重载配置文件

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

有关AntiXray子模块的详细说明，请参照[此文档](anti_x_ray.zh.md).

```jsonc
{
    "version": 4, // 配置文件版本
    "consoleLog": true, // 是否在控制台记录日志
    "worldSafety": { // 世界安全配置
        "fakeSeed": { // 假种子配置
            "enable": true, // 是否启用假种子
            "randomSeed": false, // 是否启用随机种子
            "seed": 0 // 种子值
        },
        "offlineInventoryProtection": false, // 离线存储保护
        "illegalBreakingCheck": true // 非法破坏检测
    },
    "cheatPrevention": { // 作弊预防配置
        "antiXray": { // 反透视配置
            "enable": true, // 是否启用反透视
            "DimensionConfigs": { // 维度配置
                "overworld": { // 主世界配置
                    "Enable": true, // 是否启用反透视
                    "EngineMode": 2, // 引擎模式
                    "UpdateRadius": 2.0, // 更新半径
                    "MaxBlockHeight": 64, // 最大方块高度
                    "HiddenBlocks": [ // 隐藏的方块
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
                    "ReplacementBlocks": [ // 替换的方块
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
                    "SolidBlocks": [] // 实心方块
                },
                "nether": { // 下界配置
                    "Enable": true, // 是否启用反透视
                    "EngineMode": 1, // 引擎模式
                    "UpdateRadius": 1.0, // 更新半径
                    "MaxBlockHeight": 128, // 最大方块高度
                    "HiddenBlocks": [ // 隐藏的方块
                        "minecraft:ancient_debris",
                        "minecraft:nether_gold_ore",
                        "minecraft:quartz_ore"
                    ],
                    "ReplacementBlocks": [ // 替换的方块
                        "minecraft:netherrack"
                    ],
                    "SolidBlocks": [ // 实心方块
                        "minecraft:netherrack",
                        "minecraft:magma",
                        "minecraft:blackstone",
                        "minecraft:basalt",
                        "minecraft:crimson_nylium",
                        "minecraft:warped_nylium",
                        "minecraft:gravel"
                    ]
                },
                "the end": { // 末地配置
                    "Enable": false, // 是否启用反透视
                    "EngineMode": 1, // 引擎模式
                    "UpdateRadius": 2.0, // 更新半径
                    "MaxBlockHeight": 0, // 最大方块高度
                    "HiddenBlocks": [], // 隐藏的方块
                    "ReplacementBlocks": [], // 替换的方块
                    "SolidBlocks": [] // 实心方块
                },
                "nether(engine mode 2 or 3 example)": { // 下界（引擎模式2或3示例）
                    "Enable": true, // 是否启用反透视
                    "EngineMode": 3, // 引擎模式
                    "UpdateRadius": 2.0, // 更新半径
                    "MaxBlockHeight": 128, // 最大方块高度
                    "HiddenBlocks": [ // 隐藏的方块
                        "minecraft:ancient_debris",
                        "minecraft:glowstone",
                        "minecraft:bone_block",
                        "minecraft:quartz_ore",
                        "minecraft:magma_block",
                        "minecraft:nether_bricks",
                        "minecraft:nether_gold_ore",
                        "minecraft:polished_blackstone_bricks"
                    ],
                    "ReplacementBlocks": [ // 替换的方块
                        "minecraft:basalt",
                        "minecraft:blackstone",
                        "minecraft:gravel",
                        "minecraft:soul_soil",
                        "minecraft:netherrack",
                        "minecraft:soul_sand"
                    ],
                    "SolidBlocks": [] // 实心方块
                }
            }
        },
        "antiToolbox": true, // 是否启用反Toolbox
        "antiFakeName": true, // 是否启用反假名
        "antiSpawnXpOrbs": true, // 是否启用反生成经验球
        "antiXpHack": true, // 是否启用反经验值作弊
        "antiBadPacket": true // 是否启用反坏数据包
    },
    "bugFixes": { // Bug 修复配置
        "uiItemDuplicateFix": true, // UI物品复制修复
        "sleepTeleportFix": true, // 睡眠传送修复
        "gatewayCopyFix": true, // 折跃门复制修复
        "decoratedPotLootTableFix": true // 装饰罐战利品表修复
    },
    "inventoryManagement": { // 物品管理配置
        "antiAutoOffhand": true, // 是否启用反自动副手
        "rectifyUiItemDrop": true, // 是否纠正界面物品掉落
        "invalidItemDetection": true, // 无效物品检测
        "anvilEnchantLimits": true, // 铁砧附魔限制
        "invalidStackDetection": true, // 无效堆叠检测
        "antiInvalidNbtItem": true, // 反无效NBT物品
        "banItem": { // 禁用物品配置
            "enable": true, // 是否启用禁用物品
            "blacklist": [] // 黑名单物品
        },
        "enchantCheck": { // 附魔检查
            "enable": false, // 是否启用附魔检查
            "maxEnchantLevel": { // 最大附魔等级
                "example_enchant": 5 // 示例附魔
            }
        }
    },
    "playerInteractions": { // 玩家交互配置
        "illegallyTradeRestrictions": true, // 非法交易限制
        "antiSpam": { // 反垃圾信息
            "enable": true, // 是否启用反垃圾信息
            "maxChatLength": 300, // 最大聊天长度
            "maxRate": 5, // 最大发送速率
            "disableSelector": true // 禁用选择器
        },
        "itemNameLengthCheck": { // 物品名称长度检查
            "enable": true, // 是否启用物品名称长度检查
            "maxStringLength": 90 // 最大字符串长度
        }
    },
    "movement": { // 移动检测
        "illegalMovementCheck": { // 非法移动检测
            "enable": true, // 是否启用非法移动检测
            "maxMismatchDistance": 1.0, // 最大不匹配距离
            "triggerReplayDistance": 2.0, // 触发回放距离
            "detectLevel": 2 // 检测级别
        },
        "timerCheck": { // 变速齿轮检测
            "enable": true, // 是否启用变速齿轮检测
            "maxPacketSpeed": 24, // 最大数据包速度
            "detectLevel": 15 // 检测级别
        },
        "noPacketCheck": { // 无数据包检测
            "enable": true, // 是否启用无数据包检测
            "maxNoPacketTime": 5 // 最大无数据包时间
        }
    },
    "combat": { // 战斗检测
        "autoClickCheck": { // 自动点击检测
            "enable": true, // 是否启用自动点击检测
            "maxCps": 10, // 最大每秒点击次数
            "detectLevel": 10 // 检测级别
        },
        "reachDistanceCheck": { // 攻击距离检测
            "enable": true, // 是否启用攻击距离检测
            "detectLevel": 5 // 检测级别
        }
    },
    "securityMeasures": { // 安全措施
        "antiLoginFloodCheck": false // 登录洪流检测
    },
    "punish": { // 惩罚配置
        "enable": true, // 是否启用惩罚
        "enableBanWave": true, // 是否启用封波系统
        "kickVL": 100, // 踢出违反值
        "banVL": -1, // 封禁违反值
        "banDuration": 0 // 封禁时长
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
