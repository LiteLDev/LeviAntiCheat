# LeviAntiCheat

![English](https://img.shields.io/badge/English-inactive?style=for-the-badge)
[![中文](https://img.shields.io/badge/简体中文-informational?style=for-the-badge)](README.zh.md)

Powerful anti-cheating for LeviLamina

## Install

```bash
lip install github.com/LiteLDev/LeviAntiCheat
```

## Usage

### Commands

`/lac ban <Player> [reason] [duration(minute)]` Ban a player manually  
`/lac unban <Player>` Pardon a player manually  
`/lac mute <Player> [duration(minute)]` Mute a player mamually  
`/lac unmute <Player>` Unmute a player mamually  
`/lac query <Player>` Query a player's status  
`/lac reload` Reload the configuration file

## Features

### Bugfixes

- Fix UI item duplication
- Fix incorrect teleport when going to bed while changing dimension
- Fix gateway falling block duplication
- Fix crafter crash
- Fix infinite block

### Client Cheating

- Prevent X-ray vision of minerals
- Prevent Toolbox using
- Prevent auto click
- Prevent reach
- Prevent fake name
- Prevent spawn xp orbs packet
- Prevent xp hack

### Inventory

- Check anvil enchantment
- Prevent automatic tool selection
- Prevent invalid items
- Prevent invalid NBT items
- Ban illegal items
- Check enchantment level
- Prevent invalid stack
- Prevent some resource packs cheating

### Movement

- Prevent interacting with containers while moving
- Prevent illegal movement such as fly, speed hack, wall hack
- Prevent no packet
- Prevent timer(another type of speed hack by adjust client's speed)

### Interaction

- Prevent illegal trades
- Prevent long item nametag
- Prevent spam(including selector spam, command spam etc.)

### Secure

- Prevent login flood attack
- Prevent bad packet
- Block suspicious clients

### World

- Fake seed
- Prevent illegal breaking
- Patch player's inventory when online mode is off

### Configuration file

For X-Ray prevention, see [here](anti_x_ray.md).

```jsonc
{
    "version": 12,
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
                        "minecraft:diamond_ore",
                        "minecraft:raw_iron_block",
                        "minecraft:emerald_ore",
                        "minecraft:deepslate_diamond_ore",
                        "minecraft:deepslate_emerald_ore",
                        "minecraft:calcite",
                        "minecraft:oak_planks",
                        "minecraft:tuff",
                        "minecraft:coal_ore",
                        "minecraft:deepslate_coal_ore",
                        "minecraft:iron_ore",
                        "minecraft:deepslate_iron_ore",
                        "minecraft:amethyst_block",
                        "minecraft:andesite",
                        "minecraft:gravel",
                        "minecraft:budding_amethyst",
                        "minecraft:deepslate",
                        "minecraft:smooth_basalt",
                        "minecraft:diorite",
                        "minecraft:stone",
                        "minecraft:dirt",
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
                        "minecraft:magma",
                        "minecraft:netherrack",
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
                }
            }
        },
        "antiToolbox": true,
        "antiFakeName": false,
        "antiSpawnXpOrbs": true,
        "antiXpHack": true,
        "antiBadPacket": true
    },
    "bugFixes": {
        "uiItemDuplicateFix": true,
        "sleepTeleportFix": true,
        "gatewayCopyFix": true,
        "crafterCrashFix": true,
        "infiniteBlockFix": true
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
            "maxCmdRate": 2, // Maximum command executing rate in 1 second
            "chatRateDuration": 10, // Chat rate check duration, in seconds
            "maxChatRate": 5, // Maximum chat rate in chatRateDuration seconds
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
            "maxMismatchDistance": 2.0,
            "detectLevel": 7
        },
        "timerCheck": {
            "enable": true,
            "maxPacketSpeed": 24,
            "detectLevel": 15
        },
        "noPacketCheck": {
            "enable": true,
            "maxNoPacketTime": 12
        }
    },
    "combat": {
        "autoClickCheck": {
            "enable": true,
            "maxCps": 12,
            "detectLevel": 10
        },
        "reachDistanceCheck": {
            "enable": true,
            "reachDistance": 3.200000047683716,
            "reachDistanceCreative": 5.300000190734863,
            "detectLevel": 7
        }
    },
    "securityMeasures": {
        "loginFloodCheck": false,
        "antiSuspiciousClient": true
    },
    "punish": {
        "enable": true,
        "enableBanWave": true,
        "kickVL": 100,
        "banVL": -1,
        "banDuration": 0 // In seconds
    }
}
```

## Development

You can develop your own punishment system based on [LeviPenalizeCheat](https://github.com/LiteLDev/LeviPenalizeCheat)

## Contributing

Ask questions by creating an issue.

Since this project is closed source, you can't contribute to the code directly. But if you have great ideas or suggestions, please feel free to contact us.

## Used Projectes

| Project          | License    | Link                                         |
| ---------------- | ---------- | -------------------------------------------- |
| parallel-hashmap | Apache-2.0 | https://github.com/greg7mdp/parallel-hashmap |
| libhat           | MIT        | https://github.com/BasedInc/libhat           |

## License

Copyright © LiteLDev

Without the prior written consent of LiteLDev, users shall not perform the following actions:

1. Decompile, disassemble and modify all or part of LeviAnticheat in any way, or reverse engineer any function or program of LeviAntiCheat.

2. Rent and sell LeviAntiCheat.
