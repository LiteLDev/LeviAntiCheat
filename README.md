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

### Configuration

For X-Ray prevention, see [here](anti_x_ray.md).

```jsonc
{
    "version": 2,
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
                },
                "overworld(engine mode 1 example)": {
                    "Enable": true,
                    "EngineMode": 1,
                    "UpdateRadius": 1.0,
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
                    ]
                },
                "the end": {
                    "Enable": false,
                    "EngineMode": 1,
                    "UpdateRadius": 2.0,
                    "MaxBlockHeight": 0,
                    "HiddenBlocks": [],
                    "ReplacementBlocks": []
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
                    ]
                }
            }
        },
        "antiToolbox": true,
        "antiFakeName": true,
        "antiSpawnXpOrbs": true,
        "antiXpHack": true
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
            "maxMismatchDistance": 1.0,
            "triggerReplayDistance": 2.0,
            "detectLevel": 5
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
        "kickVL": 100,
        "banVL": -1,
        "banDuration": 0
    }
}
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
- 

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

### World

- Fake seed
- Prevent illegal breaking
- Patch player's inventory when online mode is off

## Contributing

Ask questions by creating an issue.

Since this project is closed source, you can't contribute to the code directly.

## License

Copyright © LiteLDev
