# TeleportPack Plugin Wiki

## Overview

TeleportPack is a powerful multi-world teleportation plugin that provides the following core features:

- Precise coordinate teleportation
- Random safe location teleportation
- Return to last position
- Cross-world return
- Intelligent fallback teleportation
- Custom respawn points
- Economic system integration
- Rich visual effects

## Installation Guide

### Basic Installation

1. Place the plugin JAR file into the server's plugins folder
2. Restart the server
3. Configuration files will be automatically generated on first run
4. Modify config.yml as needed

### Dependency Plugins

- **Required**: None

- Recommended

  :

  - Vault (for economic system)
  - PlaceholderAPI (for condition checks)

## Command List

| Command     | Description                                    | Usage                                         | Permission                   |
| :---------- | :--------------------------------------------- | :-------------------------------------------- | :--------------------------- |
| /tp         | Teleport to specified coordinates              | /tp <world> <x> <y> <z></z></y></x></world>   | teleportpack.tp              |
| /rtp        | Random teleport                                | /rtp                                          | teleportpack.rtp             |
| /back       | Return to last position in the same world      | /back                                         | teleportpack.back.use        |
| /backworld  | Return to last position in specified world     | /backworld <world></world>                    | teleportpack.back.crossworld |
| /smartback  | Intelligent return (prioritize world position) | /smartback                                    | teleportpack.smartback       |
| /setrespawn | Set world respawn point                        | /setrespawn <world> [x y z yaw pitch]</world> | teleportpack.admin           |
| /tpreload   | Reload configuration                           | /tpreload                                     | teleportpack.admin           |

## Permission Nodes

| Permission Node              | Description               | Default |
| :--------------------------- | :------------------------ | :------ |
| teleportpack.*               | All permissions           | op      |
| teleportpack.tp              | Use /tp command           | true    |
| teleportpack.rtp             | Use /rtp command          | true    |
| teleportpack.back.use        | Use /back command         | true    |
| teleportpack.back.crossworld | Use /backworld command    | true    |
| teleportpack.smartback       | Use /smartback command    | op      |
| teleportpack.respawn         | Use custom respawn points | true    |
| teleportpack.admin           | Admin commands            | op      |
| teleportpack.bypass.cost     | Bypass teleport costs     | false   |
| teleportpack.bypass.cooldown | Bypass cooldown times     | false   |

## Configuration Details

### Basic Configuration (config.yml)

```
teleport:
  delay: 3               # Teleport delay (seconds)
  allow-movement: false  # Whether to allow movement during teleport
  cooldown: 10           # Global cooldown time (seconds)
  
  # Title settings
  title:
    enabled: true
    main: "&aTeleporting!"
    sub: "&7Please wait {countdown} seconds..."
  
  # Particle effects
  particles:
    enabled: true
    type: PORTAL         # Particle type
    count: 50            # Particle count
  
  # Sound effects
  sounds:
    enabled: true
    start: BLOCK_PORTAL_TRIGGER      # Start sound
    complete: ENTITY_ENDERMAN_TELEPORT # Complete sound
```

### Random Teleport Configuration

```
random-teleport:
  target-world: world    # Default target world
  max-attempts: 20       # Maximum attempts
  safe-check: true       # Whether to check for safe locations
  
  # World-specific settings
  worlds:
    world:
      enabled: true
      min-range: 100     # Minimum range
      max-range: 5000    # Maximum range
      
      # Fixed height settings
      fixed-height:
        enabled: false
        min-y: 60
        max-y: 100
      
      # Terrain restrictions
      terrain:
        allow-water: false
        allow-lava: false
        allowed-blocks:  # Allowed landing blocks
          - GRASS_BLOCK
          - DIRT
        forbidden-blocks: # Forbidden landing blocks
          - CACTUS
      
      # Excluded biomes
      excluded-biomes:
        - OCEAN
```

### Return System Configuration

```
back:
  enabled: true
  allow-in-same-world: true    # Allow same-world return
  allow-cross-world: true      # Allow cross-world return
  expire-time: 600             # Location record expiration time (seconds)
  clear-on-death: true         # Clear records on death
  cross-world-extra-cost: 100  # Extra cost for cross-world
```

### Economic System Configuration

```
costs:
  enabled: true
  tp:
    money: 100    # Normal teleport cost
    conditions:   # Usage conditions
      - "%player_level% >= 10"
    condition-messages: # Messages for unmet conditions
      - "&cYou need at least level 10!"
```

### Intelligent Fallback Command Configuration

```
fork-command:
  enabled: true
  command-name: "smartback"
  permission: "teleportpack.smartback"
  primary-cmd: "backworld world"  # Primary command
  fallback-cmd: "rtp"             # Fallback command
  messages:
    executing-primary: "&aReturning to your previous location!"
    executing-fallback: "&aNo previous location, random teleporting!"
```

## Feature Highlights

### 1. Intelligent Location Recording

- Automatically records the player's last position in each world
- Configurable expiration time
- Optional clearing of records on death

### 2. Safe Random Teleport

- Intelligent detection of safe landing points
- Configurable teleport range
- Biome and block filtering

### 3. Complete Economic System

- Supports Vault economy
- Independent costs for each teleport type
- Usage condition checks

### 4. Visual Effects

- Configurable particle effects
- Teleport progress titles
- Custom sound effects

## Common Issues

**Q: Why does random teleport fail?** A: Possible reasons:

1. No safe location found (try increasing max-attempts)
2. Target world not enabled (check worlds.<world>.enabled)</world>
3. Player does not meet conditions (check costs.rtp.conditions)

**Q: How to reset a player's cooldown time?** A: Admins can use the command:

```
/plugman reload TeleportPack
```

**Q: Why isn't the custom respawn point working?** A: Ensure:

1. respawn.enabled is set to true
2. Player has teleportpack.respawn permission
3. Not respawning at bed or respawn anchor
