# 🎮 Command Usage Guide

## 📋 Command Overview

| Command | Description | Permission | Usage |
|---|---|---|---|
| `/rtp` | Random teleportation | `teleportpack.rtp` | `/rtp [world]` |
| `/tp` | Precise coordinate teleportation | `teleportpack.tp` | `/tp <world> <x> <y> <z>` |
| `/back` | Return to previous location | `teleportpack.back.use` | `/back` |
| `/backworld` | Cross-world return | `teleportpack.back.crossworld` | `/backworld <world>` |
| `/respawn` | Teleport to respawn point | `teleportpack.respawn` | `/respawn [world]` |
| `/setrespawn` | Set respawn point for a world | `teleportpack.admin` | `/setrespawn <world> [x] [y] [z]` |
| `/tpreload` | Reload plugin configuration | `teleportpack.admin` | `/tpreload` |
| `/smartback` | Smart return with fallback to random teleport | `teleportpack.smartback` | `/smartback` |

## 🎯 Player Commands Detailed

### 🎲 Random Teleport (/rtp)

**Basic Usage:**
```
/rtp
```
Randomly teleport to a safe location in the default world.

**Specify World:**
```
/rtp world_nether
```
Teleport to a random location in the Nether.

**Permission Requirements:**
- `teleportpack.rtp` - Use random teleportation
- `teleportpack.bypass.cooldown` - Bypass cooldown time
- `teleportpack.bypass.cost` - Bypass cost

**Notes:**
- Must wait for cooldown time (default 10 seconds)
- Requires payment (default 50 coins)
- Automatically finds safe locations

### 📍 Precise Teleport (/tp)

**Basic Usage:**
```
/tp world 100 64 200
```
Teleport to coordinates (100, 64, 200) in the main world.

**Full Usage:**
```
/tp world 100 64 200 90 0
```
Teleport to specified coordinates and set orientation (yaw 90, pitch 0).

**Permission Requirements:**
- `teleportpack.tp` - Use precise teleportation
- May need to meet level requirements (default level 10)

### 🔙 Return Function (/back)

**Basic Usage:**
```
/back
```
Return to the previous location in the current world.

**Cross-world Return:**
```
/backworld world_nether
```
Return to the previous location in the Nether.

**Permission Requirements:**
- `teleportpack.back.use` - Same-world return
- `teleportpack.back.crossworld` - Cross-world return

**Mechanism Explanation:**
- Records the last 10 teleportation locations
- Location expiration time: 10 minutes
- Clears location records on death

### 🏠 Respawn Point Teleport (/respawn)

**Basic Usage:**
```
/respawn
```
Teleport to the respawn point of the current world.

**Specify World:**
```
/respawn world_the_end
```
Teleport to the respawn point of the End.

**Permission Requirements:**
- `teleportpack.respawn` - Use respawn point teleportation

### 🤖 Smart Return (/smartback)

**Basic Usage:**
```
/smartback
```
Smart return mechanism:
1. First attempts to return to the previous location
2. If no previous location exists, executes random teleportation

**Permission Requirements:**
- `teleportpack.smartback` - Use smart return

## 🔧 Admin Commands

### 🎯 Set Respawn Point (/setrespawn)

**Basic Usage:**
```
/setrespawn world
```
Set the current location as the world's respawn point.

**Precise Setting:**
```
/setrespawn world 100 64 200 90 0
```
Set precise coordinates and orientation.

**Force Update:**
```
/setrespawn world 100 64 200 --force
```
Also update Multiverse respawn point.

**Parameter Explanation:**
- `<world>` - World name
- `[x]` - X coordinate (optional, defaults to player position)
- `[y]` - Y coordinate (optional)
- `[z]` - Z coordinate (optional)
- `[yaw]` - Yaw angle (optional)
- `[pitch]` - Pitch angle (optional)
- `[--force]` - Force update Multiverse respawn point

### 🔄 Reload Configuration (/tpreload)

**Usage:**
```
/tpreload
```
Reload plugin configuration files without restarting the server.

**Permission Requirements:**
- `teleportpack.admin` - Admin permissions

## 🎮 Usage Examples

### Scenario 1: New Player Random Teleport
```
# New player input
/rtp

# System prompt
[TeleportPack] Teleporting in 3 seconds...
[TeleportPack] Teleport successful!
```

### Scenario 2: VIP Player Precise Teleport
```
# VIP player input
/tp world_nether 100 70 200

# System prompt
[TeleportPack] Teleporting in 3 seconds...
[TeleportPack] Teleport successful!
```

### Scenario 3: Return to Death Point
```
# Player input after death
/back

# System prompt
[TeleportPack] Return successful!
```

### Scenario 4: Admin Setting Respawn Point
```
# Admin input
/setrespawn world 0 80 0 --force

# System prompt
[TeleportPack] Respawn point set for world world and synced to Multiverse!
```

## ⚡ Cooldown and Cost System

### Cooldown Time
- Default cooldown: 10 seconds
- Bypass permission: `teleportpack.bypass.cooldown`

### Cost System
| Command Type | Default Cost | Permission Bypass |
|---|---|---|
| `/rtp` | 50 coins | `teleportpack.bypass.cost` |
| `/tp` | 100 coins | `teleportpack.bypass.cost` |
| `/back` | 200 coins | `teleportpack.bypass.cost` |
| `/respawn` | Free | - |

### Condition Restrictions
- `/tp` command requires player level ≥ 10
- Additional conditions can be added through configuration

## 🎯 Practical Tips

### 1. Quick Home Setup
```
# Set home respawn point
/setrespawn world 100 64 200

# Return home anytime
/respawn
```

### 2. World Exploration
```
# Random exploration
/rtp

# Return to starting point
/back
```

### 3. Cross-world Travel
```
# Teleport to the End
/tp world_the_end 0 80 0

# Return to previous location in main world
/backworld world
```

## 📊 Command Aliases

### Common Alias Setup
In `commands.yml`, you can set aliases:

```yaml
aliases:
  randomtp:
  - rtp
  home:
  - respawn
  return:
  - back
```

## 🔍 Troubleshooting

### Command Invalid
1. Check permissions: `/lp user <player> permission info`
2. Check world configuration: Confirm world name is correct
3. Check cooldown time: Use `/lp user <player> permission set teleportpack.bypass.cooldown true`

### Teleportation Failure
1. Check safe location: Confirm target location is safe
2. Check world boundaries: Confirm coordinates are within boundaries
3. Check permissions: Confirm sufficient permissions

### Cost Issues
1. Check economic plugin: Confirm Vault and Economy plugins are installed
2. Check balance: Use `/money` to view balance
3. Check cost configuration: Review cost settings in `config.yml`