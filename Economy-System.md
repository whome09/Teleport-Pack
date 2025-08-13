# 💰 Economy System

## 📋 System Overview

TeleportPack integrates a complete economic system that supports Vault API and can work with any Vault-compatible economy plugin.

### Supported Plugins
- **EssentialsX** - Most commonly used economy plugin
- **Vault** - Economic API interface
- **CMI** - Comprehensive plugin
- **Other Vault-compatible plugins**

## 🔧 Enabling the Economy System

### 1. Install Dependencies
```bash
# Required plugins
plugins/
├── Vault.jar
├── EssentialsX.jar (or other economy plugin)
└── TeleportPack.jar
```

### 2. Configuration Enablement
Enable the economic system in `config.yml`:
```yaml
costs:
  enabled: true    # Enable economic system
```

### 3. Verification Installation
Check console after startup:
```
[TeleportPack] Vault detected, economy features enabled!
```

## 💸 Cost Configuration

### Teleportation Cost Settings
```yaml
costs:
  enabled: true
  
  # Precise teleportation cost
  tp:
    money: 100
    conditions:
      - "%player_level% >= 10"
    condition-messages:
      - "&cYou need at least level 10 to use this command!"
  
  # Random teleportation cost
  rtp:
    money: 50
    conditions: []
    condition-messages: []
  
  # Return functionality cost
  back:
    money: 200
    conditions: []
    condition-messages: []
  
  # Respawn point teleportation cost
  respawn:
    money: 0
    conditions: []
    condition-messages: []
```

### Cross-world Additional Cost
```yaml
back:
  cross-world-extra-cost: 100  # Cross-world return additional cost
```

## 🎯 Economy System Features

### 1. Cost Deduction
- **Automatic Deduction** - Automatically deducted from player account during teleportation
- **Balance Check** - Check player balance before teleportation
- **Failure Handling** - Cancel teleportation when balance is insufficient

### 2. Condition System
- **Level Restrictions** - Conditions based on player level
- **Permission Restrictions** - Conditions based on permissions
- **Custom Conditions** - Using PlaceholderAPI variables

### 3. Bypass Mechanism
- **VIP Permissions** - Free teleportation for specific permission groups
- **Admin Permissions** - Free teleportation for administrators
- **Temporary Bypass** - Free teleportation during events

## 🏗️ Configuration Examples

### Basic Economic Configuration
```yaml
costs:
  enabled: true
  
  # Newbie-friendly configuration
  tp:
    money: 50
    conditions:
      - "%player_level% >= 5"
  
  rtp:
    money: 10
    conditions: []
  
  back:
    money: 25
    conditions: []
```

### VIP Economic Configuration
```yaml
costs:
  enabled: true
  
  # VIP free
  tp:
    money: 0
    conditions: []
  
  rtp:
    money: 0
    conditions: []
  
  back:
    money: 0
    conditions: []
```

### Hardcore Server Configuration
```yaml
costs:
  enabled: true
  
  # High cost configuration
  tp:
    money: 500
    conditions:
      - "%player_level% >= 20"
      - "%vault_eco_balance% >= 1000"
    condition-messages:
      - "&cYou need at least level 20!"
      - "&cYou need at least 1000 coins in your account!"
  
  rtp:
    money: 100
    conditions:
      - "%player_level% >= 10"
  
  back:
    money: 1000
    conditions: []
```

## 🔍 Condition System Details

### Supported Variables
Using PlaceholderAPI supported variables:

#### Player Attributes
```yaml
conditions:
  - "%player_level% >= 10"           # Level restriction
  - "%player_health% >= 15"          # Health restriction
  - "%player_food_level% >= 10"      # Hunger restriction
```

#### Economic Attributes
```yaml
conditions:
  - "%vault_eco_balance% >= 100"     # Balance restriction
  - "%vault_eco_balance_formatted% >= $1000"  # Formatted balance
```

#### Permission Checks
```yaml
conditions:
  - "%player_has_permission_teleportpack.vip% == yes"  # VIP permission check
```

### Condition Messages
```yaml
condition-messages:
  - "&cInsufficient level! Need at least level 10"
  - "&cInsufficient balance! Need at least 100 coins"
  - "&cVIP permission required!"
```

## 💡 Economic Balance Strategies

### 1. Newbie Protection
```yaml
costs:
  tp:
    money: 0
    conditions:
      - "%player_level% <= 5"
  
  rtp:
    money: 0
    conditions:
      - "%player_level% <= 3"
```

### 2. Level-based Pricing
```yaml
# Use PlaceholderAPI to calculate dynamic pricing
# Cost = base cost * (level / 10)
conditions:
  - "cost = 50 * (%player_level% / 10)"
```

### 3. Member Discounts
```yaml
# 50% discount for VIP
conditions:
  - "cost = %player_has_permission_teleportpack.vip% ? original_cost * 0.5 : original_cost"
```

## 🎮 Practical Application Cases

### Case 1: Survival Server Economy

#### Economic Model
- **Newbie Phase** (Levels 1-5): Free teleportation
- **Growth Phase** (Levels 6-15): Basic cost
- **Mature Phase** (Level 16+): Standard cost
- **VIP**: Permanent free

#### Configuration Implementation
```yaml
costs:
  enabled: true
  
  # Newbie free
  tp:
    money: 0
    conditions:
      - "%player_level% <= 5"
  
  # Basic cost
  tp_level_6_15:
    money: 50
    conditions:
      - "%player_level% >= 6"
      - "%player_level% <= 15"
  
  # Standard cost
  tp_level_16_plus:
    money: 100
    conditions:
      - "%player_level% >= 16"
```

### Case 2: Minigame Server

#### Arena Economy
- **Lobby**: Free teleportation
- **Arena**: Teleportation cost
- **Spectator Mode**: Free teleportation

#### Configuration Implementation
```yaml
# Lobby world configuration
worlds:
  lobby:
    costs:
      enabled: false  # Lobby free
  
  arena:
    costs:
      enabled: true
      tp:
        money: 200
      rtp:
        money: 100
```

### Case 3: RPG Server

#### Profession Economic System
- **Warrior**: Teleportation cost discount
- **Mage**: Free teleportation (magic consumption)
- **Merchant**: Economic teleportation discount

#### Configuration Implementation
```yaml
# Warrior profession
warrior:
  costs:
    tp:
      money: 75  # 25% discount
    conditions:
      - "%player_has_permission_rpg.warrior% == yes"

# Mage profession
mage:
  costs:
    tp:
      money: 0   # Free, but consumes magic
    conditions:
      - "%player_has_permission_rpg.mage% == yes"
      - "%rpg_mana% >= 10"
```

## 🔧 Economy System Management

### 1. Balance Inquiry
```bash
# View player balance
/money <playername>

# View economic statistics
/balancetop
```

### 2. Economic Management
```bash
# Give money
/money give <playername> 1000

# Deduct money
/money take <playername> 500

# Set balance
/money set <playername> 2000
```

### 3. Economic Monitoring
```yaml
# Enable economic logs
logging:
  economy: true
  transactions: true
```

## 📊 Economic Data Analysis

### 1. Teleportation Cost Statistics
```yaml
# Record teleportation data
statistics:
  enabled: true
  track:
    - tp_usage
    - rtp_usage
    - back_usage
    - total_cost
```

### 2. Economic Balance Check
```bash
# View teleportation cost statistics
/tp stats economy

# View player spending rankings
/tp top spenders
```

## 🛠️ Troubleshooting

### Common Issues

#### 1. Economy Plugin Not Detected
**Issue**: "Vault not found, economy features disabled"
**Solution**: 
- Install Vault plugin
- Install economy plugin (EssentialsX)
- Restart server

#### 2. Insufficient Balance but Teleportation Successful
**Issue**: Cost deduction failed
**Solution**:
- Check economy plugin configuration
- Confirm player has sufficient balance
- Check permission bypass settings

#### 3. Cost Display Error
**Issue**: Cost displays as 0
**Solution**:
- Check configuration file format
- Confirm economic system is enabled
- Check PlaceholderAPI variables

### Debug Commands
```bash
# Check economic system status
/tp debug economy

# Test cost deduction
/tp test cost tp 100

# View economic variables
/papi parse me %vault_eco_balance%
```

## 🎯 Economy System Optimization

### 1. Dynamic Pricing
```yaml
# Time-based dynamic pricing
pricing:
  peak_hours:
    multiplier: 1.5
    time: "18:00-22:00"
  
  off_peak:
    multiplier: 0.8
    time: "02:00-06:00"
```

### 2. Membership System
```yaml
# Membership level discounts
membership:
  bronze:
    discount: 0.9
  silver:
    discount: 0.7
  gold:
    discount: 0.5
  platinum:
    discount: 0.0  # Free
```

### 3. Event Discounts
```yaml
# Limited-time events
events:
  weekend_sale:
    discount: 0.5
    active: true
    duration: "2025-08-15 to 2025-08-17"
```

## 📈 Economy System Monitoring

### 1. Data Collection
```yaml
metrics:
  enabled: true
  collect:
    - daily_transactions
    - average_cost
    - player_spending
    - economic_impact
```

### 2. Report Generation
```bash
# Generate economic reports
/tp report economy weekly
/tp report economy monthly
```

### 3. Balance Adjustment
Adjust costs based on data analysis:
- Monitor teleportation frequency
- Analyze economic impact
- Adjust cost balance