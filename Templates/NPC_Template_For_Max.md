<%*
const dataview = app.plugins.plugins["dataview"];
if (!dataview) {
    throw new Error("Dataview plugin is not installed or enabled.");
}

// Load Dataview API
const dv = dataview.api;

const raceInput = await tp.system.prompt("Enter NPC Race");
const subraceInput = await tp.system.prompt("Enter NPC Sub-Race");

tp.user.race = raceInput;
tp.user.subrace = subraceInput;
_%>
---
race:  <% tp.user.race %>
subrace: <% tp.user.subrace %>
---
