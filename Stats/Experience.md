## XP Sources
  
**Questing:**  

Main Quests - 75 XP  
College Quests - 50 XP  
Thieves Quests - 50 XP  
Brotherhood Quests - 50 XP  
Companions Quests - 50 XP  
Daedric Quests - 75 XP  
Side Quests - 50 XP  
CivilWar Quests - 75 XP  
Dawnguard Quests - 50 XP  
Dragonborn Quests - 75 XP  
Quest Objectives - 10 XP  

  
  
**Exploring:**  

Fort - 15 XP  
Nordic Ruin - 15 XP  
Dwemer Ruin - 20 XP  
Shipwreck - 20 XP  
Dragon Lair - 30 XP  
Doomstone - 20 XP  
Imperial Tower - 15 XP  
Orc Stronghold - 15 XP  
Giant Camp - 20 XP  
Nordic Tower - 20 XP  
Nordic Dwelling - 20 XP  
Daedric Shrine - 30 XP  
Default - 10 XP  

  
  
**Clearing:**  

Cave - 40 XP  
Fort - 60 XP  
Nordic Ruin - 100 XP  
Dwemer Ruin - 100 XP  
Dragon Lair - 100 XP  
Imperial Tower - 50 XP  
Giant Camp - 60 XP  
Nordic Tower - 50 XP  
Default - 30 XP  

  
  
**Killing:**  

Final XP reward is calculated from racial XP and multipliers:  
  
$$
finalXP = ceil(racialXP * levelMult * groupMult) 
$$
  
Level multiplier gives penalty or bonus based on level difference:  
  
$$
\text{levelMulti} = 1 - \frac{\text{playerLevel} - \text{victimLevel}}{\text{levelRange}}
$$