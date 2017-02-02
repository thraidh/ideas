# Overview

This is the idea for a game. Some might call it an MMORPG, and I admit, that WOW
actually is an inspiration (mostly because it is the only MMORPG I actually
played).
But as I played I noticed two things: most of the time I actually played alone,
doing quests, but had few contacts to other players. Most of the time I didn't
even see them or when I did they annoyed me, because they made my questing
harder because they had the same objectives as I had.
I did chat with some friends and occasionally we quested together.
This probably describes most peoples experiences in that part of the game.
The other part is played in instances, where you cannot meet other people
except those who entered the instance with you. This part of the game takes up
almost all of the end-game.
So actually you do not really play an MMORPG, or when you do, you actually
rather wish you wouldn't.
This is all the perspective of a non-PvP player. If you are in PvP, you might
want to meet other players in the wild to kill them, but most of the time
you'll spend your time in battlefields or arena matches.

Therefore I propose an MORPG, e.g. limit the actual game completely to instances
with a common lobby, where you cannot actually do anything, except communicate,
share, sell, buy and gather people to play the next instance.

In contrast to WOW there are instances for every number of players, including
those for a single player. Also in contrast to WOW, instances also include
questing.

Oh, and there is the minor thing of procedural generation, which is used for
landscapes, buildings and quests. Yes, it will be hard to get it into a state
where procedural quests will be interesting.

Actually this whole project is just an excuse to work on cool procedurally
generated quests.

# Features

## Lobby, between games

- gather all things and stats from survived instances
- can be reallocated for each entry into a new instance, but only to a max
    of things which were already reached and only to a cumulative maximum which
    was previously reach. Example: Game 1 was survived with STR=30, DEX=25,
    Cooking=200, Blacksmithing=300. Game 2 was survived with STR=35, DEX=25,
    Cook=250, Blacksmith=300. Game 3 was survived with STR=30, DEX=30, Cook=200,
    Blacksmith=350. This totals to STR+DEX=60, Cook+Blacksmith=550. So for
    Game 4, the user can choose STR<=35 (from Game 2), DEX<=30 (from Game 3),
    Cook<=250, Blacksmith<=350, but these also must be met: STR+DEX<=60,
    C+B<=550, so STR=35 and DEX=30 would be too much and STR=40, DEX=20, would
    also not work because you never earned a STR of 40 during play.
- PERMADEATH! Well somewhat. If you die in a game, it is over. You lose all
    your equipment, which you took into the game and all stat and skill advance-
    ments. You keep all skill, stat and cumulative maxes from before the game
    and every item still in the vault
- you have a vault of items in the lobby. When entering a game you can take
    whatever items from your vault you want. During the game you can send items
    to your vault, but cannot take anything from the vault. If you survive the
    game, all items on your person will end up in your vault. You can quit
    a game whenever you want and keep all your items and stats, but then you
    cannot go back and continue the story line. You cannot quit while fighting.
- items from vaults can be traded among players. Money is an item as everything
    else, so you can exchange an one or more items for money or other items
- a market place/auction house is there, if you don't know a buyer or seller
    personally
- the lobby is global, so there is only one auction house and nobody has to
    suffer from bad economy on his server
- with all this you do not really have characters, since you can create a com-
    pletely new character for each game, but to identify with characters you
    can save those setups you like as templates or starting points. Nevertheless
    you can update and change those templates as you like, as long as you stay
    in the confines mentioned above


## Saved Games

- you can save a number of games, but at most 3*n games can be saved if there
    are n players total. Saved games are shared between all players in the game,
    so if you play with a total of 4 players there is only 1 saved game for 4
    players, so it only counts as 1/4th of a game per player. A game shared
    among 2 people is worth 1/2 saved game and single-player games count full.
    Therefore you can have either 3 single-player save games, 192 64-player
    save games or anything in between.
    
## Generated Terrain

- terrain is generated using simulated geology and hydrology
- probably using a torus world
- AI will find the interesting spots and build a story around that
- or: AI will build the story first and nudge the terrain generator into the
    right direction to build a suitable terrain
- or: something in between

## Random Ideas Based on Pat Rothfuss' Comments

- don't do anything with children
- realistic NPC reactions
    - the should have memory
    - do not day "oh someone killed my buddy, but that's probably ok 2 seconds later"
    - "someone is dismanteling my stuff, that's probably ok"
- player should never feel helplessness
- player should be able to do something about whatever bothers him
- player should be able to talk to every npc
- no npc should be marked "bad" by the game
- a "raider" should be identifiable by his outfit, but still it should be possible to befriend him
- roleplaying: npcs should react to your appearance (i.e. having your gun out)
- roleplaying: optionally must eat and drink and sleep
- npcs should not pick a fight with a guy in a robot suit
- voice recognition
- disguise, by wearing the same clothes as the npcs
- buddies should not walk into line of fire (especially not yours)
- npcs need survival instinct
- if npcs are outclassed, they should recognize it and act accordingly like giving up or running away
- assign people to make stuff you choose including making ingredients after showing them the process a couple of times
- settlers should have a clear job and not wander around aimlessly
- settlers should have interests and work better when assigned to appropriate jobs
- actual tower defense mechanics for settlements
- settlers should choose a job on their own
- settlers may be lazy and cause conflict
- settlers should complain about other lazy settlers or if they have to do jobs they don't like
- work schedule, so everyone can be equally unhappy about doing bad jobs

