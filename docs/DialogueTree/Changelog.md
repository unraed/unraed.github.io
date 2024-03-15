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