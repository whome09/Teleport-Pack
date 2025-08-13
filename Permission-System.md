# 🔐 Permission System

## 📋 Permission Overview

TeleportPack provides a complete permission management system with fine-grained permission control.

### Permission Node Structure
```
teleportpack.*                          # All permissions
├── teleportpack.tp                    # Precise teleportation
├── teleportpack.rtp                   # Random teleportation
├── teleportpack.back.*                # Return functionality
├── teleportpack.respawn               # Respawn point teleportation
├── teleportpack.admin                 # Admin permissions
├── teleportpack.bypass.*              # Bypass permissions
└── teleportpack.smartback             # Smart return
```

## 🎯 Player Permissions

### Basic Teleportation Permissions

| Permission Node | Description | Default |
|---|---|---|
| `teleportpack.tp` | Use `/tp` command | `true` |
| `teleportpack.rtp` | Use `/rtp` command | `true` |
| `teleportpack.back.use` | Use `/back` command | `true` |
| `teleportpack.back.crossworld` | Use `/backworld` command | `true` |
| `teleportpack.respawn` | Use `/respawn` command | `true` |
| `teleportpack.smartback` | Use `/smartback` command | `true` |

### Bypass Permissions

| Permission Node | Description | Default |
|---|---|---|
| `teleportpack.bypass.cost` | Bypass teleportation costs | `false` |
| `teleportpack.bypass.cooldown` | Bypass cooldown time | `false` |

### Admin Permissions

| Permission Node | Description | Default |
|---|---|---|
| `teleportpack.admin` | All admin commands | `op` |

## 🏗️ Permission Group Configuration Examples

### Using LuckPerms Configuration

#### 1. Default Player Group
```bash
# Create default group
/lp creategroup default

# Basic teleportation permissions
/lp group default permission set teleportpack.rtp true
/lp group default permission set teleportpack.back.use true
/lp group default permission set teleportpack.respawn true
/lp group default permission set teleportpack.smartback true

# Restrictions: Cannot bypass costs and cooldowns
/lp group default permission set teleportpack.bypass.cost false
/lp group default permission set teleportpack.bypass.cooldown false
```

#### 2. VIP Player Group
```bash
# Create VIP group
/lp creategroup vip

# Inherit default group permissions
/lp group vip parent add default

# Additional permissions
/lp group vip permission set teleportpack.tp true
/lp group vip permission set teleportpack.back.crossworld true

# VIP privileges: Bypass costs
/lp group vip permission set teleportpack.bypass.cost true
```

#### 3. Admin Group
```bash
# Create admin group
/lp creategroup admin

# All permissions
/lp group admin permission set teleportpack.* true
```

### Permission Inheritance Structure

```
admin (teleportpack.*)
├── vip (partial permissions)
│   ├── default (basic permissions)
│   └── player
└── player
```

## 🎮 Practical Configuration Cases

### Case 1: Survival Server

#### Permission Group Setup
```bash
# Newbie group
/lp creategroup newbie
/lp group newbie permission set teleportpack.rtp true
/lp group newbie permission set teleportpack.respawn true

# Member group
/lp creategroup member
/lp group member parent add newbie
/lp group member permission set teleportpack.back.use true
/lp group member permission set teleportpack.smartback true

# VIP group
/lp creategroup vip
/lp group vip parent add member
/lp group vip permission set teleportpack.tp true
/lp group vip permission set teleportpack.back.crossworld true
/lp group vip permission set teleportpack.bypass.cooldown true

# Admin group
/lp creategroup moderator
/lp group moderator permission set teleportpack.admin true
```

#### Permission Assignment
```bash
# Set default group
/lp group default parent add newbie

# Set VIP group permissions
/lp group vip permission set teleportpack.bypass.cost true
```

### Case 2: Minigame Server

#### Arena Permissions
```bash
# Arena group
/lp creategroup arena
/lp group arena permission set teleportpack.rtp false
/lp group arena permission set teleportpack.tp false
/lp group arena permission set teleportpack.back false
/lp group arena permission set teleportpack.respawn true
```

#### Lobby Permissions
```bash
# Lobby group
/lp creategroup lobby
/lp group lobby permission set teleportpack.rtp true
/lp group lobby permission set teleportpack.tp true
/lp group lobby permission set teleportpack.back true
/lp group lobby permission set teleportpack.respawn true
```

## 🔍 Permission Checking

### Check Player Permissions
```bash
# View all player permissions
/lp user <playername> permission info

# Check specific permission
/lp user <playername> permission check teleportpack.rtp

# View permission inheritance
/lp user <playername> permission checkinherits teleportpack.rtp
```

### Debug Permission Issues

#### 1. Permission Test Commands
```bash
# Test permissions
/lp user <playername> permission check teleportpack.rtp

# View permission tree
/lp tree teleportpack
```

#### 2. Permission Validation
```bash
# Validate permission settings
/lp user <playername> permission info
/lp user <playername> parent info
```

## 🛡️ Security Permission Configuration

### Prevent Abuse

#### 1. Limit Frequent Use
```bash
# Set cooldown bypass permission only for admins
/lp group admin permission set teleportpack.bypass.cooldown true
/lp group default permission set teleportpack.bypass.cooldown false
```

#### 2. Economic System Protection
```bash
# Only VIP can bypass costs
/lp group vip permission set teleportpack.bypass.cost true
/lp group default permission set teleportpack.bypass.cost false
```

### World-Specific Permissions

#### 1. World Permission Restrictions
```bash
# Disable teleportation in specific worlds
/lp group default permission set teleportpack.rtp false world=world_nether
/lp group default permission set teleportpack.tp false world=world_nether
```

#### 2. Region Permission Control
```yaml
# Use WorldGuard region permissions
regions:
  spawn:
    permissions:
      teleportpack.rtp: false
      teleportpack.tp: false
```

## 📊 Permission Templates

### Complete Permission Templates

#### 1. Default Player (default.yml)
```yaml
groups:
  default:
    permissions:
      - teleportpack.rtp
      - teleportpack.respawn
      - teleportpack.smartback
    permissions-false:
      - teleportpack.bypass.cost
      - teleportpack.bypass.cooldown
```

#### 2. VIP Player (vip.yml)
```yaml
groups:
  vip:
    inheritance:
      - default
    permissions:
      - teleportpack.tp
      - teleportpack.back.use
      - teleportpack.back.crossworld
      - teleportpack.bypass.cooldown
      - teleportpack.bypass.cost
```

#### 3. Admin (admin.yml)
```yaml
groups:
  admin:
    permissions:
      - teleportpack.*
```

## 🎯 Permission Best Practices

### 1. Layered Permission Design
```
Basic Player → Advanced Player → VIP → Admin
```

### 2. Principle of Least Privilege
- Only grant necessary permissions
- Avoid over-authorization
- Regularly review permission settings

### 3. Permission Documentation
```markdown
## Permission Documentation

### Player Permissions
- teleportpack.rtp: Random teleportation
- teleportpack.back.use: Return functionality

### VIP Permissions
- teleportpack.tp: Precise teleportation
- teleportpack.bypass.cost: Free teleportation

### Admin Permissions
- teleportpack.admin: All admin functions
```

## 🔧 Permission Troubleshooting

### Common Issues

#### 1. Permissions Not Taking Effect
```bash
# Check permission inheritance
/lp user <player> parent info

# Check permission conflicts
/lp user <player> permission info
```

#### 2. Bypass Permissions Invalid
```bash
# Check bypass permissions
/lp user <player> permission check teleportpack.bypass.cost

# Check permission source
/lp user <player> permission checkinherits teleportpack.bypass.cost
```

#### 3. World-Specific Permissions
```bash
# Check world permissions
/lp user <player> permission info world=world_nether
```

### Debugging Tools

#### 1. Permission Testing
```bash
# Create test user
/lp user testuser permission set teleportpack.rtp true

# Test permissions
/lp user testuser permission check teleportpack.rtp
```

#### 2. Permission Logs
```yaml
# Enable debugging in LuckPerms config
verbose: true
```

## 📈 Permission Optimization Suggestions

### 1. Permission Grouping
- Group permissions by function
- Use permission inheritance
- Avoid duplicate settings

### 2. Dynamic Permissions
- Adjust permissions based on player level
- Unlock permissions based on game progress
- Temporary permission management

### 3. Permission Monitoring
- Regularly review permission usage
- Monitor permission abuse
- Collect player feedback