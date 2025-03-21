---
type: Shout
shout: Throw Voice
---
# Throw voice
---
*The Thu'um is heard, but its source unknown, fooling those into seeking it out.*

A sound of your choice is heard from a point within radius, and all creatures withing 100ft. of it can hear it, even as a whisper if it is too silent for them to normally hear it.

```dataview
table rank as "Rank", meaning as "Meaning"
where shout = "Throw Voice" and rank != null
sort rank asc
```