# LeviAntiCheat

<img src="docs/logo.png" alt="" width="128" align="right">

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
`/lac mute <Player> [duration(minute)]` Mute a player manually  
`/lac unmute <Player>` Unmute a player manually  
`/lac query <Player>` Query a player's status  
`/lac reload` Reload the configuration file

## Features

### Bugfixes

- Fix item duplication through UI slots
- Fix incorrect teleport when going to bed while changing dimension
- Fix falling block duplication
- Fix client crashes caused by invalid double chest pairing
- Fix state inconsistencies when dispensers shear entities outside ticking chunks
- Prevent primed sulfur cubes from exploding after being sheared
- Preserve the weight and capacity of nested bundle contents when flattening
- Prevent item duplication when a storage container's identity changes
- Prevent container item duplication when pistons move block actors
- Prevent item duplication and ghost states during mounted dimension transfers

### Client Cheating

- Prevent X-ray vision of ores
- Prevent fake name
- Prevent spawn xp orbs packet
- Prevent xp hack
- Prevent bad packets (forged chat, actor event and sub-chunk request packets)
- Prevent auto click
- Prevent reach

### Inventory

- Prevent auto offhand (moving items into the offhand without opening the inventory)
- Return items left in UI slots (such as the crafting grid) when a player dies
- Detect invalid items
- Check anvil enchantment
- Prevent invalid stack
- Prevent invalid NBT items
- Ban illegal items
- Check enchantment level

### Movement

- Prevent timer (another type of speed hack by adjusting the client's speed)
- Prevent no packet
- Remove the client's authority over player actions (disabled by default)

### Interaction

- Prevent illegal trades
- Prevent long item nametag
- Prevent spam (including selector spam, command spam etc.)

### Secure

- Block suspicious clients

### World

- Fake seed
- Prevent illegal breaking
- Patch player's inventory when online mode is off

### Configuration file

The configuration file is `plugins/LeviAntiCheat/config/config.json`. The default configuration is shown below. For X-Ray prevention, see [here](anti_x_ray.md).

```jsonc
{
    "version": 21, // Configuration file version, do not change
    "consoleLog": true, // Log detections to the console
    "worldSafety": {
        "fakeSeed": {
            "enable": true, // Send a fake seed to clients
            "randomSeed": false, // Use a random fake seed
            "seed": 0 // The fake seed to send when randomSeed is false
        },
        "offlineInventoryProtection": false, // Patch player's inventory when online mode is off
        "illegalBreakingCheck": true // Prevent illegal breaking
    },
    "cheatPrevention": {
        "antiXray": { // See anti_x_ray.md
            "enable": true,
            "maxThreads": 4, // Worker threads for rewriting chunks, 0 = number of CPU threads
            "debugDump": false, // Dump packets for debugging
            "autoSolidCheck": true, // Detect solid blocks automatically
            "treatAddonBlocksAsNonSolid": true, // Treat blocks from add-ons as non-solid
            "dimensions": {
                "nether": {
                    "enable": true,
                    "engineMode": 1, // 0, 1 or 2
                    "maxHeight": 128, // Only obfuscate below this Y level, must be a multiple of 16
                    "updateRadius": 2, // Radius of real blocks resent around a changed block
                    "obfuscateBlocks": [
                        "minecraft:ancient_debris",
                        "minecraft:nether_gold_ore",
                        "minecraft:quartz_ore"
                    ]
                },
                "overworld": {
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
        "antiFakeName": false, // Prevent fake name
        "antiSpawnXpOrbs": true, // Prevent spawn xp orbs packet
        "antiXpHack": true, // Prevent xp hack
        "antiBadPacket": true // Prevent bad packets
    },
    "bugFixes": {
        "uiItemDuplicateFix": true, // Fix item duplication through UI slots
        "sleepTeleportFix": true, // Fix incorrect teleport when going to bed while changing dimension
        "fallingBlockCopyFix": true, // Fix falling block duplication
        "chunkChestCrashFix": true, // Fix client crashes caused by invalid double chest pairing
        "dispenserShearTickFix": true, // Fix dispensers shearing entities outside ticking chunks
        "sulfurCubeShearFuseFix": true, // Prevent primed sulfur cubes from exploding after being sheared
        "nestedBundleWeightFix": true, // Preserve nested bundle weight and capacity when flattening
        "bundleContainerIdentityFix": true, // Prevent duplication when a storage container's identity changes
        "blockActorContainerMoveFix": true, // Prevent duplication when pistons move containers
        "mountedDimensionTransferFix": true // Prevent duplication during mounted dimension transfers
    },
    "inventoryManagement": {
        "antiAutoOffhand": true, // Prevent auto offhand
        "rectifyUiItemDrop": true, // Return items left in UI slots when a player dies
        "invalidItemDetection": true, // Detect invalid items
        "anvilEnchantLimits": true, // Check anvil enchantment
        "invalidStackDetection": true, // Prevent invalid stack
        "antiInvalidNbtItem": true, // Prevent invalid NBT items
        "banItem": {
            "enable": true,
            "blacklist": [] // Banned item names
        },
        "enchantCheck": {
            "enable": false,
            "maxEnchantLevel": { // Maximum level of each enchantment
                "example_enchant": 5
            }
        }
    },
    "playerInteractions": {
        "illegallyTradeRestrictions": true, // Prevent illegal trades
        "antiSpam": {
            "enable": true,
            "maxChatLength": 300, // Maximum chat message length
            "maxCmdRate": 2, // Maximum command executing rate in 1 second
            "chatRateDuration": 10, // Chat rate check duration, in seconds
            "maxChatRate": 5, // Maximum chat rate in chatRateDuration seconds
            "disableSelector": true // Disallow target selectors in player commands
        },
        "itemNameLengthCheck": {
            "enable": true,
            "maxStringLength": 90 // Maximum item name length
        }
    },
    "movement": {
        "timerCheck": {
            "enable": true,
            "maxPacketSpeed": 24, // Maximum movement input packets per second
            "detectLevel": 15
        },
        "noPacketCheck": {
            "enable": true,
            "maxNoPacketTime": 12 // Maximum time without packets, in seconds
        },
        "disablePlayerActionsAuthority": false // Remove the client's authority over player actions
    },
    "combat": {
        "autoClickCheck": {
            "enable": true,
            "maxCps": 12, // Maximum clicks per second
            "detectLevel": 10
        },
        "reachDistanceCheck": {
            "enable": true,
            "reachDistance": 3.200000047683716, // Maximum reach outside creative mode
            "reachDistanceCreative": 5.300000190734863, // Maximum reach in creative mode
            "detectLevel": 7
        }
    },
    "securityMeasures": {
        "antiSuspiciousClient": true // Block suspicious clients
    },
    "punish": {
        "enable": true,
        "enableBanWave": true, // Enable ban waves
        "kickVL": 100, // Violation level to kick a player
        "banVL": -1, // Violation level to ban a player, -1 = never
        "banDuration": 0, // In seconds, 0 = permanent
        "checkTypeViolationMap": { // Violation level added for each detection
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

## Development

You can develop your own punishment system based on [LeviPenalizeCheat](https://github.com/LiteLDev/LeviPenalizeCheat)

## Contributing

Ask questions by creating an issue.

Since this project is closed source, you can't contribute to the code directly. But if you have great ideas or suggestions, please feel free to contact us.

## Used Projects

| Project          | License    | Link                                         |
| ---------------- | ---------- | -------------------------------------------- |
| parallel-hashmap | Apache-2.0 | https://github.com/greg7mdp/parallel-hashmap |
| libhat           | MIT        | https://github.com/BasedInc/libhat           |

## License

Copyright © LeviMC

Without the prior written consent of LeviMC, users shall not perform the following actions:

1. Decompile, disassemble and modify all or part of LeviAntiCheat in any way, or reverse engineer any function or program of LeviAntiCheat.

2. Rent and sell LeviAntiCheat.
