# 📋 Example Configurations

## 🎯 Complete Configuration Examples

### Survival Server Configuration
```yaml
# Complete survival server configuration

# Teleportation settings
teleport:
  delay: 3
  allow-movement: false
  cooldown: 30
  title:
    enabled: true
    main: "&6[Teleport System]"
    sub: "&7Preparing teleport... {countdown}"
    fadeIn: 10
    stay: 40
    fadeOut: 10
    success-main: "&a✓"
    success-sub: "&7Teleport complete!"
  particles:
    enabled: true
    type: ENDER_SIGNAL
    count: 30
  sounds:
    enabled: true
    start: ENTITY_ENDERMAN_TELEPORT
    complete: ENTITY_PLAYER_LEVELUP

# Random teleport configuration
random-teleport:
  target-world: world
  worlds:
    world:
      enabled: true
      min-range: 500
      max-range: 10000
      fixed-height:
        enabled: false
      terrain:
        allow-water: false
        allow-lava: false
        allowed-blocks:
          - GRASS_BLOCK
          - DIRT
          - STONE
          - PODZOL
          - MYCELIUM
          - SAND
          - GRAVEL
        forbidden-blocks:
          - CACTUS
          - MAGMA_BLOCK
          - SOUL_SAND
          - LAVA
      excluded-biomes:
        - OCEAN
        - DEEP_OCEAN
        - FROZEN_OCEAN
        - RIVER
    world_nether:
      enabled: true
      min-range: 200
      max-range: 3000
      terrain:
        allow-lava: true
        allowed-blocks:
          - NETHERRACK
          - SOUL_SAND
          - NETHER_BRICKS
        forbidden-blocks:
          - LAVA
      excluded-biomes: []
    world_the_end:
      enabled: true
      min-range: 100
      max-range: 2000
      terrain:
        allowed-blocks:
          - END_STONE
        forbidden-blocks:
          - VOID_AIR
  max-attempts: 50
  safe-check: true

# Economic system
costs:
  enabled: true
  tp:
    money: 200
    conditions:
      - "%player_level% >= 5"
    condition-messages:
      - "&cYou need at least level 5 to use precise teleport!"
  rtp:
    money: 100
    conditions: []
  back:
    money: 150
    conditions: []
  respawn:
    money: 50
    conditions: []

# Return functionality
back:
  enabled: true
  allow-in-same-world: true
  allow-cross-world: true
  expire-time: 1800  # 30 minutes
  clear-on-death: true
  cross-world-extra-cost: 100

# Respawn system
respawn:
  enabled: true
  worlds:
    world:
      x: 0
      y: 70
      z: 0
      yaw: 0
      pitch: 0
    world_nether:
      x: 0
      y: 70
      z: 0
      yaw: 90
      pitch: 0
    world_the_end:
      x: 0
      y: 70
      z: 0
      yaw: 0
      pitch: 0

# Smart return
fork-command:
  enabled: true
  command-name: "back"
  permission: "teleportpack.back"
  primary-cmd: "backworld world"
  fallback-cmd: "rtp"
  messages:
    executing-primary: "&aReturning to previous location in world..."
    executing-fallback: "&cNo location found, random teleporting..."

# Message configuration
messages:
  prefix: "&6[Teleport System] &r"
  teleporting: "&7Preparing teleport... &e{countdown} &7seconds"
  teleport-success: "&aTeleport successful!"
  teleport-cancelled: "&cTeleport cancelled!"
  no-permission: "&cYou don't have permission to use this command!"
  invalid-world: "&cWorld doesn't exist!"
  world-disabled: "&cRandom teleport is disabled in this world!"
  invalid-coordinates: "&cCoordinate format error!"
  no-back-location: "&cNo location to return to!"
  back-location-expired: "&cReturn location has expired!"
  cooldown-message: "&cOn cooldown... &e{time} &cseconds until retry"
  random-teleport-fail: "&cCouldn't find safe location, please retry!"
  not-enough-money: "&cNot enough coins! Required: &e${cost}"
  money-deducted: "&aDeducted &e${cost} &acoins"
  condition-not-met: "&cCondition not met:"
  teleport-countdown: "&e{time} &7seconds..."
  respawn-set: "&aSet respawn point for &e{world}"
  respawn-teleport: "&aTeleported to respawn point!"
  reload-success: "&aConfiguration reloaded!"
  no-respawn-point: "&cNo respawn point set for this world!"
  respawn-cost: "&aTeleporting to respawn point, cost: &e${cost}"
```

### Minigame Server Configuration
```yaml
# Minigame server configuration

# Teleportation settings
teleport:
  delay: 0  # No delay, fast teleportation
  allow-movement: true
  cooldown: 0
  title:
    enabled: false  # Disable titles to avoid interference
  particles:
    enabled: false  # Disable particles for performance
  sounds:
    enabled: false  # Disable sounds

# Random teleport configuration
random-teleport:
  target-world: lobby
  worlds:
    lobby:
      enabled: true
      min-range: 50
      max-range: 500
    arena:
      enabled: false  # Disable random teleport in arena
    minigames:
      enabled: true
      min-range: 100
      max-range: 1000

# Economic system
costs:
  enabled: false  # Disable economic system for minigame server

# Return functionality
back:
  enabled: true
  allow-in-same-world: true
  allow-cross-world: false  # Don't allow cross-world return
  expire-time: 300  # 5 minutes
  clear-on-death: true

# Respawn system
respawn:
  enabled: true
  worlds:
    lobby:
      x: 0
      y: 70
      z: 0
    arena:
      x: 100
      y: 70
      z: 100
    minigames:
      x: 200
      y: 70
      z: 200
```

### VIP Server Configuration
```yaml
# VIP server configuration

# Teleportation settings
teleport:
  delay: 1  # VIP fast teleportation
  allow-movement: true
  cooldown: 5  # Short cooldown time
  title:
    enabled: true
    main: "&d&l[VIP Teleport]"
    sub: "&fVIP privilege teleport... {countdown}"
  particles:
    enabled: true
    type: HEART
    count: 100  # More particle effects
  sounds:
    enabled: true
    start: ENTITY_FIREWORK_ROCKET_LAUNCH
    complete: ENTITY_FIREWORK_ROCKET_TWINKLE

# Random teleport configuration
random-teleport:
  target-world: world
  worlds:
    world:
      enabled: true
      min-range: 1000  # VIP larger range
      max-range: 50000
      terrain:
        allow-water: true  # VIP can teleport to water
        allow-lava: false
        allowed-blocks:
          - "*"  # Allow all blocks
        forbidden-blocks: []
      excluded-biomes: []  # VIP no biome restrictions

# Economic system
costs:
  enabled: true
  tp:
    money: 0  # VIP free precise teleportation
    conditions: []
  rtp:
    money: 0  # VIP free random teleportation
    conditions: []
  back:
    money: 0  # VIP free return
    conditions: []
  respawn:
    money: 0  # VIP free respawn teleportation
    conditions: []

# Return functionality
back:
  enabled: true
  allow-in-same-world: true
  allow-cross-world: true
  expire-time: 3600  # VIP 1 hour expiration time
  clear-on-death: false  # VIP don't clear death records
  cross-world-extra-cost: 0  # VIP free cross-world

# Respawn system
respawn:
  enabled: true
  worlds:
    world:
      x: 0
      y: 100
      z: 0
      yaw: 0
      pitch: 0
    world_nether:
      x: 0
      y: 100
      z: 0
      yaw: 0
      pitch: 0
    world_the_end:
      x: 0
      y: 100
      z: 0
      yaw: 0
      pitch: 0
```

## 🏗️ Permission Configuration Examples

### LuckPerms Permission Configuration
```yaml
# Default player group
groups:
  default:
    permissions:
      - teleportpack.rtp
      - teleportpack.back.use
      - teleportpack.respawn
    permissions-false:
      - teleportpack.bypass.cost
      - teleportpack.bypass.cooldown

# VIP group
groups:
  vip:
    inheritance:
      - default
    permissions:
      - teleportpack.tp
      - teleportpack.back.crossworld
      - teleportpack.bypass.cost
      - teleportpack.bypass.cooldown

# Admin group
groups:
  admin:
    permissions:
      - teleportpack.*
```

### Command Setup Examples
```bash
# Create permission groups
/lp creategroup default
/lp creategroup vip
/lp creategroup admin

# Set permissions
/lp group default permission set teleportpack.rtp true
/lp group default permission set teleportpack.back.use true
/lp group default permission set teleportpack.respawn true

/lp group vip parent add default
/lp group vip permission set teleportpack.tp true
/lp group vip permission set teleportpack.back.crossworld true
/lp group vip permission set teleportpack.bypass.cost true
/lp group vip permission set teleportpack.bypass.cooldown true

/lp group admin permission set teleportpack.* true

# Set default group
/lp group default parent add default
```

## 🎮 Usage Scenario Configurations

### Newbie Server
```yaml
# Newbie-friendly configuration
random-teleport:
  worlds:
    world:
      min-range: 100
      max-range: 1000  # Smaller range to avoid getting lost
      max-attempts: 30  # More attempts to ensure success

costs:
  enabled: true
  tp:
    money: 0  # Newbie free precise teleportation
  rtp:
    money: 10  # Low-cost random teleportation
  back:
    money: 5   # Low-cost return
```

### Hardcore Survival Server
```yaml
# Hardcore configuration
random-teleport:
  worlds:
    world:
      min-range: 1000
      max-range: 50000  # Large range for challenge
      max-attempts: 10  # Fewer attempts for risk
      safe-check: false  # Disable safety checks for risk

costs:
  enabled: true
  tp:
    money: 500  # High cost
    conditions:
      - "%player_level% >= 15"
  rtp:
    money: 200  # High cost
  back:
    money: 1000  # High cost
```

### Creative Server
```yaml
# Creative mode configuration
costs:
  enabled: false  # Completely free

teleport:
  delay: 0  # No delay
  cooldown: 0  # No cooldown
  allow-movement: true
```

## 📊 Performance Optimization Configurations

### High Concurrency Server
```yaml
# Performance optimization configuration
teleport:
  delay: 1  # Reduced delay
  particles:
    enabled: true
    count: 10  # Reduced particle count
  sounds:
    enabled: true

random-teleport:
  max-attempts: 15  # Reduced attempts
  safe-check: true  # Keep safety checks
```

### Low-end Server
```yaml
# Low-end server configuration
teleport:
  delay: 0
  particles:
    enabled: false  # Disable particle effects
  sounds:
    enabled: false  # Disable sounds

random-teleport:
  max-attempts: 10
  safe-check: false  # Disable safety checks (use at your own risk)
```