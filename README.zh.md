# LeviAntiCheat

<img src="docs/logo.png" alt="" width="128" align="right">

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
`/lac mute <玩家> [时长(分钟)]` 手动禁言玩家  
`/lac unmute <玩家>` 解除玩家禁言  
`/lac query <玩家>` 查询玩家状态  
`/lac reload` 重载配置文件

## 特性

### 修复错误

- 修复UI物品复制问题
- 修复床超传问题
- 修复掉落方块复制问题
- 修复无效的大箱子配对导致客户端崩溃的问题
- 修复发射器在非活动区块中剪切实体导致的状态不一致问题
- 防止被点燃的硫磺立方体在被剪切后仍然爆炸
- 修复嵌套收纳袋展开时内容物重量与容量丢失的问题
- 防止存储容器身份变化时的物品复制
- 防止活塞推动方块实体时的容器物品复制
- 防止骑乘状态下跨维度时的物品复制与幽灵状态

### 客户端作弊

- 防止矿物透视
- 防止假名
- 防止发包生成经验球
- 防止刷经验
- 拦截恶意数据包（伪造的聊天、实体事件与子区块请求数据包）
- 防止连点器
- 防止长臂猿

### 物品栏

- 防止自动副手（未打开背包时将物品移入副手）
- 玩家死亡时归还遗留在UI槽位（如合成格）中的物品
- 检测无效物品
- 检查铁砧附魔
- 防止无效堆叠
- 防止无效NBT物品
- 封禁非法物品
- 检查附魔等级

### 移动

- 防止Timer（通过调整客户端速度的另一种加速作弊，也称变速齿轮）
- 防止停止发包
- 移除客户端对玩家动作的权威（默认关闭）

### 互动

- 防止非法交易
- 防止物品名称标签过长
- 防止刷屏（包括选择器刷屏、命令刷屏等）

### 安全

- 阻止可疑的客户端

### 世界

- 伪造种子
- 防止非法破坏
- 修复离线模式玩家背包丢失问题

### 配置文件

配置文件位于 `plugins/LeviAntiCheat/config/config.json`，默认配置如下。有关AntiXray子模块的详细说明，请参照[此文档](anti_x_ray.zh.md)。

```jsonc
{
    "version": 21, // 配置文件版本，请勿修改
    "consoleLog": true, // 是否在控制台记录日志
    "worldSafety": { // 世界安全配置
        "fakeSeed": { // 假种子配置
            "enable": true, // 是否向客户端发送假种子
            "randomSeed": false, // 是否使用随机种子
            "seed": 0 // randomSeed 为 false 时发送的种子值
        },
        "offlineInventoryProtection": false, // 离线模式背包保护
        "illegalBreakingCheck": true // 非法破坏检测
    },
    "cheatPrevention": { // 作弊预防配置
        "antiXray": { // 反矿物透视配置，见 anti_x_ray.zh.md
            "enable": true, // 是否启用反矿物透视
            "maxThreads": 4, // 改写区块的工作线程数，0 表示使用 CPU 线程数
            "debugDump": false, // 导出数据包用于调试
            "autoSolidCheck": true, // 自动判断实心方块
            "treatAddonBlocksAsNonSolid": true, // 将附加包中的方块视为非实心方块
            "dimensions": { // 维度配置
                "nether": { // 下界配置
                    "enable": true, // 是否在该维度启用
                    "engineMode": 1, // 引擎模式：0、1 或 2
                    "maxHeight": 128, // 只混淆此 Y 坐标以下的方块，必须是 16 的倍数
                    "updateRadius": 2, // 方块变化时重新发送周围真实方块的半径
                    "obfuscateBlocks": [ // 混淆方块
                        "minecraft:ancient_debris",
                        "minecraft:nether_gold_ore",
                        "minecraft:quartz_ore"
                    ]
                },
                "overworld": { // 主世界配置
                    "enable": true,
                    "engineMode": 1,
                    "maxHeight": 256,
                    "updateRadius": 2,
                    "obfuscateBlocks": [
                        "minecraft:coal_ore",
                        "minecraft:copper_ore",
                        "minecraft:deepslate_coal_ore",
                        "minecraft:deepslate_copper_ore",
                        "minecraft:deepslate_diamond_ore",
                        "minecraft:deepslate_emerald_ore",
                        "minecraft:deepslate_gold_ore",
                        "minecraft:deepslate_iron_ore",
                        "minecraft:deepslate_lapis_ore",
                        "minecraft:deepslate_redstone_ore",
                        "minecraft:diamond_ore",
                        "minecraft:emerald_ore",
                        "minecraft:gold_ore",
                        "minecraft:iron_ore",
                        "minecraft:lapis_ore",
                        "minecraft:raw_copper_block",
                        "minecraft:raw_iron_block",
                        "minecraft:redstone_ore"
                    ]
                }
            }
        },
        "antiFakeName": false, // 是否启用反假名
        "antiSpawnXpOrbs": true, // 是否启用反发包生成经验球
        "antiXpHack": true, // 是否启用反刷经验
        "antiBadPacket": true // 是否拦截恶意数据包
    },
    "bugFixes": { // Bug 修复配置
        "uiItemDuplicateFix": true, // UI物品复制修复
        "sleepTeleportFix": true, // 床超传修复
        "fallingBlockCopyFix": true, // 掉落方块复制修复
        "chunkChestCrashFix": true, // 大箱子配对崩溃修复
        "dispenserShearTickFix": true, // 发射器在非活动区块中剪切实体修复
        "sulfurCubeShearFuseFix": true, // 硫磺立方体剪切后爆炸修复
        "nestedBundleWeightFix": true, // 嵌套收纳袋重量与容量修复
        "bundleContainerIdentityFix": true, // 存储容器身份变化复制修复
        "blockActorContainerMoveFix": true, // 活塞推动容器复制修复
        "mountedDimensionTransferFix": true // 骑乘跨维度复制修复
    },
    "inventoryManagement": { // 物品管理配置
        "antiAutoOffhand": true, // 是否启用反自动副手
        "rectifyUiItemDrop": true, // 玩家死亡时归还UI槽位中的物品
        "invalidItemDetection": true, // 无效物品检测
        "anvilEnchantLimits": true, // 铁砧附魔限制
        "invalidStackDetection": true, // 无效堆叠检测
        "antiInvalidNbtItem": true, // 反无效NBT物品
        "banItem": { // 禁用物品配置
            "enable": true, // 是否启用禁用物品
            "blacklist": [] // 禁用的物品名称
        },
        "enchantCheck": { // 附魔检查
            "enable": false, // 是否启用附魔检查
            "maxEnchantLevel": { // 各附魔的最大等级
                "example_enchant": 5 // 示例附魔
            }
        }
    },
    "playerInteractions": { // 玩家交互配置
        "illegallyTradeRestrictions": true, // 非法交易限制
        "antiSpam": { // 反刷屏
            "enable": true, // 是否启用反刷屏
            "maxChatLength": 300, // 最大聊天长度
            "maxCmdRate": 2, // 一秒钟内最高指令速率
            "chatRateDuration": 10, // 聊天速率检查间隔，以秒为单位
            "maxChatRate": 5, // chatRateDuration秒内最高聊天速率
            "disableSelector": true // 禁止玩家在命令中使用目标选择器
        },
        "itemNameLengthCheck": { // 物品名称长度检查
            "enable": true, // 是否启用物品名称长度检查
            "maxStringLength": 90 // 最大字符串长度
        }
    },
    "movement": { // 移动检测
        "timerCheck": { // 变速齿轮检测
            "enable": true, // 是否启用变速齿轮检测
            "maxPacketSpeed": 24, // 每秒最多的移动输入数据包数
            "detectLevel": 15 // 检测级别
        },
        "noPacketCheck": { // 停止发包检测
            "enable": true, // 是否启用停止发包检测
            "maxNoPacketTime": 12 // 最长不发包时间，以秒为单位
        },
        "disablePlayerActionsAuthority": false // 移除客户端对玩家动作的权威
    },
    "combat": { // 战斗检测
        "autoClickCheck": { // 连点器检测
            "enable": true, // 是否启用连点器检测
            "maxCps": 12, // 最大每秒点击次数
            "detectLevel": 10 // 检测级别
        },
        "reachDistanceCheck": { // 攻击距离检测
            "enable": true, // 是否启用攻击距离检测
            "reachDistance": 3.200000047683716, // 除创造模式外最大攻击范围
            "reachDistanceCreative": 5.300000190734863, // 创造模式最大攻击范围
            "detectLevel": 7 // 检测级别
        }
    },
    "securityMeasures": { // 安全措施
        "antiSuspiciousClient": true // 阻止可疑的客户端
    },
    "punish": { // 惩罚配置
        "enable": true, // 是否启用惩罚
        "enableBanWave": true, // 是否启用封禁潮
        "kickVL": 100, // 踢出违规值
        "banVL": -1, // 封禁违规值，-1 表示不封禁
        "banDuration": 0, // 封禁时长，以秒为单位，0 表示永久
        "checkTypeViolationMap": { // 每种检测增加的违规值
            "IllegalTrade": 90,
            "AutoClick": 20,
            "InvalidFilterString": 50,
            "IllegalBreaking": 20,
            "Reach": 20,
            "SpawnXpOrbs": 90,
            "Timer": 20,
            "Spam": 20,
            "InvalidNbtItem": 90,
            "InvalidAnvilEnchant": 90,
            "AutoOffhand": 70,
            "BanItem": 50,
            "InvalidEnchantLevel": 50,
            "InvalidGetItem": 45,
            "InvalidStackItem": 90,
            "MessageTooLong": 10,
            "CommandSpam": 50,
            "XpHack": 90,
            "NoPacket": 20,
            "BadPacket": 90
        }
    }
}
```

## 拓展

请参考 [LeviPenalizeCheat](https://github.com/LiteLDev/LeviPenalizeCheat) 了解事件的外部处理与拓展功能方式

## 贡献

通过创建Issue提问。

由于该项目是闭源的，您无法直接对代码进行贡献。但是如果你有很棒的点子或想法，欢迎与我们联系。

## 使用的开源项目

| Project          | License    | Link                                         |
| ---------------- | ---------- | -------------------------------------------- |
| parallel-hashmap | Apache-2.0 | https://github.com/greg7mdp/parallel-hashmap |
| libhat           | MIT        | https://github.com/BasedInc/libhat           |

## 许可证

版权所有 © LeviMC

未经LeviMC事先书面同意，用户不得实施下列行为：

1. 反编译（de-compile）、反汇编（disassemble）和任何方式修改LeviAntiCheat的全部或部分内容，或对LeviAntiCheat任何功能或程序进行反向工程（reverse engineering）。

2. 出租、销售LeviAntiCheat。
