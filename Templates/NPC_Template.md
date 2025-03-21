<%*
// Ensure Dataview plugin is loaded
const dataview = app.plugins.plugins["dataview"];
if (!dataview) {
    throw new Error("Dataview plugin is not installed or enabled.");
}

// Load Dataview API
const dv = dataview.api;

// Prompt user to select an archetype
const archetypes = dv.pages('"Archetypes"').map(page => page.file.name);
const selectedArchetype = await tp.system.suggester(archetypes, archetypes);

// Prompt user to enter NPC level
const levelInput = await tp.system.prompt("Enter NPC level:");
const level = parseInt(levelInput);
if (isNaN(level) || level <= 0) {
    throw new Error("Invalid level input. Please enter a positive number.");
}

// Load archetype data
const archetypeData = dv.page(`Archetypes/${selectedArchetype}`);
if (!archetypeData) {
    throw new Error(`Archetype file "${selectedArchetype}" not found.`);
}

const primarySkills = archetypeData.primary_skills;
const secondarySkills = archetypeData.secondary_skills;

// Calculate total skill points
const calculateSkillPoints = (level) => {
    let total = 0;
    for (let k = 1; k <= level; k++) {
        total += 10 + 3 * k;
    }
    return total;
};
const totalSkillPoints = calculateSkillPoints(level);

// Define skill level cost thresholds
const skillCosts = { 0: 3, 25: 5, 50: 7, 75: 9, 100: Infinity };
const maxSkillLevelBase = 20;
const maxSkillLevelMultiplier = 2;
const maxSkillLevel = Math.min(maxSkillLevelBase + (level * maxSkillLevelMultiplier), 100); // Cap at 100

// Function to determine cost per skill level
const getSkillCost = (currentLevel) => {
    if (currentLevel >= 75) return skillCosts[75];
    if (currentLevel >= 50) return skillCosts[50];
    if (currentLevel >= 25) return skillCosts[25];
    return skillCosts[0];
};

// Distribute skill points with priority handling
const distributeSkillPoints = (skills, availablePoints) => {
    let skillLevels = {};
    let skillPointsInvested = {}; // Track points invested in each skill
    skills.forEach(skill => {
        skillLevels[skill] = 10; // All start at 10
        skillPointsInvested[skill] = 0; // Initialize points invested
    });
    
    let remainingPoints = availablePoints;

    // Loop through each skill and increase levels until no points remain
    while (remainingPoints > 0) {
        let pointsSpentInLoop = 0; // Track points spent in this iteration

        skills.forEach(skill => {
            if (remainingPoints <= 0) return; // Exit if no points remain

            const currentLevel = skillLevels[skill];
            if (currentLevel >= maxSkillLevel) return; // Skip if skill is already at max

            const cost = getSkillCost(currentLevel);
            if (remainingPoints >= cost) {
                remainingPoints -= cost;
                skillLevels[skill]++;
                skillPointsInvested[skill] += cost;
                pointsSpentInLoop += cost;
            }
        });

        // If no points were spent in this loop, break to avoid infinite loops
        if (pointsSpentInLoop === 0) break;
    }

    return { skillLevels, skillPointsInvested, remainingPoints };
};

// Allocate points separately to primary and secondary skills
let availablePoints = totalSkillPoints;
const primaryResult = distributeSkillPoints(primarySkills, availablePoints * 0.6); // 60% for primary skills
availablePoints -= (totalSkillPoints * 0.6 - primaryResult.remainingPoints);
const secondaryResult = distributeSkillPoints(secondarySkills, availablePoints); // Remaining for secondary skills

// Combine results
const skillLevels = { ...primaryResult.skillLevels, ...secondaryResult.skillLevels };
const skillPointsInvested = { ...primaryResult.skillPointsInvested, ...secondaryResult.skillPointsInvested };
const remainingPoints = secondaryResult.remainingPoints;

// Calculate total points invested
const totalPointsInvested = Object.values(skillPointsInvested).reduce((sum, points) => sum + points, 0);

// Format skill levels and points invested for display
const formatSkillLevels = (skillLevels) => {
    return Object.entries(skillLevels)
        .map(([skill, level]) => {
            // Extract only the skill name
            const skillName = skill.replace(/\[\[Stats\/Skills\/(.*?)\.md\|\1\]\]/g, '[[$1]]');
            return `  - ${skillName}: ${level}`; // Add consistent indentation
        })
        .join("\n");
};

const formatSkillPointsInvested = (skillPointsInvested) => {
    return Object.entries(skillPointsInvested)
        .map(([skill, points]) => {
            const skillName = skill.replace(/\[\[Stats\/Skills\/(.*?)\.md\|\1\]\]/g, '[[$1]]');
            return `  - ${skillName}: ${points}`; // Add consistent indentation
        })
        .join("\n");
};

// Load existing skills from "Stats/Skills/" and format them as links
const existingSkills = dv.pages('"Stats/Skills"')
    .map(page => `[[${page.file.name}]]`);

// Merge primary and secondary skills, ensuring no duplicates from existing skills
// Create a single skills object and ensure no duplicates
let allSkills = {};

// Merge primary and secondary skills
[...Object.keys(primaryResult.skillLevels), ...Object.keys(secondaryResult.skillLevels), ...existingSkills].forEach(skill => {
    // Standardize the skill format
    let formattedSkill = skill.replace(/\[\[Stats\/Skills\/(.*?)\.md\|\1\]\]/g, '[[$1]]');
    
    // If the skill is already present, keep the highest level
    if (!allSkills[formattedSkill] || allSkills[formattedSkill] < (primaryResult.skillLevels[skill] || secondaryResult.skillLevels[skill] || 10)) {
        allSkills[formattedSkill] = primaryResult.skillLevels[skill] || secondaryResult.skillLevels[skill] || 10;
    }
});

// Format skills for output
const formattedSkills = Object.entries(allSkills)
    .map(([skill, level]) => `  - ${skill}: ${level}`) // Add consistent indentation
    .join("\n");

// Function to calculate attribute level based on total skill points
function calculateAttributeLevel(totalPoints) {
    if (totalPoints < 45) return 10; // Default to 10 if below 45
    if (totalPoints >= 300) return 30; // Cap at 30 for 300 or more points

    // Mapping of total skill points to attribute levels
    const levelMap = [
        { points: 45, level: 11 },
        { points: 60, level: 12 },
        { points: 75, level: 13 },
        { points: 90, level: 14 },
        { points: 105, level: 15 },
        { points: 120, level: 16 },
        { points: 135, level: 17 },
        { points: 150, level: 18 },
        { points: 165, level: 19 },
        { points: 180, level: 20 },
        { points: 195, level: 21 },
        { points: 210, level: 22 },
        { points: 225, level: 23 },
        { points: 240, level: 24 },
        { points: 255, level: 25 },
        { points: 270, level: 26 },
        { points: 285, level: 28 },
        { points: 300, level: 30 },
    ];

    // Find the appropriate level based on total points
    for (const entry of levelMap) {
        if (totalPoints < entry.points) {
            return entry.level - 1; // Return the previous level
        }
    }
    return 30; // Default to 30 if not found (should not happen)
}

// Load Attributes
const attributes = dv.pages('"Stats/Attributes"').map(page => page.file.name);

// Object to store attribute levels
const attributeLevels = {};

// Loop through each attribute file
attributes.forEach(attribute => {
    // Construct the full path to the attribute file
    const attributeData = dv.page(`Stats/Attributes/${attribute}`);
    
    // Log the attribute name (alias) and remove .md, then surround with [[ ]]
    const attributeAlias = attribute.split('/').pop().replace('.md', ''); // Remove .md

    // Initialize total points for the attribute
    let totalPoints = 0;

    // Check if the attributeData exists and has the 'skills' property
    if (attributeData && attributeData.skills) {
        // Handle skills as an array or single value
        if (Array.isArray(attributeData.skills)) {
            attributeData.skills.forEach(skill => {
                if (typeof skill === 'string') {
                    const skillAlias = skill.split('/').pop().replace('.md', ''); // Remove .md
                    const formattedSkill = `[[${skillAlias}]]`; // Format skill name
                    // Find the skill level from allSkills
                    const skillLevel = allSkills[formattedSkill] || 0; // Default to 0 if not found
                    totalPoints += skillLevel; // Add to total points
                } else if (skill && skill.path) {
                    const skillAlias = skill.path.split('/').pop().replace('.md', ''); // Remove .md
                    const formattedSkill = `[[${skillAlias}]]`; // Format skill name
                    // Find the skill level from allSkills
                    const skillLevel = allSkills[formattedSkill] || 0; // Default to 0 if not found
                    totalPoints += skillLevel; // Add to total points
                } else if (skill && skill.name) {
                    const skillAlias = skill.name.replace('.md', ''); // Remove .md
                    const formattedSkill = `[[${skillAlias}]]`; // Format skill name
                    // Find the skill level from allSkills
                    const skillLevel = allSkills[formattedSkill] || 0; // Default to 0 if not found
                    totalPoints += skillLevel; // Add to total points
                }
            });
        } else if (typeof attributeData.skills === 'string') {
            const skillAlias = attributeData.skills.split('/').pop().replace('.md', ''); // Remove .md
            const formattedSkill = `[[${skillAlias}]]`; // Format skill name
            // Find the skill level from allSkills
            const skillLevel = allSkills[formattedSkill] || 0; // Default to 0 if not found
            totalPoints += skillLevel; // Add to total points
        }
    }

    // Calculate attribute level based on total points
    const attributeLevel = calculateAttributeLevel(totalPoints);

    // Store the attribute level in the object
    attributeLevels[`[[${attributeAlias}]]`] = attributeLevel;
});

// Format the attributes as a string with consistent indentation and [[ ]] around attribute names
const formattedAttributes = Object.entries(attributeLevels)
    .map(([attribute, level]) => `  - [[${attribute.replace(/\[\[|\]\]/g, '')}]]: ${level}`) // Ensure [[ ]] around attribute names
    .join("\n");

// Save results to template variables
tp.user.attributes = formattedAttributes; // Assign the formatted string
tp.user.level = level; // Assuming `level` is defined elsewhere
tp.user.selected_archetype = selectedArchetype; // Assuming `selectedArchetype` is defined elsewhere
tp.user.total_skill_points = totalSkillPoints; // Assuming `totalSkillPoints` is defined elsewhere
tp.user.skill_points_invested = formatSkillPointsInvested(skillPointsInvested); // Assuming `skillPointsInvested` is defined elsewhere
tp.user.total_points_invested = totalPointsInvested; // Assuming `totalPointsInvested` is defined elsewhere
tp.user.remaining_points = remainingPoints; // Assuming `remainingPoints` is defined elsewhere
tp.user.all_skills = formattedSkills; // Assuming `formattedSkills` is defined elsewhere
_%>
---
npc_name: <% tp.file.title %>
level: <% tp.user.level %>
archetype: <% tp.user.selected_archetype %>
race: ""
factions: []
essential: false
quests: []
dead: false
location: ""
home_town: ""
wiki_link: ""
gender: ""
---
## Info
---

## Stats
---
- **Level**: <% tp.user.level %>
- **Archetype**: <% tp.user.selected_archetype %>
- **Attributes**: 
<% tp.user.attributes %>
- **Skills**: 
<% tp.user.all_skills %>
- **Total Skill Points**: <% tp.user.total_skill_points %>
- **Skill Points Invested**: 
<% tp.user.skill_points_invested %>
- **Total Points Invested**: <% tp.user.total_points_invested %>
- **Remaining Skill Points**: <% tp.user.remaining_points %>
---