# Fixture Group Labeler

## Overview
The **Fixture Group Labeler** is a Lua script for GrandMA2 that automates the process of assigning groups to fixtures based on their fixture numbers and labeling the groups accordingly. This script enhances the efficiency and manageability of your lighting setup by ensuring that each group is clearly labeled with the name of its corresponding fixture.

## Features
- **Automatic Group Assignment**: Assigns groups to fixtures based on a predefined list of fixture numbers.
- **Dynamic Labeling**: Retrieves and applies fixture names as group labels.
- **Clear Previous Selections**: Ensures a fresh start by clearing all previous selections before execution.

## Script Details

### Functions
1. **getFixtureName(fixtureNumber)**: Retrieves the name of a fixture given its number.
2. **labelGroupWithFixtureName(groupNumber, fixtureNumber)**: Labels a group with the name of the corresponding fixture. Logs a message if the fixture name is not found.
3. **assignAndLabelFixtures()**: Main function that performs the group assignment and labeling process.

### Code
```lua
-- Lua Script for GrandMA2
-- This script assigns groups to fixtures based on their fixture numbers and labels them accordingly.

local function getFixtureName(fixtureNumber)
    local handle = gma.show.getobj.handle('Fixture ' .. fixtureNumber)
    return gma.show.getobj.name(handle)
end

local function labelGroupWithFixtureName(groupNumber, fixtureNumber)
    local fixtureName = getFixtureName(fixtureNumber)
    if fixtureName then
        gma.cmd('Label Group ' .. groupNumber .. ' "' .. fixtureName .. '"')
    else
        gma.echo('No name found for fixture ' .. fixtureNumber)
    end
end

local function assignAndLabelFixtures()
    -- Clear all previous selections.
    gma.cmd('ClearAll')
    
    -- Fixture numbers whose names need to be retrieved.
    local fixturesToLabel = {1, 101, 201, 301, 401, 501, 601}
    
    -- Loop through the list of fixtures and assign names to the groups.
    for i, fixtureNumber in ipairs(fixturesToLabel) do
        labelGroupWithFixtureName(i, fixtureNumber)  -- Group numbers correspond to the index in the list.
    end
end

assignAndLabelFixtures()
```

### How to Use
1. **Load the Script:** Import the script into the GrandMA2 console or onPC software.
2. **Execute the Script:** Run the script to automatically assign and label groups based on the predefined fixture numbers.
3. **Verify Labels:** Check the groups to ensure they are labeled correctly according to the fixture names.
