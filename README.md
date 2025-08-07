# TeleportPack Plugin Wiki

TeleportPack is a comprehensive teleportation plugin for Minecraft servers running on Bukkit/Spigot/Paper. It offers a wide range of features including multi-world teleportation, random teleportation, economy integration, PlaceholderAPI conditions, customizable effects, and world-specific respawn points.

------

## Features

- **Multi-World Teleportation** - Seamlessly teleport between different worlds.
- **Random Teleportation** - Configurable range and terrain restrictions for random teleports.
- **Back/Return System** - Return to your previous location, whether in the same world or a different one.
- **Economy Support** - Set costs for teleportation (requires the Vault plugin).
- **PlaceholderAPI Conditions** - Define custom conditions for teleportation.
- **Visual Effects** - Particle effects, sounds, and title displays during teleportation.
- **Custom Respawn Points** - Set default respawn locations for each world.
- **Cooldown System** - Prevent excessive teleportation with cooldowns.
- **Movement Detection** - Automatically cancel teleportation if the player moves during the countdown.
- **Highly Configurable** - Customize all features in detail via the configuration file.

------

## Installation Guide

1. **Download** the latest version of TeleportPack.jar.
2. Place the jar file into your server’s plugins folder.
3. Install dependency plugins (optional but recommended):
   - [Vault](https://www.spigotmc.org/resources/vault.34315/) - For economy functionality.
   - [PlaceholderAPI](https://www.spigotmc.org/resources/placeholderapi.6245/) - For advanced condition support.
4. **Restart** your server.
5. Edit the plugins/TeleportPack/config.yml file to configure the plugin as needed.

------

## Commands

| Command     | Description                                    | Usage                                         | Permission                   |
| :---------- | :--------------------------------------------- | :-------------------------------------------- | :--------------------------- |
| /tp         | Teleport to a specific world and coordinates   | /tp <world> <x> <y> <z>                       | teleportpack.tp              |
| /rtp        | Random teleport                                | /rtp [world]                                  | teleportpack.rtp             |
| /back       | Return to the previous location (same world)   | /back                                         | teleportpack.back.use        |
| /backworld  | Return to a previous location in another world | /backworld <world>                            | teleportpack.back.crossworld |
| /setrespawn | Set the respawn point for a world              | /setrespawn <world> [x] [y] [z] [yaw] [pitch] | teleportpack.admin           |
| /tpreload   | Reload the TeleportPack configuration          | /tpreload                                     | teleportpack.admin           |

------

## Permissions

| Permission Node              | Description                                    | Default |
| :--------------------------- | :--------------------------------------------- | :------ |
| teleportpack.*               | Access to all TeleportPack permissions         | op      |
| teleportpack.tp              | Use the /tp command                            | true    |
| teleportpack.rtp             | Use the /rtp command                           | true    |
| teleportpack.back.use        | Use the /back command                          | true    |
| teleportpack.back.crossworld | Use the /backworld command                     | true    |
| teleportpack.respawn         | Use custom respawn points                      | true    |
| teleportpack.admin           | Access admin commands (/setrespawn, /tpreload) | op      |
| teleportpack.bypass.cost     | Bypass teleportation costs                     | false   |
| teleportpack.bypass.cooldown | Bypass teleportation cooldowns                 | false   |

------

## Configuration Guide

The main configuration file is located at plugins/TeleportPack/config.yml. All messages and settings are fully customizable.

### Teleport Settings

yaml

```
teleport:
  delay: 3                    # Teleport delay in seconds
  allow-movement: false       # Allow movement during countdown
  cooldown: 10                # Cooldown between teleports (seconds)
  title:
    enabled: true             # Enable title display during teleport
    main: "&aTeleporting!"    # Main title text
    sub: "&7Please wait {countdown} seconds..." # Subtitle text, {countdown} is replaced with seconds
    fadeIn: 10                # Fade-in time (ticks, 1 second = 20 ticks)
    stay: 40                  # Display duration (ticks)
    fadeOut: 10               # Fade-out time (ticks)
  particles:
    enabled: true             # Enable particle effects
    type: PORTAL              # Particle type (e.g., PORTAL, END_ROD, FLAME)
    count: 50                 # Number of particles
  sounds:
    enabled: true             # Enable sound effects
    start: BLOCK_PORTAL_TRIGGER # Sound played when teleport starts
    complete: ENTITY_ENDERMAN_TELEPORT # Sound played when teleport completes
```

### Random Teleport

Random teleport settings can be configured per world:

yaml

```
random-teleport:
  worlds:
    world:                    # World name
      enabled: true           # Enable random teleport in this world
      min-range: 100          # Minimum distance from spawn
      max-range: 5000         # Maximum distance from spawn
      fixed-height:
        enabled: false        # Use a fixed height instead of finding the highest block
        min-y: 60             # Minimum Y coordinate
        max-y: 100            # Maximum Y coordinate
      terrain:
        allow-water: false    # Allow teleporting onto water
        allow-lava: false     # Allow teleporting onto lava
        allowed-blocks:       # Only allow teleporting onto these blocks (empty = all allowed)
          - GRASS_BLOCK
          - DIRT
          - STONE
          - SAND
        forbidden-blocks:     # Never allow teleporting onto these blocks
          - CACTUS
          - MAGMA_BLOCK
      excluded-biomes:        # Biomes where teleportation is disabled
        - OCEAN
        - DEEP_OCEAN
  max-attempts: 20            # Maximum attempts to find a safe location
  safe-check: true            # Enable safe location checking
```

### Economy and Conditions

Set costs and conditions for each teleport type:

yaml

```
costs:
  enabled: true               # Enable economy system (requires Vault)
  tp:
    money: 100                # Cost for /tp command
    conditions:               # PlaceholderAPI conditions
      - "%player_level% >= 10"
    condition-messages:       # Messages shown when conditions aren’t met
      - "&cYou need at least level 10 to use this command!"
  rtp:
    money: 50                 # Cost for /rtp command
    conditions: []
    condition-messages: []
  back:
    money: 200                # Cost for /back command
    conditions: []
    condition-messages: []
```

### Back/Return Settings

yaml

```
back:
  enabled: true               # Enable the /back command
  allow-in-same-world: true   # Allow returning to the previous location in the same world
  allow-cross-world: true     # Allow returning to a previous location in another world
  expire-time: 600            # Time before the back location expires (seconds)
  clear-on-death: true        # Clear the back location on player death
  cross-world-extra-cost: 100 # Additional cost for cross-world returns
```

### Respawn Settings

yaml

```
respawn:
  enabled: true               # Enable custom respawn points
  worlds:                     # Define respawn points per world
    world:
      x: 0
      y: 80
      z: 0
      yaw: 0
      pitch: 0
    world_nether:             # Example: Respawn point for the Nether
      x: 0
      y: 70
      z: 0
      yaw: 0
      pitch: 0
```

**Note**: Coordinates can be set in-game using the /setrespawn command.

### Messages

All messages are customizable in the messages section and support & color codes:

yaml

```
messages:
  prefix: "&6[TeleportPack] &r"
  teleporting: "&aTeleporting... &e{countdown} &aseconds."
  teleport-success: "&aTeleport successful!"
  teleport-cancelled: "&cTeleport cancelled!"
  no-permission: "&cYou do not have permission!"
  # Additional messages can be found in config.yml
```

------

## PlaceholderAPI Support

TeleportPack integrates with PlaceholderAPI for advanced condition checks. Use any placeholder in the conditions section.

**Examples:**

- %player_level% >= 10 - Requires player level 10 or higher.
- %player_health% > 5 - Requires health above 5.
- %player_world% == world - Restricts usage to the world world.
- %vault_eco_balance% >= 1000 - Requires a minimum balance of 1000.

**Supported Operators:** >, <, >=, <=, ==

------

## FAQ

**Q: Why isn’t the economy system working?**
 A: Ensure Vault and an economy plugin (e.g., EssentialsX or CMI) are installed and loaded before TeleportPack.

**Q: Can I disable the title during teleportation?**
 A: Yes, set enabled to false in the teleport.title section.

**Q: Why do players teleport to unsafe locations?**
 A: Enable random-teleport.safe-check: true and configure the random-teleport.worlds.<world>.terrain section to define allowed or forbidden blocks.

**Q: How do I add more worlds for random teleportation?**
 A: Duplicate an existing world entry in random-teleport.worlds, update the world name, and adjust the settings as needed.

**Q: Why doesn’t teleportation cancel when players move during the countdown?**
 A: Verify that teleport.allow-movement is set to false. High server latency may cause detection delays.

------

## Troubleshooting

### "No economy plugin found"

- Install Vault and an economy plugin.
- Ensure they load before TeleportPack (check the plugin load order).

### "Cannot find a safe location"

- Increase random-teleport.max-attempts.
- Review allowed-blocks and forbidden-blocks settings for reasonableness.
- Ensure the world has sufficient safe teleportation areas.

### PlaceholderAPI conditions not working

- Confirm PlaceholderAPI is installed.
- Use /papi list to verify the placeholder exists.
- Check the condition syntax for errors.

------

## Support

For bug reports, feature requests, or assistance:

- Submit an issue on GitHub.
- Contact the plugin author.
- Regularly check for updates to access new features and fixes.

**Version:** 1.0.3-Beta
 **API:** Bukkit/Spigot/Paper 1.13+
