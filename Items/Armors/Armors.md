# Amors
---
## Light Armors
---
```dataview
table sub-category as "Sub-Category", material as "Material", ac as "AC", weight as "Weight", properties as "Properties"
where sub-category = "Light Armor" and material != null
sort ac asc
```

## Heavy Armors
---
```dataview
table sub-category as "Sub-Category", material as "Material", ac as "AC", weight as "Weight", properties as "Properties", requirements as "Requirements"
where sub-category = "Heavy Armor" and material != null
sort ac asc
```