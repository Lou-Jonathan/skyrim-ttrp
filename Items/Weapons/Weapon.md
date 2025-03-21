# Weapon
---
## One-Handed
---
### War Axes
---
All war axes have the light and versatile property.

```dataview
table damage as "Damage", properties as "Properties"
where sub-category = "War Axe" and material != null
sort leveled-list asc, name asc
```
### Dagger
---
All daggers have the light and finesse properties.

```dataview
table damage as "Damage", properties as "Properties"
where sub-category = "Dagger" and material != null
```

### Maces
---
Maces are known for their powerful attacks.

```dataview
table damage as "Damage", properties as "Properties"
where sub-category = "Mace" and material != null
```

### Sword
---
All swords have the light and finesse properties.

```dataview
table without id file.link as "Name", damage as "Damage", properties as "Properties"
where sub-category = "Sword" and material != null
sort leveled-list asc, name asc
```

## Two-Handed

### Greatsword
---
All greatswords have the heavy and two-handed properties.

```dataview
table without id file.link as "Name", damage as "Damage", properties as "Properties"
where sub-category = "Greatsword" and material != null
sort leveled-list asc, name asc
```

### Battleaxe
---


```dataview
table without id file.link as "Name", damage as "Damage", properties as "Properties"
where sub-category = "Battleaxe" and material != null
sort leveled-list asc, name asc
```

### Warhammer
---


```dataview
table without id file.link as "Name", damage as "Damage", properties as "Properties"
where sub-category = "Warhammer" and material != null
sort leveled-list asc, name asc
```
## Ranged Weapons

### Bow
---

```dataview
table without id file.link as "Name", damage as "Damage", properties as "Properties"
where sub-category = "Bow" and material != null
sort leveled-list asc, name asc
```