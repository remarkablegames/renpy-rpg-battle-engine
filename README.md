# RPG Battle Engine for Ren'Py

## Table of contents
* [Features](#features)
* [Screenshots](#screenshots)
* [Documentation](#documentation)
* [Credits](#credits)

## Features
* 3 player slots and 8 monster slots
* Monsters split between two rows (you can't attack a monster in the back row if there's another one in front of it)
* Active and passive skills
* Player skills can target enemies (one, more or all), allies (one or more), k.o. allies (to revive them) and themselves
* Monsters can use skills too (attack only)
* "Attack", "Defend" and "Use Item" commands
* Damage, accuracy, experience and leveling formulas
* Randomized monster selection and slot position
* In-battle inventory system
* Player selection screen
* Mouse-following Tooltips
* Message box at the top of the screen
* ATL for players, monsters and damage display
* Animated hp and mp bars

## Screenshots

![screenshot 1](screenshots/1.png)
![screenshot 2](screenshots/2.png)
![screenshot 3](screenshots/3.png)
![screenshot 4](screenshots/4.png)

## Documentation

### Create new character:
1. Open scripts/define/char_def.rpy and scroll to the bottom
2. Use this template and follow the previous examples to define a new character:
```py
define character.var = Character("Name", image="")
default var = Char("Name", img="", skills=[], p_skills=[], equip={'hand': None, 'head': None, 'chest': None, 'accs': None})
```
3. Open scripts/define/assets/images.rpy and define the battle avatar, either following the examples or using this more basic template:
```py
image char_battle = "images/char/char_battle.png"
```
4. Add the character sprite/s to the images/char folder
5. You can now add it to the party_list list:
```py
$ var.append(party_list)
```

### Create new monster:
1. Open scripts/define/monsters_def.rpy and look for the load_monsters label
2. Use this template and follow the examples to define a new monster:
```py
monster_var = Monster(name, hpmax, atk, dfn, exp, lvl, img, sfx_atk, anim, skills)
```
3. Add the monster sprite to the images/monsters folder
4. You can now add it to the wild_monsters list:
```py
$ monster_var.append(wild_monsters)
```

### Create new skill:
1. Open scripts/define/battle_def.rpy and look for the other skills defined at the bottom
2. Follow the examples and use the respective template depending if it's a passive or active skill:
```py
default skill_var = ActiveSkill(name, pwr, mp_cost, sfx, targ, targs, type='active', trans=None, img=None, back_row=False)`
default skill_var = PassiveSkill(name, sfx=None, img=None, trans=None, lvl=0)
```
3. You can now append it to a character:
```py
$ skill_var.addSkill(a)
```

### Create new item:
1. Open scripts/define/items_def.rpy and look for the load_items label
2. Use this template and follow the examples to define a new item:
```py
item_var = Item(name, desc, icon=False, value=0, act=Show("inventory_popup", message="Nothing happened!"), type="item", recipe=False, tags={})
```
3. Add the item sprite to the images/inv folder
4. You can now append it to your inventory, indicating the quantity:
```py
$ player_inv.take(item_var,2)
```

### battle.rpy:
* Battle setup
* Player select screens
* Tooltip screen
* Player and monster display screens
* Message screen
* "label battling": switchs between player and monsters turns
* "label end_battle"

### player_actions.rpy:
* "label turn_actions": handles player turn phases
* "label player_skill": handles the type of action that was selected (skill, item, defend, etc.)
* Skill select screen
* Target select screens (enemy, ally, row, etc.)
* Damage animation screens

## Credits
* RPG Framework by Gabriel Herrera [@Habitacle](https://github.com/Habitacle)
* Music by Lucy Villarreal [@filmnoirtoday](https://www.instagram.com/filmnoirtoday/)

### Scripts
* [Inventory system by saguaro](https://lemmasoft.renai.us/forums/viewtopic.php?t=25579)
* [TransitionConditionSwitch by Asceai](https://lemmasoft.renai.us/forums/viewtopic.php?t=26612)
* [Mouse following Tooltip by Human Bolt Diary](https://lemmasoft.renai.us/forums/viewtopic.php?t=47205)
* [Random statement by PyTom](https://patreon.renpy.org/three-creator-defined-statements.html)
* [Random Bag by PyTom](https://patreon.renpy.org/python-tricks-2.html)
* [Shake function by nyaatrap (animation.rpy)](https://github.com/nyaatrap/renpy-utilities)
* [Inspired by Dragonaqua's RPG Battle System](https://lemmasoft.renai.us/forums/viewtopic.php?t=57105)

### Sprites
* [Character sprites from Persona Q2: New Cinema Labyrinth](https://www.spriters-resource.com/3ds/personaq2newcinemalabyrinth/sheet/124365/)
* [Monsters sprites from Pokémon Black / White](https://www.spriters-resource.com/ds_dsi/pokemonblackwhite/sheet/34111/)
* [Item sprites from Atelier Totori: The Adventurer of Arland](https://www.spriters-resource.com/playstation_3/ateliertotoritheadventurerofarland/sheet/67913/)
* [Backgrounds from Hyperdevotion Noire: Goddess Black Heart](https://www.spriters-resource.com/pc_computer/hyperdevotionnoire/sheet/78589/)
* [Skill sprites from Castle Clash](https://www.spriters-resource.com/mobile/castleclash/sheet/61773/)

### Sound effects
* [Pokémon GO](https://www.sounds-resource.com/mobile/pokemongo/sound/7823/)
* [Pokémon Sun / Moon](https://www.sounds-resource.com/3ds/pokemonsunmoon/sound/12170/)
* [FATE Undiscovered Realms](https://www.sounds-resource.com/pc_computer/fateundiscoveredrealms/sound/19238/)
* [Fire Emblem: Awakening](https://www.sounds-resource.com/3ds/fireemblemawakening/sound/8431/)
