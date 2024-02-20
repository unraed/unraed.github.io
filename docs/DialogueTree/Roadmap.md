---
layout: default
title: Dialogue Tree Roadmap
permalink: /DialogueTree/Roadmap
---
**Click [here](DialogueTree.md) to return to the Dialogue Tree home page.** 

# Dialogue Tree: Roadmap
Below you will find a list of planned and in progress features for Dialogue Tree. Features are broken down by priority, and a rough category for each is included in parentheses. As new features are completed they will be moved to the "Completed" section. 

Where appropriate, additional explanations are included at the bottom of the page.

## Help & Support
You can reach me for questions and support at unraedgames@gmail.com, or on the plugin's [**Discord Channel**](https://discord.gg/mf7mGXbePB). Feel free to reach out with any questions or requests. 

If you're enjoying the plugin, I would be extremely grateful if you could take a few moments out of your day to leave me a review on the [**Unreal Marketplace**](https://www.unrealengine.com/marketplace/en-US/product/dialogue-tree). 

If you would like to support further development on the project you can do so on [**Patreon.com**](https://www.patreon.com/UnraedGames). 

## High Priority 
- Auto-arrange feature (Quality of Life)
- Ability to search for and focus a specific node in the graph (Quality of Life)
- Ability to collapse groups of nodes into a "macro" or folder node (Quality of Life) - [Note 1](Roadmap.md#note-1-collapsing-groups-of-nodes-to-a-macro) 

## Medium Priority 
- Networked multiplayer dialogue controller (New Capability) - [Note 2](Roadmap.md#note-2-networked-multiplayer-dialogue-controller)
- Configurable duration for speech nodes that do not have audio (New Capability) - [Note 3](Roadmap.md#note-3-configurable-default-duration-for-speech-nodes)
- Error log that allows user to focus problem nodes (Quality of Life) - [Note 4](Roadmap.md#note-4-error-log-that-allows-user-to-focus-problem-nodes)
- Button in Jump Node details panel to focus the target node (Quality of Life)

## Low Priority 
- Comment bubbles (Cosmetic)
- Clean up appearance of reroute nodes (Cosmetic) - [Note 5](Roadmap.md#note-5-clean-up-appearance-of-reroute-nodes)
- Compile sound (Cosmetic)
- Analytics log: counts speeches, lines of dialogue, etc. (Quality of Life)

## Completed 
- Switched Behavior Flags from a Set to a GameplayTagContainer for a much more flexible approach. 
- Changed the way variables are pulled from Queries and Events to create fields in the Graph's details panel. This removes the restriction around the types of variables that can be filled from the editor and simplifies the creation of custom graph descriptions.
- Fixed a benign but annoying issue where the events Reset Node Visits and Reset All Node Visits required a Speaker to be selected in the graph despite having nothing to do with speakers.

## Notes 
#### Note 1: Collapsing groups of nodes to a "macro"
This feature is planned to help wrangle very large dialogues. Like most dialogue plugins out there, the bigger and more interconnected the dialogue, the more it will start to sprawl. I therefore intend to add some kind of feature to collapse groups of nodes into a sub-graph. Think of a sub-state machine or a Blueprint macro. The idea being to allow the user to abstract a chunk of dialogue and place that abstracted node freely in the graph.

#### Note 2: Networked multiplayer dialogue controller
Why is this not already in the plugin? Couple reasons. First, I very rarely work with multiplayer projects so it requires a bunch of extra legwork for me to implement. Second, because it isn't part of the minimum viable product for the plugin. Extra complexity + only being necessary in some cases = save it for later.

Why is it not in the high priority category? Again, I want to focus on getting a few major Quality of Life improvements in place before I worry about expanding to new capabilities.

All of that said, the feature is coming. It's just not at the top of the list.

#### Note 3: Configurable default duration for speech nodes 
Currently speech nodes with an auto-transition wait for their audio to finish playing before moving on to the next node in the chain. If they have no audio, they proceed instantly. This is fine for most situations, but slightly awkward for games that include text and no audio, as it slightly limits their ability to "chain" npc speeches. Essentially they are currently forced to choose between **a)** including an empty audio clip or **b)** having some kind of "continue" option for the player to select between the chained npc speeches.

Adding a configurable duration to the speech node will allow speeches to be given a minimum duration to wait before proceeding. Not the highest priority change, but worth adding.

#### Note 4: Error log that allows user to "focus" problem nodes
Currently nodes that cause a compilation error get a red error banner and display a message indicating the problem. This allows users to visually identify problems without too much difficulty. That said, especially for large dialogues with hundreds of nodes, it would be better to include an error log that separately identifies the problem nodes.

#### Note 5: Clean up appearance of reroute nodes
Currently there's a bit of an awkward flow to reroute nodes, particularly on connections that flow backward. In general such connections are better handled via a Jump Node, which is why this is a lower priority.