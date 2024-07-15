# LeviAntiCheat

![English](https://img.shields.io/badge/English-inactive?style=for-the-badge)
[![中文](https://img.shields.io/badge/简体中文-informational?style=for-the-badge)](README.zh.md)

Powerful anti-cheating for LeviLamina

## Install

```bash
lip install github.com/LiteLDev/LeviAntiCheat
```

## Features

### Bugfixes

- Fix UI item duplication
- Fix sleep teleport
- Fix gateway copy

### Client Cheating

- Prevent X-ray vision of minerals
- Prevent Toolbox using
- Prevent auto click
- Prevent Reach
- Prevent fake name
- Prevent spawn xp orbs
- Prevent `xp` hack

### Inventory

- Check anvil enchantment
- Prevent automatic tool selection
- Prevent invalid items
- Prevent invalid nbt items
- Ban illegal items
- Check enchantment level
- Prevent invalid stack
- Prevent some resource packs cheating

### Movement

- Prevent interacting with containers while moving
- Prevent illegal movement such as fly, speed hack, wall hack
- Prevent NoPacket
- Prevent Timer(another type of speed hack by adjust client's speed)

### Interaction

- Prevent illegal trades
- Prevent long item nametag
- Prevent spam(including selector spam, command spam etc.)

### Secure

- Prevent LoginFlood attack
- Fix empty packet spam

### World

- Fake seed
- Prevent illegal breaking
- Patch player's inventory when online mode is off

## Usage

### Commands

`/lac ban <Player> [reason] [duration(minute)]` Ban a player manually  
`/lac unban <Player>` Pardon a player manually  
`/lac reload` Reload the configuration file

### Configuration file

For X-Ray prevention, see [here](anti_x_ray.md).

```jsonc
{
    "version": 5,
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
                        "minecraft:calcite",
                        "minecraft:oak_planks",
                        "minecraft:tuff",
                        "minecraft:deepslate_diamond_ore",
                        "minecraft:coal_ore",
                        "minecraft:deepslate_coal_ore",
                        "minecraft:iron_ore",
                        "minecraft:deepslate_iron_ore",
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
        "gatewayCopyFix": true
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
            "maxMismatchDistance": 2.0,
            "triggerReplayDistance": 3.0,
            "detectLevel": 3
        },
        "timerCheck": {
            "enable": true,
            "maxPacketSpeed": 24,
            "detectLevel": 15
        },
        "noPacketCheck": {
            "enable": true,
            "maxNoPacketTime": 10
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
        "emptyPacketFix": true,
        "antiLoginFloodCheck": false
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

## License

Copyright © LiteLDev

Without the prior written consent of LiteLDev, users shall not perform the following actions:

1. Decompile, disassemble and modify all or part of LeviAnticheat in any way, or reverse engineer any function or program of LeviAntiCheat.

2. Rent and sell LeviAntiCheat.
