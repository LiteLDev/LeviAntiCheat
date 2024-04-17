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

### 配置文件

For X-Ray prevention, see [here](anti_x_ray.md).

```jsonc
{
    "version": 1,
    "consoleLog": true, // 控制台日志
    "worldSafety": {
        "fakeSeed": { // 假种子
            "enable": true,
            "randomSeed": false,
            "seed": 0
        },
        "offlineInventoryProtection": false, // 防止离线服务器玩家丢背包
        "illegalBreakingCheck": true // 非法破坏检测
    },
    "cheatPrevention": {
        "antiXray": { // 反矿透
            "enable": true,
            "DimensionConfigs": {
                "overworld": {
                    "Enable": true,
                    "EngineMode": 2,
                    "UpdateRadius": 2.0,
                    "MaxBlockHeight": 64, // 最大高度
                    "HiddenBlocks": [
                        "minecraft:copper_ore",
                        "minecraft:deepslate_copper_ore",
                        "minecraft:raw_copper_block",
                        "minecraft:deepslate_coal_ore",
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
                        "minecraft:deepslate_redstone_ore",
                        "minecraft:coal_ore"
                    ],
                    "ReplacementBlocks": [
                        "minecraft:stone",
                        "minecraft:deepslate"
                    ]
                },
                "nether": {
                    "Enable": true,
                    "EngineMode": 3,
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
                },
                "the end": {
                    "Enable": false,
                    "EngineMode": 1,
                    "UpdateRadius": 2.0,
                    "MaxBlockHeight": 0,
                    "HiddenBlocks": [],
                    "ReplacementBlocks": []
                }
            }
        },
        "antiToolbox": true, // 反Toolbox
        "antiFakeName": true, // 反假名
        "antiSpawnXpOrbs": true, // 反刷经验
        "antiXpHack": true // 反刷经验
    },
    "bugFixes": {
        "uiItemDuplicateFix": true, // UI刷物修复
        "sleepTeleportFix": true // 睡眠传送修复
    },
    "inventoryManagement": {
        "antiAutoOffhand": true, // 阻止自动切换副手
        "rectifyUiItemDrop": true, // 防止通过材质包做到死亡不掉落
        "invalidItemDetection": true, // 非法物品检查
        "anvilEnchantLimits": true, // 铁站附魔限制
        "invalidStackDetection": true, // 反非法堆叠
        "antiInvalidNbtItem": true, // 反非法NBT物品
        "banItem": { // 禁用物品
            "enable": true,
            "blacklist": []
        },
        "enchantCheck": { // 附魔等级检查
            "enable": false,
            "maxEnchantLevel": {
                "example_enchant": 5
            }
        }
    },
    "playerInteractions": {
        "illegallyTradeRestrictions": true, // 非法交易限制
        "antiSpam": { // 反刷屏
            "enable": true,
            "maxChatLength": 60,
            "maxRate": 1
        },
        "itemNameLengthCheck": { // 物品最大名称长度
            "enable": true,
            "maxStringLength": 90
        }
    },
    "movement": {
        "containerMoveCheck": true, // 开背包移动
        "illegalMovementCheck": true, // 移动检测
        "timerCheck": { // 变速齿轮
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
        "autoClickCheck": { // 连点器
            "enable": true,
            "maxCps": 10, // 最大CPS
            "detectLevel": 10
        },
        "reachDistanceCheck": { // 长臂猿
            "enable": true,
            "detectLevel": 5
        }
    },
    "securityMeasures": {
        "antiLoginFloodCheck": false // 启用LoginFlood防护，如果您正在使用frp等代理服务，请勿启用
    },
    "punish": {
        "enable": true, // 启用内置惩罚系统
        "kickVL": 100, // 玩家VL达到此值后，将被踢出，-1为禁用
        "banVL": -1, // 玩家VL达到此值后，将被封禁，-1为禁用
        "banDuration": 0 // 封禁时长，以分钟为单位，0为永久
    }
}
```

## 特性

### 修复错误

- 修复UI物品复制问题
- 修复睡眠传送问题

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
- 防止NoPacket
- 防止Timer（通过调整客户端速度的另一种加速作弊，也称变速齿轮）

### 互动

- 防止非法交易
- 防止物品名称标签过长
- 防止刷屏（包括选择器刷屏、命令刷屏等）

### 安全

- 防止LoginFlood攻击

### 世界

- 伪造种子
- 防止非法破坏
- 修复离线模式玩家背包丢失问题

## 贡献

通过创建Issue提问。

由于该项目是闭源的，您无法直接对代码进行贡献。

## 许可证

版权所有 © LiteLDev
