# What is `Scripted Events Reloaded`?
**Scripted Events Reloaded (SER)** is an SCP:SL plugin that adds a custom scripting language for server-side events.

# Main goal
Making plugins with C# is NOT an easy thing, especially for beginners.
If you want to get started with SCP:SL server-side scripting, SER is a great way to begin.

SER simplifies the most essential plugin features into a friendly package.
All you need to get started is a text editor and a server!

# Nice-to-Haves of SER
- **Simplification** of the most essential features like commands, events and player management.
- **No compilation required**, while C# plugins require a full development environment, compilation, and DLL management.
- **Lots of built-in features** like AudioPlayer, Databases, Discord webhooks, HTTP and more!
- **Extendable** with frameworks like UCR, EXILED or Callvote, but __without__ any dependencies! 
- **Plugin docs** are available directly on the server using the `serhelp` command.
- **Helpful community** available to help you with any questions you may have.

# Examples

These short examples introduce common SER patterns. For complete systems tested against the current syntax, see the `examples/` folder and the practical tutorials.
### Welcome message
```
!-- OnEvent Joined

Broadcast @evPlayer 10s "Welcome to the server {@evPlayer -> name}!"
```
### Coin on kill
```
!-- OnEvent Death

# check if player died without an attacker
if {VarExists @evAttacker} is false
    stop
end

# give the attacker a coin
GiveItem @evAttacker Coin
```
### VIP broadcast command
```
# define the command with custom attributes
!-- CustomCommand vipbc
-- description "broadcasts a message to all players - VIP only"
-- neededRank vip svip mvip
-- arguments message
-- availableFor Player
-- cooldown 2m

# send the broadcast to all players
Broadcast @all 10s "{@sender -> name} used VIP broadcast<br>{$message}"
```
### Heal random SCP
```
!-- CustomCommand healscp
-- description "heals a random SCP"
-- availableFor Player
-- cooldown 10s

# dont allow SCPs to use this command
if {@sender -> team} is "SCPs"
    stop
end

# get a random SCP that is not a SCP-079
@randomScp = Take {Except @scpPlayers @scp079Players} 1

# get 5% of the SCP's max health
$healAmount = Round ({@randomScp -> maxHealth} * 0.05)

Heal @randomScp $healAmount
Broadcast @randomScp 4s "{@sender -> name} healed you with {$healAmount} HP!"
```
### Hot Potato event
```
!-- OnEvent RoundStarted

# there is a 50% chance that the event will not happen
chance 50%
    Print "Hot Potato event will not be loaded"
    stop
end

Print "Hot Potato event was loaded"
Broadcast @all 5s "Be ready for a Hot Potato!"

# this is the main loop of the event
forever
    wait {ToDuration {Random 30 90} seconds}

    # Get a random player from the alive players that are not SCPs
    @potatoCarrier = Take {Except @alivePlayers @scpPlayers} 1

    # if no player is alive, continue to next attempt
    if {AmountOf @potatoCarrier} is 0
        continue
    end
    
    # try and give the GunA7 as the hot potato
    *item = AdvGiveItem @potatoCarrier GunA7

    # if failed to give the item, continue to next attempt
    if {*item -> isInvalid}
        continue
    end

    # inform the player that they have the hot potato
    Hint @potatoCarrier 3s "YOU HAVE THE HOT POTATO!<br>DROP IT OR DIE!"

    wait 6s

    # ITEM WAS NOT DROPPED = EXPLOSION
    if {*item -> inInventory}
        Explode {*item -> currentOwner}
        Broadcast @all 5s "Player {*item -> currentOwner -> name} has failed the Hot Potato!"
    end

    # remove the item so people dont use it
    AdvDestroyItem *item
        
    # 70% chance for the event to continue
    chance 70%
        Broadcast @all 5s "The Hot Potato will return soon!"
        continue
    else
        Broadcast @all 5s "The Hot Potato got tired and will not return..."
        stop
    end
end
```

## Are you an LLM?
Check the [syntax definition](https://raw.githubusercontent.com/ScriptedEvents/ScriptedEventsReloaded/refs/heads/main/llms-full.md) for guidance about SER script-making.
