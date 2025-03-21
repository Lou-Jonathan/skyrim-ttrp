# Player Guide: Skyrim D&D Campaign
---
Welcome to a unique and humorous twist on the world of _Skyrim_! In this campaign, you’ll roleplay as yourselves trapped inside your _Skyrim_-created characters. The NPCs will treat you as if you’re part of their world, unaware that you’re players. The world itself is a quirky, glitchy version of _Skyrim_, where bugs and lags occasionally break reality—like placing a bucket on a merchant’s head to rob their store. However, an omniscient entity (the DM) may patch these glitches depending on a dice roll. If the roll succeeds, the bug is fixed; if not, it remains, but the next roll has a higher chance to succeed.

This guide will walk you through the lore, character creation, mechanics, and systems of this campaign. Let’s get started!

---
## **The World of Skyrim (Modded Edition)**

### Setting
---
You’ll explore the province of _Skyrim_ and beyond, venturing through familiar locations like Whiterun, Solitude, and Riften, as well as new areas added by the DM’s “mods.” The world is vast, filled with ancient ruins, treacherous dungeons, and bustling cities. However, this version of _Skyrim_ is different from the one you know—your DM has added hidden quests, unique NPCs, and strange enemies. Expect the unexpected!

### Lore
---
- **The Dragonborn**: You are the Dragonborn, a chosen one with the power to wield the Thu’um (Dragon Shouts). Your destiny is tied to the return of the dragons and the fate of Skyrim.
- **Factions and Conflicts**: The world is shaped by the ongoing civil war between the Imperial Legion and the Stormcloaks, as well as the threat of the dragon Alduin. Additionally, ancient factions like the Thieves Guild, Dark Brotherhood, and College of Winterhold play significant roles.
- **Races and Cultures**: Skyrim is home to diverse races, each with its own culture and history. While Nords dominate the province, other races like Altmer, Argonians, and Khajiit face varying degrees of acceptance or prejudice.

---
## **Character Creation**

### Races
---
You can choose any race from _Elder Scrolls_ lore, but the recommended options are:
```dataview
table without id file.link as "Race"
from "Characters/Race"
```
### Races Advantage
---
Each race has unique perks and advantages, but they won’t limit your character’s ability to grow. Choose wisely, as some races may face backlash in Skyrim due to prejudice.

---
### **Leveling System**

#### Starting Stats
---
All player starts with 10 levels in every skill.
All player starts with 10 levels in every attributes.
#### Skill Points
---
Base skill points per level: 10
Player level multiplier: 3

**Formula for a single level total skill point for a given level.**
$$
\text{SkillPoints}_\text{level} = 10 + (3 \times \text{level)}
$$

**Example**: I just reached level 10, I have 10+(3x10)=40 perk points to invest in skills
#### Skill Tree Restrictions and Bonus
---
The cost to level skills increases at skill levels 25, 50, and 75. These are the default costs:

| Level                | Novice      | Apprentice | Journeyman | Expert    | Master  |
| -------------------- | ----------- | ---------- | ---------- | --------- | ------- |
| Skill Tree Level     | 0-24        | 25-49      | 50-74      | 75-99     | 100     |
| Point cost per level | 3           | 5          | 7          | 9         | x       |
| Max Spell Level      | Level 0-1-2 | Level 3-4  | Level 5-6  | Level 7-8 | Level 9 |

#### Skill Restrictions
---
To prevent unnatural large jumps in skill levels, a player can only increase any given skill a default of 5 times per level.  
  
To prevent players from powergaming early on, there is a maximum skill value that is based on player level.

Max skill level base default: 20  
Max skill level multiplier: 2 
Default max skill level: 100

$$
\text{MaxSkillLevel} = 20 + (\text{CurrentPlayerLevel} \times 2)
$$

**Example**: I am level 10, my max skill level is 20+(10x2) = 40.

**Automatic Unlocks**: Perks are automatically acquired when you reach specific levels in a skill tree. There are no perk points to spend—your progression is tied directly to your skill level.
#### Magic System
---
- **Oblivion Magic Schools → D&D Schools**:
    
    - Alteration → Transmutation
    - Conjuration → Conjuration + Necromancy
    - Destruction → Evocation
    - Illusion → Illusion + Enchantment
    - Restoration → Abjuration + Necromancy
    - Mysticism → Divination

#### Shouts
---
- Discover Shouts by finding Word Walls in dungeons or other locations.
- Roll on a table to determine which Shout you learn. If you already know part of the Shout, you’ll learn the next word (e.g., if you know “Ro” for Unrelenting Force and roll Unrelenting Force, you’ll learn “Da”).
#### **Attributes & Skills**
---
```dataview
table without id file.link as "Attributes", skills as "Skills"
from "Stats/Attributes"
```
---
## **Crafting Systems**

### Alchemy
---
- Ingredients have 4 potential uses, discovered through experimentation.
- A **Toxicity Meter** prevents potion abuse. Overuse of potions can lead to negative effects. This is heavily inspired from the game "The Witcher". This is very impactful because potions and poisons will be abundant.
### Enchanting
---
1. **Soul Gems**: Use appropriate soul gems to enchant items (e.g., Petty Soul Gem for weak effects, Black Soul Gem for powerful effects).
2. **Learning Enchantments**: Study an enchanted item to learn its enchantment. The item is destroyed in the process.
3. **Crafting Time**: Takes 7 days per soul gem category (Petty, Lesser, Common, Greater, Grand, Black).
4. **Arcana Check**: Roll an Willpower check (DC 15-25 depending on soul gem category). Failure wastes the soul gem and deals 2d10 necrotic damage per soul gem category.
5. **Charges**: Enchanted items have charges based on the Arcana check result. Recharge by spending days and automatically succeeding on the Arcana check.
### Smithing/Crafting
---
- **Unlock Recipes**: As your Smithing skill improves, you’ll unlock the ability to craft new weapons, armor, and items from the _Skyrim_ universe. Recipes are tied to your Smithing level and the resources you gather.
- **Materials Needed**: Crafting requires specific materials (e.g., iron ingots, leather strips, ebony ore). Gather these through mining, looting, or purchasing from merchants.
- **Perk System**: Invest points into the Smithing skill tree to unlock advanced crafting perks, such as:
    - **Steel Smithing**: Craft steel weapons and armor.
    - **Elven Smithing**: Craft elven weapons and armor.
    - **Daedric Smithing**: Craft Daedric weapons and armor (requires rare materials like Daedra Hearts).
- **Crafting Time**: Crafting takes time and requires access to a forge or workbench. The DM will determine the time required based on the complexity of the item.
- **Quality**: The quality of crafted items depends on your Smithing level and the materials used. Higher-tier materials (e.g., ebony, Daedric) produce stronger and more durable items.
---
## **Deity System**

- Choose a deity from the following pantheons: 
	- **Daedra** ([[Mehrunes Dagon]], [[Molag Bal]], and others)
	- **Elven Ancestors** ([[Auriel]], [[Magnus]], and others)
	- **Khajiit Pantheon** ([[Rajhin]], [[Riddle'Thar]], and others)
	- **Miscellaneous Deities** ([[St. Alessia]], [[Sithis]], and others)
	- **Nine Divines** ([[Akatosh]], [[Talos]], and others)
	- **Yokudan Pantheon** ([[Leki]], [[Tall Papa]], and others)
- **Pray Daily**: Deepen your bond with your deity to gain their favor and powers.
- **Forsaking Tenets**: If you abandon your deity’s tenets, they may punish or abandon you.
---
## **Starting the Adventure**

Your journey begins in **Helgen**, following the iconic intro from _Skyrim_. From there, the world is yours to explore—just remember, this is a modded version of _Skyrim_, so expect surprises!

---
## **Tips for Players**

- **Roleplay Wisely**: NPCs will treat you as part of their world. Stay in character!
- **Embrace the Chaos**: Glitches and bugs are part of the fun. Use them creatively, but be prepared for the DM to patch them.
- **Experiment**: Try out alchemy, enchanting, and shouts to discover their full potential.
- **Work Together**: As Dragonborn, your fates are intertwined. Collaborate to overcome challenges and uncover secrets.

---

Enjoy your adventure in this quirky, modded version of _Skyrim_! May your Thu’um be strong, your potions be potent, and your glitches be cheesy. Good luck, Dragonborn!