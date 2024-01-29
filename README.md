# TextAdventureEngine
 Text adventure engine that has a sample fantasy game loaded in. For the first iteration I am going to try to make it as simple as possible. The engine and game will run as the same exe.
 The user will add their text files to the rooms folder and the engine will run with those rooms. 
 Maybe in future iterations the engine will generate a separate executable for the game made out of those text files. 
 
 How to use this engine:
 -
Elements are contained within ```(element)(/element)``` blocks.

First create a text file for setting up the game in the setup folder: 
- Setup player hp example:
```
(player)(hp)10(/hp)(/player)
```

Create text files for each room in the rooms folder with the following supported elements:
- Room id. Must be a unique id. Example:
```
(id)1(/id)
```

- Story of the room displayed on entrance of the room. Example: 
```
(story) You wake up in a a room with no belongings and the room is dark. You can hear rats in the distance squeaking as you move around the
room, you notice that you are in a jail cell. You find there is a key hanging on the wall (/story)
```

- Pickup items

Listed as objects in the room that can be picked up. When selected user has the option to pick up or identify. Picking up the item adds the item to the player's inventory. Identifying the item shows the items description and, if it is not a key, the value. Example: 
``` 
    1. Dagger
    2. Health potion
    3. Iron chest piece
    4. Dungeon key
    (user picks 1)
    1. Pickup
    2. Identify
    (user picks 1)
    You pickup the Dagger
    (user picks 2)
    A small blade capable of light damage to your foes. 5 damage.
```
    
  

1. Weapon

Example: ```(weapon)(title)Dagger(/title) (value)5(/value) (description)A small blade capable of light damage to your foes.(/description)```

2. Potion

Example: ```(potion)(title)Health potion(/title) (value)10(/value) (description)A bottle with red liquid inside it appears to give life.(/description)(/potion)```

3. Armor

Example: ```(armor)(title)Iron chest piece(/title) (value)2(/value) (description)A chest piece made from rusted iron it should protect you from light blows.(/description)(/armor)```

5. Key

Example: ```(key)(title)Dungeon key(/title) (id)2(/id) (description)A key that appears to have an emerald top.(/description)(/key)```

- Locked or  unlocked room. 

Rooms are unlocked by the key that has an id matching the room id. 
Locked room example: ```(locked)true(/locked)```
Unlocked room example: ```(locked)false(/locked)```

- Enemy

Example: ```(enemy)(title)Rat(/title) (hp)10(/hp) (dmg)1(/dmg) (armor)0(/armor)(description)A little rodent looking for cheese.(/enemy)```

Connecting rooms
-

To connect the rooms an id and cardinal direction is required.

Example: 
```
(north)2(/north)
(east)3(/east) 
(south)4(/south) 
(west)5(/west)
```

Combat
-
Each enemy listed in the room file will be an option listed along with the items in the room. Choosing the enemy will allow 2 options identify, which shows the description of the enemy, or attack. 

Each time the Attack option is chosen the damage the player deals is equal to the players weapon damage minus the armor of the enemy and similarly the enemys damage is its weapon damage minus player armor. 

When the enemy reaches 0 hp it dies. When the player reaches 0 hp the game is over. 

Choosing inventory allows the player to use items from inventory during combat but allows the enemy to make a free attack that turn.

Example:
```
1. Dagger
2. Health potion
3. Iron chest piece
4. Dungeon key
5. Rat
(user chooses 5)
1. Identify
2. Attack
(user chooses 2)
You deal 5 damage to the Rat. The Rat deals 0 damage to you. You have 10 hp. The Rat has 5 hp.
1. Attack
2. Inventory
(user chooses 2)
Inventory:
1. Dagger
2. Health potion
(user chooses 2)
You heal for 0 hp. The Rat deals 0 damage to you.
1. Attack
2. Inventory
(user chooses 1)
You deal 5 damage to the Rat. The Rat deals 0 damage to you. You have 10 hp. The Rat has 0 hp.
The Rat dies.
```
