# ⚙️ Configuration Tutorial

## 📋 Configuration File Structure

TeleportPack uses `config.yml` as the main configuration file, containing the following main sections:

- `teleport` - General teleportation settings
- `random-teleport` - Random teleportation configuration
- `costs` - Economic system configuration
- `back` - Return functionality configuration
- `respawn` - Respawn point configuration
- `messages` - Message configuration

## 🎯 Teleport Settings (teleport)

### Basic Settings
```yaml
teleport:
  delay: 3                    # Teleport delay (seconds)
  allow-movement: false       # Allow movement during teleportation
  cooldown: 10               # Command cooldown (seconds)
```

### Title Messages
```yaml
title:
  enabled: true              # Enable title messages
  main: "&aTeleporting!"     # Main title
  sub: "&7Please wait {countdown} seconds..."  # Subtitle
  fadeIn: 10                 # Fade in time (ticks)
  stay: 40                   # Stay time (ticks)
  fadeOut: 10                # Fade out time (ticks)
```

### Particle Effects
```yaml
particles:
  enabled: true              # Enable particle effects
  type: PORTAL               # Particle type
  count: 50                  # Particle count
```

### Sound Settings
```yaml
sounds:
  enabled: true              # Enable sounds
  start: BLOCK_PORTAL_TRIGGER # Start sound
  complete: ENTITY_ENDERMAN_TELEPORT # Complete sound
```

## 🌍 Random Teleport Configuration (random-teleport)

### Target World
```yaml
random-teleport:
  target-world: world        # Default teleport world
```

### World-Specific Configuration
```yaml
worlds:
  world:
    enabled: true            # Enable random teleport for this world
    min-range: 100           # Minimum range
    max-range: 5000          # Maximum range
    
    # Fixed height settings
    fixed-height:
      enabled: false         # Use fixed height
      min-y: 60              # Minimum Y value
      max-y: 100             # Maximum Y value
    
    # Terrain checking
    terrain:
      allow-water: false     # Allow water
      allow-lava: false      # Allow lava
      allowed-blocks:        # Allowed blocks
        - GRASS_BLOCK
        - DIRT
        - STONE
        - SAND
      forbidden-blocks:      # Forbidden blocks
        - CACTUS
        - MAGMA_BLOCK
    
    # Excluded biomes
    excluded-biomes:
      - OCEAN
      - DEEP_OCEAN
```

### Safety Settings
```yaml
max-attempts: 20           # Maximum attempts
safe-check: true           # Enable safety check
```

## 💰 Economic System Configuration (costs)

### Enable Economy
```yaml
costs:
  enabled: true            # Enable economic system
```

### Teleportation Costs
```yaml
tp:
  money: 100               # Precise teleport cost
  conditions:              # Usage conditions
    - "%player_level% >= 10"
  condition-messages:      # Condition not met messages
    - "&cYou need at least level 10 to use this command!"

rtp:
  money: 50                # Random teleport cost
  conditions: []
  condition-messages: []

back:
  money: 200               # Return cost
  conditions: []
  condition-messages: []

respawn:
  money: 0                 # Respawn point teleport cost
  conditions: []
  condition-messages: []
```

## 🔙 Return Function Configuration (back)

```yaml
back:
  enabled: true            # Enable return functionality
  allow-in-same-world: true # Allow same-world return
  allow-cross-world: true   # Allow cross-world return
  expire-time: 600         # Location expiration time (seconds)
  clear-on-death: true     # Clear location on death
  cross-world-extra-cost: 100 # Cross-world extra cost
```

## 🏠 Respawn Point Configuration (respawn)

### World Respawn Point Settings
```yaml
respawn:
  enabled: true            # Enable respawn point system
  worlds:
    world:
      x: 0                 # X coordinate
      y: 80                # Y coordinate
      z: 0                 # Z coordinate
      yaw: 0               # Yaw angle
      pitch: 0             # Pitch angle
    world_nether:
      x: 0
      y: 70
      z: 0
      yaw: 90
      pitch: 0
```

## 🤖 Smart Fallback Configuration (fork-command)

```yaml
fork-command:
  enabled: true
  command-name: "smartback"    # Command name
  permission: "teleportpack.smartback" # Permission
  primary-cmd: "backworld world" # Primary command
  fallback-cmd: "rtp"          # Fallback command
  messages:
    executing-primary: "&aReturning to your previous location in world!"
    executing-fallback: "&cNo previous location found, teleporting randomly!"
```

## 💬 Message Configuration (messages)

### Message Prefix
```yaml
messages:
  prefix: "&6[TeleportPack] &r"     # Message prefix
```

### General Messages
```yaml
  teleporting: "&aTeleporting in &e{countdown} &aseconds..."
  teleport-success: "&aTeleport successful!"
  teleport-cancelled: "&cTeleport cancelled!"
  no-permission: "&cYou do not have permission!"
  invalid-world: "&cInvalid world name!"
  world-disabled: "&cRandom teleport is disabled in this world!"
  invalid-coordinates: "&cInvalid coordinates!"
  no-back-location: "&cNo previous location to return to!"
  back-location-expired: "&cYour previous location has expired!"
  cooldown-message: "&cPlease wait &e{time} &cseconds before using this command again!"
  random-teleport-fail: "&cCould not find a safe location to teleport!"
  not-enough-money: "&cYou do not have enough money! Required: &e${cost}"
  money-deducted: "&aDeducted &e${cost}"
  condition-not-met: "&cTeleport condition not met:"
  teleport-countdown: "&e{time} &aseconds left to teleport..."
  respawn-set: "&aRespawn point set for world: &e{world}"
  respawn-teleport: "&aYou have been respawned at the configured location!"
  reload-success: "&aTeleportPack config reloaded!"
  no-respawn-point: "&cNo respawn point set for this world!"
  respawn-cost: "&aTeleporting to respawn point - cost: &e${cost}"
```

## 🎨 Color Codes

Supports Minecraft color codes:
- `&0` - Black
- `&1` - Dark Blue
- `&2` - Dark Green
- `&3` - Dark Aqua
- `&4` - Dark Red
- `&5` - Dark Purple
- `&6` - Gold
- `&7` - Gray
- `&8` - Dark Gray
- `&9` - Blue
- `&a` - Green
- `&b` - Aqua
- `&c` - Red
- `&d` - Light Purple
- `&e` - Yellow
- `&f` - White

## 🔧 Advanced Configuration Examples

### Multi-world Configuration
```yaml
random-teleport:
  worlds:
    world:
      enabled: true
      min-range: 100
      max-range: 5000
    world_nether:
      enabled: true
      min-range: 50
      max-range: 1000
      terrain:
        allow-lava: true
        allowed-blocks:
          - NETHERRACK
          - SOUL_SAND
          - NETHER_BRICKS
        forbidden-blocks:
          - LAVA
    world_the_end:
      enabled: true
      min-range: 100
      max-range: 2000
      excluded-biomes:
        - THE_END_VOID
```

### VIP Permission Configuration
```yaml
costs:
  tp:
    money: 0                 # VIP free teleportation
    conditions: []
```

## 📝 Configuration Validation

After configuration is complete, use the command to validate:
```
/tpreload
```

Check the console for any error messages to ensure all configurations are loaded correctly.