# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.2.5] - 2024-05-23

### Changed

- AntiXray: send block update packet manually

### Fixed

- Fix AntiLoginFlood

## [0.2.4] - 2024-05-18

### Fixed

- Fix a problem of AntiXray

## [0.2.3] - 2024-05-07

### Fixed

- Fix AntiXray proxy chunk sync

## [0.2.2] - 2024-05-03

### Fixed

- Try fix an AntiXray's bug

## [0.2.1] - 2024-05-02

### Fixed

- Fix DecoratedPotLootTableFix [#9]

## [0.2.0] - 2024-04-28

### Changed

- Adapt to LeviLamina 0.12.x

## [0.1.5] - 2024-04-26

### Changed

- Revert "Let AntiXRay send block update directly"

## [0.1.4] - 2024-04-22

### Changed

- Let AntiXRay send block update directly
- Use SystemTimeScheduler

## [0.1.3] - 2024-04-18

### Fixed

- Fix event logic
- Fix errorneous judgement of BadPacket
- Fix a logic problem in punish

## [0.1.2] - 2024-04-18

### Added

- Add AntiBadPacket
- Add DecoratedPotLootTableFix
- Add PlayerCheatEvent
- Add PlayerBanWaveEvent
- Add enableBanWave configuration

### Fixed

- Fix AntiXRay hidden block behavior
- Fix AntiXRay solid map
- Fix IllegalBreakingCheck
- Ignore non-standard layer block update

## [0.1.1] - 2024-04-17

### Added

- Add disableSelector config
- Add GatewayCopyFix

### Changed

- Remove ContainerMoveCheck
- Rewrite IllegalMovementCheck

[#9]: https://github.com/LiteLDev/LeviAntiCheat/issues/9

[0.2.5]: https://github.com/LiteLDev/LeviAntiCheat/compare/v0.2.4...v0.2.5
[0.2.4]: https://github.com/LiteLDev/LeviAntiCheat/compare/v0.2.3...v0.2.4
[0.2.3]: https://github.com/LiteLDev/LeviAntiCheat/compare/v0.2.2...v0.2.3
[0.2.2]: https://github.com/LiteLDev/LeviAntiCheat/compare/v0.2.1...v0.2.2
[0.2.1]: https://github.com/LiteLDev/LeviAntiCheat/compare/v0.2.0...v0.2.1
[0.2.0]: https://github.com/LiteLDev/LeviAntiCheat/compare/v0.1.5...v0.2.0
[0.1.5]: https://github.com/LiteLDev/LeviAntiCheat/compare/v0.1.4...v0.1.5
[0.1.4]: https://github.com/LiteLDev/LeviAntiCheat/compare/v0.1.3...v0.1.4
[0.1.3]: https://github.com/LiteLDev/LeviAntiCheat/compare/v0.1.2...v0.1.3
[0.1.2]: https://github.com/LiteLDev/LeviAntiCheat/compare/v0.1.1...v0.1.2
[0.1.1]: https://github.com/LiteLDev/LeviAntiCheat/releases/tag/v0.1.1
