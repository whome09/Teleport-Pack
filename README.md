# TeleportPack Plugin Wiki

------

## Overview

TeleportPack is a powerful multi-world teleportation plugin that provides a complete teleportation system for Minecraft servers. It supports random teleportation, fixed-point teleportation, location memory, spawn point settings, and other functions, and integrates an economic system and condition checking mechanism.

**Core Features**:

- Multi-world support
- Random teleportation with safe location detection
- Location memory and return function
- Spawn point management
- Economic system integration
- Condition restriction system
- Cross-plugin compatibility

------

## Feature List

|          Feature           |                         Description                          |
| :------------------------: | :----------------------------------------------------------: |
|      Random Teleport       | Find a safe location within a specified range for teleportation |
|      Location Memory       |     Record player locations, support cross-world returns     |
|        Spawn Point         |            Custom spawn positions for each world             |
|      Teleport Effects      |          Particle effects, sounds, title animations          |
|      Economic System       |                Teleport fees, money deduction                |
|      Condition Check       | Level, permission, and other teleport condition restrictions |
|        Smart Return        |           Intelligent fallback to random teleport            |
| Cross-Plugin Compatibility |          Support location memory from other plugins          |

------

## Installation Guide

### System Requirements

- Minecraft server 1.13+
- Java 17+
- Optional dependencies: Vault, PlaceholderAPI

### Installation Steps

1. Download the latest version of the plugin JAR file
2. Place the file in the server's plugins directory
3. Restart the server
4. The configuration file will be automatically generated on first run
5. Edit plugins/TeleportPack/config.yml as needed

### Dependency Installation

```
# Add to plugin.yml
softdepend: [Vault, PlaceholderAPI]
```

### Updating the Plugin

1. Stop the server
2. Backup the old configuration file
3. Replace the plugin JAR file
4. Restart the server

------

## Command Usage

### Basic Commands

|   Command   |               Parameters                |                         Description                          |         Example          |
| :---------: | :-------------------------------------: | :----------------------------------------------------------: | :----------------------: |
|     /tp     | <world> <x> <y> <z></z></y></x></world> |              Teleport to specified coordinates               |   /tp world 100 64 200   |
|    /rtp     |                 [world]                 |             Randomly teleport to a safe location             |    /rtp world_nether     |
|    /back    |                    -                    |     Return to the previous location in the current world     |          /back           |
| /backworld  |             <world></world>             |    Return to the previous location in the specified world    |     /backworld world     |
|  /respawn   |                 [world]                 |             Teleport to the world's spawn point              |    /respawn world_end    |
| /smartback  |                    -                    | Intelligent return (prioritize return to location, otherwise random teleport) |        /smartback        |
| /setrespawn |      <world> [coordinates]</world>      |                 Set the world's spawn point                  | /setrespawn world 0 80 0 |
|  /tpreload  |                    -                    |                 Reload plugin configuration                  |        /tpreload         |

### Command Usage Instructions

**Smart Return (smartback)**

- Prioritize executing /backworld [target world]
- If no location record exists, execute /rtp for random teleport
- The target world is set in the configuration (default: world)

**Cross-World Teleport**

- When using /backworld and /respawn, specify the target world
- Cross-world teleport has additional fees (configurable)

------

## Permission Management

### Permission List

|       Permission Node        | Default |        Description        |
| :--------------------------: | :-----: | :-----------------------: |
|       teleportpack.tp        |  true   |      Use /tp command      |
|       teleportpack.rtp       |  true   |     Use /rtp command      |
|    teleportpack.back.use     |  true   |     Use /back command     |
| teleportpack.back.crossworld |  true   |  Use /backworld command   |
|     teleportpack.respawn     |  true   |   Use /respawn command    |
|    teleportpack.smartback    |  true   |  Use /smartback command   |
|      teleportpack.admin      |   op    | Admin command permissions |
|   teleportpack.bypass.cost   |  false  |   Bypass teleport fees    |
| teleportpack.bypass.cooldown |  false  |   Bypass cooldown time    |
|        teleportpack.*        |   op    |      All permissions      |

### Permission Configuration Example

```
# Give the VIP player group all teleport permissions
permissions:
  vip:
    permissions:
      - teleportpack.tp
      - teleportpack.rtp
      - teleportpack.back.use
      - teleportpack.back.crossworld
      - teleportpack.bypass.cost
```

------

## Configuration Details

### Configuration File Structure

```
# Main parts of config.yml
teleport:
  delay: 3
  allow-movement: false
  cooldown: 10
  title: {...}
  particles: {...}
  sounds: {...}

random-teleport: {...}

costs: {...}

back: {...}

respawn: {...}

fork-command: {...}

messages: {...}
```

### Key Configuration Instructions

**Teleport Settings**

```
teleport:
  delay: 3 # Teleport delay (seconds)
  allow-movement: false # Whether to allow movement during teleport
  cooldown: 10 # Teleport cooldown time (seconds)
  
  # Title settings
  title:
    enabled: true
    main: "&aTeleporting!"
    sub: "&7Please wait {countdown} seconds..."
  
  # Particle effects
  particles:
    enabled: true
    type: PORTAL
    count: 50
  
  # Sound effects
  sounds:
    enabled: true
    start: BLOCK_PORTAL_TRIGGER # Start sound effect
    complete: ENTITY_ENDERMAN_TELEPORT # Complete sound effect
```

**Random Teleport Settings**

```
random-teleport:
  target-world: world # Default random teleport world
  worlds:
    world: # World name
      enabled: true
      min-range: 100 # Minimum range
      max-range: 5000 # Maximum range
      fixed-height: # Fixed height settings
        enabled: false
        min-y: 60
        max-y: 100
      terrain: # Terrain settings
        allow-water: false
        allow-lava: false
        allowed-blocks: [...] # Allowed blocks
        forbidden-blocks: [...] # Forbidden blocks
      excluded-biomes: [...] # Excluded biomes
  max-attempts: 20 # Maximum attempts
  safe-check: true # Whether to perform safety checks
```

**Cost Settings**

```
costs:
  enabled: true # Whether to enable the cost system
  tp: # /tp command cost
    money: 100
    conditions: [...] # Condition expressions
    condition-messages: [...] # Condition not met prompts
  rtp: {...} # /rtp command cost
  back: {...} # /back command cost
  respawn: {...} # /respawn command cost
```

**Return Location Settings**

```
back:
  enabled: true
  allow-in-same-world: true # Allow same-world returns
  allow-cross-world: true # Allow cross-world returns
  expire-time: 600 # Location memory time (seconds)
  clear-on-death: true # Clear location memory on death
  cross-world-extra-cost: 100 # Cross-world extra cost
```

**Spawn Point Settings**

```
respawn:
  enabled: true
  worlds:
    world: # World name
      x: 0
      y: 80
      z: 0
      yaw: 0
      pitch: 0
```

**Smart Command Settings**

```
fork-command:
  enabled: true
  command-name: "smartback"
  permission: "teleportpack.smartback"
  primary-cmd: "backworld world" # Primary command
  fallback-cmd: "rtp" # Fallback command
  messages:
    executing-primary: "&aReturning to your previous location in world!"
    executing-fallback: "&aNo previous location found, teleporting randomly!"
```

**Message System**

```
messages:
  prefix: "&6[TeleportPack] &r" # Message prefix
  teleporting: "&aTeleporting in &e{countdown} &aseconds..."
  teleport-success: "&aTeleport successful!"
  # ... Other messages
```

------

## Advanced Features

### Condition Expression System

Use condition expressions in cost configurations:

```
costs:
  tp:
    conditions:
      - "%player_level% >= 10"
    condition-messages:
      - "&cYou need at least level 10 to use this command!"
```

Supported placeholders:

- %player_level% - Player level
- %player_health% - Player health
- %vault_balance% - Player balance (requires Vault)
- Other PlaceholderAPI placeholders

### Cross-Plugin Compatibility

- Automatically record teleport locations from other plugins
- Support teleports from plugins like Essentials, Multiverse, etc.
- Record locations when players use teleports from any plugin

### API Integration

```
// Get plugin instance
TeleportPack plugin = TeleportPack.getInstance();

// Get player location manager
LocationManager locManager = plugin.getLocationManager();

// Set player location record
locManager.setLastLocation(player);

// Perform teleport
plugin.getTeleportManager().teleport(player, location, TeleportType.NORMAL_TP, 0);
```

------

## Common Issues

### Location Memory Not Working

1. Check if back.enabled is set to true
2. Ensure the player has the teleportpack.back.use permission
3. Check if the location has expired (default 10 minutes)

### Random Teleport Cannot Find Safe Location

1. Increase the max-attempts value (default 20)
2. Adjust terrain settings to allow more block types
3. Ensure the target world has random teleport enabled

### Economic System Not Working

1. Install Vault and an economy plugin (such as EssentialsX)
2. Ensure costs.enabled is set to true
3. Check if the player has sufficient money

### Cross-World Teleport Fails

1. Check if allow-cross-world is set to true
2. Ensure the target world is loaded
3. Check if the player has the teleportpack.back.crossworld permission
