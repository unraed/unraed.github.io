---
layout: default
title: Dialogue Tree Roadmap
permalink: /DialogueTree/Roadmap
---
**Click [here](DialogueTree.md) to return to the Dialogue Tree home page.** 

# Dialogue Tree: Roadmap
Below you will find a list of planned and in progress features for Dialogue Tree. The order of completion is fluid and will depend on a combination of what seems most important and time necessary to complete the task. As new features are completed they will be moved to the "Completed" section. 

I have also included a list of tutorials I would like to add. 

Where appropriate, additional explanations are included at the bottom of the page.

## Help & Support
You can reach me for questions and support at unraedgames@gmail.com, or on the plugin's [**Discord Channel**](https://discord.gg/mf7mGXbePB). Feel free to reach out with any questions or requests. 

If you're enjoying the plugin, I would be extremely grateful if you could take a few moments out of your day to leave me a review on the [**Unreal Marketplace**](https://www.unrealengine.com/marketplace/en-US/product/dialogue-tree). 

If you would like to support further development on the project you can do so on [**Patreon.com**](https://www.patreon.com/UnraedGames). 

## Ongoing Tasks
- Auto-arrange feature (Quality of Life)
- Ability to search for and focus a specific node in the graph (Quality of Life)
- Ability to collapse groups of nodes into a "macro" or folder node (Quality of Life) - [Note](Roadmap.md#note-collapsing-groups-of-nodes-to-a-macro) 
- Networked multiplayer dialogue controller (New Capability) - [Note](Roadmap.md#note-networked-multiplayer-dialogue-controller)
- Error log that allows user to focus problem nodes (Quality of Life) - [Note](Roadmap.md#note-error-log-that-allows-user-to-focus-problem-nodes)
- Button in Jump Node details panel to focus the target node (Quality of Life)
- Comment bubbles (Cosmetic)
- Clean up appearance of reroute nodes (Cosmetic) - [Note](Roadmap.md#note-clean-up-appearance-of-reroute-nodes)
- Compile sound (Cosmetic)
- Analytics log: counts speeches, lines of dialogue, etc. (Quality of Life)
- Sprite portraits. By request, an option to use sprites interchangeably with images for CRPG portraits. (New functionality)
- A new transition type for speech nodes that automatically transitions to one of the node's children at random (New functionality) [Note](Roadmap.md#note-random-child-speech-transition)
- A new transition type for speech nodes that, each time it is visited, plays each of the node's children in sequence (New functionality) [Note](Roadmap.md#note-sequential-child-speech-transition)
- A built in solution for hooking dialogue into sequences/cutscenes (New functionality)
- CSV/Data table import/export option for dialogues (New functionality)
- Debug mode (possibly with muted audio - will require some thought - New functionality)
- Change skip behavior for input transition nodes so that the nodes by default wait to display options and only display them after a skip. Alternatively so that this behavior is selectable as an option. (Behavior Tweaks)
- Visual novel menu template. (New functionality)
- Compile shortcut (Quality of life)
- Option for automatic dialogue progression (Quality of life/New functionality)
- Icons or other visual indicators for events? (Cosmetic)
- Fix issue that prevents connections being "drawn" backwards from input to output pin (Bug fix)
- Browse to asset button for events and queries (Quality of life)
- Custom dialogue nodes extended via blueprint - e.g. a custom speech node (New functionality)? 
- Dynamic speech duration (New functionality)?
- Labels/subtitles for event/branch/etc nodes (Quality of Life)
- Formatted speeches (New functionality)

# Next
- Fix Bug: Common UI incompatibility caused by TSubclassOf<> in dialogue settings. Changing to TSoftClassPtr<> reportedly fixes. 

## Completed 
- Configurable duration for speech nodes that do not have audio
- Switched Behavior Flags from a Set to a GameplayTagContainer for a much more flexible approach. 
- Changed the way variables are pulled from Queries and Events to create fields in the Graph's details panel. This removes the restriction around the types of variables that can be filled from the editor and simplifies the creation of custom graph descriptions.
- Fixed a benign but annoying issue where the events Reset Node Visits and Reset All Node Visits required a Speaker to be selected in the graph despite having nothing to do with speakers.
- Moved the node visitation memory of dialogue from following the game instance's lifespan to that of the world. 
- Fix bug caused by Epic's implementation of SetInputMode(GameOnly) -> causes clicks to be doubled afterwards.
- Add a setting to set the default minimum duration for nodes.
- Bugfix: Skip currently continues to play previous node and next node.
- Another function for starting dialogue that allows the user to specify a specific "key node" to start at (New functionality) 
- An option to make event nodes wait for a condition before proceeding (New functionality)
- Rework speech transition icons so that there is more visual distinction - probably change input to a pure circle (Cosmetic)

## Planned Tutorials
- Tutorial on hooking dialogue into a standard/basic interaction system 
- Tutorial on creating dialogues with multiple NPCs and one player 
- Tutorial on creating "Souls" style dialogue with a silent protagonist
- Tutorial on setting up a dynamic dialogue camera which flips back and forth to point at whoever is speaking (as in The Witcher 3 and similar games)
- Tutorial on saving and loading dialogue 
- Tutorial on adding gamepad input / getting the plugin working with Common UI
- Practical tutorial on events in dialogue affecting gameplay

## Notes 
### Note: Collapsing groups of nodes to a "macro"
This feature is planned to help wrangle very large dialogues. Like most dialogue plugins out there, the bigger and more interconnected the dialogue, the more it will start to sprawl. I therefore intend to add some kind of feature to collapse groups of nodes into a sub-graph. Think of a sub-state machine or a Blueprint macro. The idea being to allow the user to abstract a chunk of dialogue and place that abstracted node freely in the graph.

### Note: Networked multiplayer dialogue controller
Why is this not already in the plugin? Couple reasons. First, I very rarely work with multiplayer projects so it requires a bunch of extra legwork for me to implement. Second, because it isn't part of the minimum viable product for the plugin. Extra complexity + only being necessary in some cases = save it for later.

All of that said, I do intend to implement the feature. 

### Note: Error log that allows user to "focus" problem nodes
Currently nodes that cause a compilation error get a red error banner and display a message indicating the problem. This allows users to visually identify problems without too much difficulty. That said, especially for large dialogues with hundreds of nodes, it would be better to include an error log that separately identifies the problem nodes.

### Note: Clean up appearance of reroute nodes
Currently there's a bit of an awkward flow to reroute nodes, particularly on connections that flow backward. In general such connections are better handled via a Jump Node, but it still needs to be addressed. 

### Note: Random Child Speech Transition 
Comes as a request from user Suthriel. Would consist of a new Speech transition that allows for multiple children of the speech node. When completing the speech, the transition would randomly select one of the node's children to proceed to. The utility of this is primarily for allowing randomized variety of responses on a more accessible level. 

Some possible additions might be the ability to ensure a given child is triggered only once (which I'm a little iffy on whether it's necessary), or the ability to weight the probability that a given child is chosen. 

Note that adding additional transition types might require a reorganization of the node creation context menu to maintain fluidity of use. 

### Note: Sequential Child Speech Transition 
Inspired by the random child transition request noted previously. The idea behind this would be to provide yet another speech transition: this one for playing each child of a speech node in sequence each time the speech is visited. Put another way:

Imagine you have a Speech creatively named "Speech," which has three children named "A," "B," and "C." 

The first time "Speech" is visited, it will transition to "A." 

If "Speech" is visited again, it will transition to "B." 

And if "Speech" is visited one more time, it will transition to "C." 

The "looping" behavior of the transition remains to be defined. It would either loop around when all options are exhausted, starting from the beginning again, or it would stay on the last option. It might also be a good idea to make this a toggleable option. 