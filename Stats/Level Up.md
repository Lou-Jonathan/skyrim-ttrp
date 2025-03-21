## **Starting Stats**
---
All player starts with 10 levels in every skill.
All player starts with 10 levels in every attributes.
## **Skill Points**
---
Base skill points per level: 10
Player level multiplier: 3

**Formula for a single level total skill point for a given level.**
$$
\text{SkillPoints}_\text{level} = 10 + 3 \times \text{level}
$$

- $S_n$​: Total cumulative skill points from level 1 to level n.
- $∑_{k=1}^n$: Summation from $k$=1 to $k$ = $n$.
- 10+$3k$: Skill points at level $k$.

**Formula for the total amount of skill points for a given level.**
$$S_n = ∑_{k=1}^n (10 + 3k)$$
## **Skill Tree Restrictions and Bonus**
---
The cost to level skills increases at skill levels 25, 50, and 75. These are the default costs:

| Level                | Novice      | Apprentice | Journeyman | Expert    | Master  |
| -------------------- | ----------- | ---------- | ---------- | --------- | ------- |
| Skill Tree Level     | 0-24        | 25-49      | 50-74      | 75-99     | 100     |
| Point cost per level | 3           | 5          | 7          | 9         | x       |
| Max Spell Level      | Level 0-1-2 | Level 3-4  | Level 5-6  | Level 7-8 | Level 9 |

## **Skill Restrictions**
---
To prevent unnatural large jumps in skill levels, a player can only increase any given skill a default of 5 times per level.  
  
To prevent players from powergaming early on, there is a maximum skill value that is based on player level.

Max skill level base default: 20  
Max skill level multiplier: 2 
Default max skill level: 100

$$
\text{MaxSkillLevel} = \text{MaxSkillLevelBaseDefault} + (\text{CurrentPlayerLevel} \times \text{MaxSkillLevelMultiplier})
$$


## **Attributes**
---
Attributes stats a related to your Skill Tree level. Each attribute is governed by 3 Perk Tree, and the advancement you make in them reflects on the attribute stats.

For each 15 levels total gained in a attribute,

| Total Skill Point | Attribute Level |
| ----------------- | --------------- |
| 45                | 11              |
| 60                | 12              |
| 75                | 13              |
| 90                | 14              |
| 105               | 15              |
| 120               | 16              |
| 135               | 17              |
| 150               | 18              |
| 165               | 19              |
| 180               | 20              |
| 195               | 21              |
| 210               | 22              |
| 225               | 23              |
| 240               | 24              |
| 255               | 25              |
| 270               | 26              |
| 285               | 28              |
| 300               | 30              |

## **Health Calculation**
---
You start with 10 Health Points at level 1. Every level, you get your Endurance attribute divided by 2.

HP per Level:
$$
HP = END - 5
$$

Quick Total HP Formula: 
$$
Total HP = 10 + ∑_{k=2}^n (END - 5)
$$

## **Magicka Calculation**
---
You start with 10 Magicka at level 1, and you passively regenerate 5% rounded down at a minimum of 1. The following table shows the cost of each tiered spell :

| Spell Tier | Magicka Cost |
| ---------- | ------------ |
| 0          | 1            |
| 1          | 5            |
| 2          | 10           |
| 3          | 15           |
| 4          | 20           |
| 5          | 25           |
| 6          | 30           |
| 7          | 35           |
| 8          | 40           |
| 9          | 45           |
Your Magicka Pool will increase for every level that one of the Magic governing attribute increases above 10. Here is the list : 
- **Intelligence**: 5 Magicka Points
- **Willpower**: 3 Magicka Points
- **Personality**: 2 Magicka Points

Example : A Healer has 12 Intelligence, 14 Personality and 15 Willpower. The total Magicka Pool is :
Int 12-10=2; 2x5=10
Per 14-10=4; 4x2 = 8
Wil 15-10=5; 5x3 = 15
Total Magicka Pool : 10(Initial Pool) + 10(Int) + 8(Per) + 15(Wil) = 43 