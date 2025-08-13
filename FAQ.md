# ❓ Frequently Asked Questions

## 🚀 Installation Issues

### Q1: Plugin Fails to Load
**Issue Description**: Plugin fails to load during server startup

**Possible Causes**:
- Java version incompatibility
- Server version not supported
- Missing dependency plugins

**Solutions**:
```bash
# Check Java version
java -version  # Requires Java 8+

# Check server version
version  # Requires 1.13+

# Check dependencies
plugins folder should contain:
├── Vault.jar (optional)
├── EssentialsX.jar (optional)
└── TeleportPack.jar
```

### Q2: Commands Invalid or Non-existent
**Issue Description**: Inputting commands shows "unknown command"

**Solutions**:
```bash
# Check if plugin is enabled
/plugins list | grep TeleportPack

# Check console errors
Look for error messages in console

# Reload plugin
/tpreload
```

## 🎯 Teleportation Issues

### Q3: Random Teleport Fails
**Issue Description**: `/rtp` command shows "Could not find safe location"

**Possible Causes**:
- World configuration error
- Teleportation range settings unreasonable
- Safety checks too strict

**Solutions**:
```yaml
# Check world configuration
random-teleport:
  worlds:
    world:
      enabled: true
      min-range: 100    # Not too small
      max-range: 5000   # Not too large
      max-attempts: 20  # Increase attempts
      safe-check: true  # Can temporarily disable for testing
```

### Q4: Cross-world Teleportation Fails
**Issue Description**: Cannot teleport to other worlds

**Solutions**:
```bash
# Check if world exists
/worlds list

# Check world names
Ensure world names in configuration match actual names

# Check permissions
/lp user <player> permission check teleportpack.back.crossworld
```

### Q5: Teleportation Location Unsafe
**Issue Description**: Teleporting to dangerous locations (lava, high altitude, etc.)

**Solutions**:
```yaml
# Adjust safety checks
terrain:
  allow-water: false
  allow-lava: false
  allowed-blocks:
    - GRASS_BLOCK
    - DIRT
    - STONE
    - SAND
  forbidden-blocks:
    - CACTUS
    - MAGMA_BLOCK
    - LAVA
```

## 💰 Economic System Issues

### Q6: Economic System Not Working
**Issue Description**: Teleportation does not deduct costs

**Solutions**:
```bash
# Check Vault installation
/plugins list | grep Vault

# Check economy plugin
/plugins list | grep Essentials

# Check configuration
Ensure in config.yml:
costs:
  enabled: true

# Check permission bypass
/lp user <player> permission check teleportpack.bypass.cost
```

### Q7: Cost Display Error
**Issue Description**: Cost displays as 0 or incorrect amount

**Solutions**:
```yaml
# Check PlaceholderAPI
Ensure PlaceholderAPI is installed

# Check variables
/papi parse me %vault_eco_balance%

# Check configuration format
Ensure YAML format is correct with no indentation errors
```

## 🔐 Permission Issues

### Q8: Permissions Not Taking Effect
**Issue Description**: Players cannot use commands

**Solutions**:
```bash
# Check permission plugin
/plugins list | grep LuckPerms

# Check permission settings
/lp user <player> permission info

# Check permission inheritance
/lp user <player> parent info

# Reload permissions
/lp sync
```

### Q9: Bypass Permissions Invalid
**Issue Description**: VIP players still charged fees

**Solutions**:
```bash
# Check bypass permissions
/lp user <player> permission check teleportpack.bypass.cost

# Check permission conflicts
/lp user <player> permission checkinherits teleportpack.bypass.cost

# Check permission group settings
/lp group <groupname> permission info
```

## 🌍 World Configuration Issues

### Q10: World Not Found
**Issue Description**: "Invalid world name"

**Solutions**:
```bash
# View all worlds
/worlds list

# Check world name case sensitivity
World names are case-sensitive

# Check if world is loaded
/worlds info <worldname>
```

### Q11: Respawn Point Setting Invalid
**Issue Description**: `/setrespawn` set respawn points not taking effect

**Solutions**:
```bash
# Check permissions
Ensure teleportpack.admin permission

# Check world configuration
respawn:
  worlds:
    world:
      x: 0
      y: 80
      z: 0

# Use force update
/setrespawn world 100 64 200 --force
```

## 🔄 Cooldown Time Issues

### Q12: Cooldown Time Not Taking Effect
**Issue Description**: Players can use commands without restriction

**Solutions**:
```yaml
# Check cooldown settings
teleport:
  cooldown: 10  # Ensure greater than 0

# Check bypass permissions
/lp user <player> permission check teleportpack.bypass.cooldown

# Check data file
plugins/TeleportPack/data.yml for cooldown data
```

### Q13: Cooldown Time Display Error
**Issue Description**: Cooldown time display abnormal

**Solutions**:
```bash
# Reset player cooldown data
/tpreload  # Reload configuration to clear cooldown

# Manually clear data
Delete player cooldown records in data.yml
```

## 🎨 Effects Issues

### Q14: Particle Effects Not Displaying
**Issue Description**: No particle effects during teleportation

**Solutions**:
```yaml
# Check particle settings
particles:
  enabled: true
  type: PORTAL
  count: 50

# Check client settings
Ensure client particle effects are enabled

# Check server performance
/spark healthreport
```

### Q15: Sounds Not Playing
**Issue Description**: No sounds during teleportation

**Solutions**:
```yaml
# Check sound settings
sounds:
  enabled: true
  start: BLOCK_PORTAL_TRIGGER
  complete: ENTITY_ENDERMAN_TELEPORT

# Check sound names
Ensure sound names are correct (version 1.20.1)

# Check client volume
Ensure client volume settings are correct
```

## 📊 Performance Issues

### Q16: Server Lag
**Issue Description**: Server lags when using teleportation commands

**Solutions**:
```yaml
# Optimize random teleport settings
random-teleport:
  max-attempts: 10  # Reduce attempts
  safe-check: false  # Disable safety checks (higher risk)

# Optimize particle effects
particles:
  count: 20  # Reduce particle count
```

### Q17: Memory Leaks
**Issue Description**: High memory usage after long operation

**Solutions**:
```bash
# Regular data cleanup
/tpreload  # Reload configuration to clear cache

# Check data file size
ls -la plugins/TeleportPack/data.yml

# Set data cleanup
Set reasonable expire-time in config.yml
```

## 🔍 Debugging Tips

### 18. Enable Debug Mode
```yaml
# Add to config.yml
debug: true

# View detailed logs
Check console output for debug information
```

### 19. Test Commands
```bash
# Test random teleport
/tp debug rtp

# Test economic system
/tp debug economy

# Test permission system
/tp debug permissions
```

### 20. Log Analysis
```bash
# View error logs
tail -f logs/latest.log | grep TeleportPack

# View teleport records
grep "TeleportPack" logs/latest.log
```

## 🛠️ Data Repair

### 21. Configuration File Corruption
**Issue Description**: Configuration file format error

**Solutions**:
```bash
# Backup configuration files
cp config.yml config.yml.backup

# Regenerate default configuration
Delete config.yml and restart server

# Manually fix YAML format
Use YAML validation tools to check format
```

### 22. Data File Corruption
**Issue Description**: data.yml file corruption

**Solutions**:
```bash
# Backup data files
cp data.yml data.yml.backup

# Regenerate data file
Delete data.yml and restart server

# Manually repair data
Use text editor to fix format
```

## 📋 Common Error Codes

### Error Code Reference

| Error Message | Cause | Solution |
|---|---|---|
| "Invalid world" | World name error | Check world name spelling |
| "No safe location" | Cannot find safe location | Expand teleportation range |
| "Not enough money" | Insufficient balance | Recharge or adjust cost |
| "No permission" | Insufficient permissions | Check permission settings |
| "Cooldown active" | In cooldown | Wait or use bypass permission |
| "Config error" | Configuration format error | Check YAML format |

## 🆘 Getting Help

### 1. Official Support
- **GitHub Issues**: Submit detailed issue reports
- **Discord**: Join official Discord for support
- **Wiki**: View complete documentation

### 2. Community Support
- **SpigotMC**: Post on SpigotMC forums
- **Minecraft Forums**: Chinese community support
- **QQ Groups**: Join relevant technical groups

### 3. Self-help Tools
```bash
# Generate debug report
/tp report debug

# Check system status
/tp status

# View version information
/version TeleportPack
```

## 📞 Contact Support

### Provide Information
When seeking help, please provide:
1. **Server Version**: `/version`
2. **Plugin Version**: `/version TeleportPack`
3. **Error Logs**: Relevant console output
4. **Configuration Files**: Relevant configuration snippets
5. **Reproduction Steps**: How to reproduce the issue

### Issue Report Template
```markdown
## Issue Description
Briefly describe the issue encountered

## Environment Information
- Server Version: [version]
- Plugin Version: [version]
- Java Version: [version]
- Operating System: [system]

## Configuration Files
```yaml
[relevant configuration]
```

## Error Logs
```
[error message]
```

## Reproduction Steps
1. [step1]
2. [step2]
3. [step3]
```