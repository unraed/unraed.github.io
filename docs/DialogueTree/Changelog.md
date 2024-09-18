---
layout: default
title: Dialogue Tree Changelog
permalink: /DialogueTree/Changelog
---
**Click [here](DialogueTree.md) to return to the Dialogue Tree home page.** 

# Dialogue Tree: Changelog
Below you will find a brief summary of changes made to the plugin. 

## Initial Release - v1.0  
- Plugin released on the Unreal Marketplace 

## 2/12/2024 - v1.0, Hotfix 1 
- Fixed an issue that was causing node visuals not to load in the plugin build downloaded from the Unreal Marketplace. 

## 2/13/2024 - v1.0, Hotfix 2
- Adjusted the zOrder of the template widgets in the viewport to account for conflicts with other widgets/plugins that may accidentally make a Canvas Panel visible, thereby blocking the dialogue widget from receiving input. Dialogue Menu Widgets should now spawn "above" any blocking widgets. 

## 3/4/2024 - v1.1
**New Features**
- Added a subsystem to manage the creation of the dialogue controller following a Singleton-like pattern. Thanks to user dalby_spook for the suggestion. See the documentation on [**Dialogue Controllers**](Documentation/DialogueController.md) for more information. Some considerations: 
    * Any custom dialogue controller actors you have created can still be used. 
    * Dialogue Controller actors are no longer placeable, and any Dialogue Controllers already present in the level will be automatically removed when the world instantiates.
    * Your preferred Dialogue Controller can now be set in Project Settings under DialogueTree>>DialogueControllerType. Not setting this field will result in the system using the default dialogue controller. 
    * The Dialogue Controller will share the lifespan of your World. 
    * **TLDR; you no longer have to manually place a Dialogue Controller in your level and if you want to specify a custom controller you can do it in Project Settings.**
- Added configurable settings for the default dialogue controller to ProjectSettings>>DialogueTree. For more information, see the documentation page for the [**new settings**](Documentation/PluginSettings.md). The settings include: 
    * Setting the widget type used 
    * Setting the ZOrder the widget will be spawned at in the viewport. 
    * Setting the input mode values that the system will revert your game to when exiting dialogue.
    * Toggling whether normal game input will be allowed while navigating the dialogue menu. 
- Added a configurable "minimum play time" property to speech nodes. This allows auto-transitions to play with a fixed duration even if no audio is attached. See the documentation on [**Speech Nodes**](Documentation/DialogueNodes.md#speech-node) for more information. 
- Converted the parameters for user-implementable Query and Event functions to a struct consisting of both a SpeakerComponent and its owning Actor. This was done to eliminate confusion and provide easier access to the owning actor's functionality. **Please note that existing Queries and Events will need to have their "entry" pins reconnected.** Thanks to all of you who requested this change for the suggestion. More information is available on the documentation pages for [**Queries**](Documentation/DialogueQuery.md) and [**Events**](Documentation/DialogueEvent.md).
- Added an array of additional speakers as parameters to user-implementable Query and Event functions to facilitate more complex behavior. Thanks to user Gladiator for the suggestion. 
- Added an EndCurrentDialogue() function to the Speaker Components to make terminating dialogue externally easier. This function is BlueprintCallable. Thanks to user Suthriel for the suggestion. See the documentation on [**Speaker Components**](Documentation/DialogueSpeakerComponent.md) for more information. 
- Added a TrySkipSpeech() function to the Speaker Components to make skipping speeches easier. This function is BlueprintCallable. 
- Added three new delegates to the Dialogue Controller to facilitate another avenue of customization. These are BlueprintAssignable for ease of use. See the documentation on [**Dialogue Controllers**](Documentation/DialogueController.md) for more information. The delegates are:
    * OnDialogueStarted
    * OnDialogueEnded
    * OnDialogueSpeechDisplayed

**Version Synchronization**
- Backported previous hotfixes to engine 5.1 and 5.2 versions.
- Made engine 5.1 version the default development build so as to avoid future incompatibilities. 

**Bug Fixes and Cleanup**
- Made the Dialogue Widgets focusable. 
- Fixed an issue that caused CRPG Potraits to stretch rather than scale to fit the intended space in the dialogue widget. They will now scale, keeping their proper dimensions as intended.
- Fixed an issue where dialogues would not abort for speeches with missing Speakers. 
- Fixed a crash that occurred when an Event Node triggered at the very end of a dialogue. 
- Fixed an issue that caused some nodes to share data when copied and pasted. 
- Removed the awkward "paste" option from the graph context menu. Pasting nodes is still possible using standard hotkeys.
- Made the "memory" of which dialogue nodes had been visited follow the lifespan of the World rather than the Game Instance as had been the case previously.  
- Added a number of new error/warning messages to the output log to help troubleshoot potential issues. 

## 3/7/2024 - v1.1.1
- Added additional measures to ensure Dialogue Controller would not be unloaded spatially when using Open World projects
- Fixed a bug that caused certain settings not to load if Widget Type had not been explicitly set in project settings
- Eased the overly aggressive text wrapping on the speaker name text for the basic dialogue controller.
- Made the default setting for the dialogue controller be to allow game input in dialogue 
- Fixed an issue with the various skip() functions that prevented them from operating:
    * Please note that, if you set the controller to not allow game input while in dialogue, you will need an alternative way to call skip(). Please see the documentation for the [**Dialogue Controller**](Documentation/DialogueController.md) for more information.

## 3/15/2024 - v1.1.2
- Fixed a crash that sometimes occurred when the last two nodes in dialogue were a speech node with an input transition followed by an event node.

## 4/25/2024 - v1.1.3
- Added compatibility with Unreal Engine v5.4. Please note that other engine versions will continue to use plugin v1.1.2, as there are no user-facing changes between the two versions.

## 9/18/2024 - v1.2.0
Please note that many of the new features require you to recompile your dialogues. All existing dialogues will work as before; you just need to reclick the compile button. 

**Features**
- Added a new Option Lock Node to allow users to display unselectable options in dialogue, along 
with a message indicating why the option is "locked." For example: "Mais, je suis Unraed! [You don't speak French]".
- Made it possible to introduce a custom dialogue option widget when using the default controller 
and default widgets. To do this, change the value of "Dialogue Option Widget Type" in Project Settings>>Dialogue Tree. 
- Added the ability to start dialogue from an arbitrary node using new StartDialogueAt(NodeID) functions. The Node ID is an FName matching the speech title in the graph. 
- Added the option to resume dialogue from a preset location rather than starting from either the beginning or an arbitrary node. 
- Added a dialogue event to set the resume node from dialogue. 
- Added a new setting allowing users to set the default minimum play time for new speech nodes. Minimum play time can still be edited on the speech nodes themselves. This setting defaults to 3 seconds.
- Gave dialogue events the ability to "block" until a condition is met. For example, if you had an event where you wanted a character to move from point A to point B, you could make the dialogue wait to transition out of the event node until the character reached point B. 
- Made speeches able to play dialogue events, complete with blocking until events finish. 
- Added a function in dialogue events that allows them to retrieve the speech details struct of any speech they were called from. If the dialogue event was called from a normal event node rather than a speech, this function will return an empty speech details struct. 
- Added a helper function to dialogue events allowing them to more easily spawn actors into the current world. "SpawnActorToCurrentWorld()" is functionally the same as "SpawnActorOfClass()". 
- Added a dialogue event that spawns and plays a cinematic, automatically attempting to bind event speakers using their dialogue names for tags.
- Added the option to Skip() events, complete with a new function to define skipping behavior in the dialogue event.
- Changed input transition symbol to more clearly differentiate it from the autotransition.
- Added helper function to dialogue events to more easily spawn actors into the world. 
- By request, moved the playing of speech audio into a blueprintnative function on the speaker component called "PlaySpeechAudioClip()". This allows users to override the way audio is handled by creating a custom speaker component in blueprint. 
- By request, added a bindable delegate to the speaker component that can be used to assign custom behavior when a speech is skipped. 

**Bug Fixes and Misc.**
- Refactored details panel customization code for greatly improved performance when changing conditions as well as target nodes and speakers. 
- Changed the storage of dialogue nodes to be indexed by a unique FNameID matching the graph node's speech title. This is a precondition for the ability to start dialogue at an arbitrary point (see above).
- Fixed a crash resulting from attempting to call SelectOption() when no dialogue is playing.
- Fixed a bug that caused audio from a speech with an input transition to continue playing after selecting an option, causing two nodes to try "talking over each other." 
- Fixed a bug in point and click type games where setting the input mode to Game Only resulted in users having to double click instead of single click in the world.
- Fixed a bug that caused the graph description of a dialogue event not to update in the details panel until the dialogue graph was closed and then reopened. 
- Closed an edge case that I think was causing an issue where dialogue graphs would get "wiped." For context, I think what was happening is that the dialogue graph was loading in too late on some projects, causing a new graph to be generated. I was not able to replicate the issue, however, so I would be very grateful for reports of whether or not it is now fixed. 
- Renamed "Behavior Flags" to "Gameplay Tags" for greater clarity. 
- Replaced some "hard" pointers with their soft equivalents to better account for conflicts with other plugins. Changing loading phase to "Post-Default" introduced its own crashes, so I have opted to leave it at "Pre-Default" for now and rely on the soft pointers. 
- Fixed a bug that caused a crash when compiling a dialogue that contained a node with connections back to a parent node. 
- Fixed crash that could occur when attempting to play an empty dialogue.