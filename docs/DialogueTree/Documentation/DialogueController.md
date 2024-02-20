---
layout: default
title: Dialogue Controller Documentation
permalink: /DialogueTree/Documentation/DialogueController
---
**Click [here](Contents.md) to return to table of contents.** 

# Dialogue Tree: Dialogue Controller 
**Extends: [AActor](https://docs.unrealengine.com/5.2/en-US/API/Runtime/Engine/GameFramework/AActor/)**

Actor that serves as a controller linking the various axes of dialogue behavior: user input, dialogue widgets (or other display schemes), and the 
dialogue itself. Think of this as the primary interface between the player and dialogue. 

## Contents
1. [**Blueprint Callable Methods**](DialogueController.md#1-blueprint-callable-methods)
   * [**Select Option**](DialogueController.md#select-option-blueprintcallable-virtual)
   * [**Get Speakers**](DialogueController.md#get-speakers-blueprintcallable-virtual-pure)
   * [**Start Dialogue With Names**](DialogueController.md#start-dialogue-with-names-blueprintcallable)
   * [**Start Dialogue**](DialogueController.md#start-dialogue-blueprintcallable)
   * [**End Dialogue**](DialogueController.md#end-dialogue-blueprintcallable)
   * [**Skip**](DialogueController.md#skip-blueprintcallable)
   * [**Clear Node Visits**](DialogueController.md#clear-node-visits-blueprintcallable)
   * [**Set Speaker**](DialogueController.md#set-speaker-blueprintcallable)
   * [**Get Dialogue Records**](DialogueController.md#get-dialogue-records-blueprintcallable-pure)
   * [**Clear Dialogue Records**](DialogueController.md#clear-dialogue-records-blueprintcallable)
   * [**Import Dialogue Records**](DialogueController.md#import-dialogue-records-blueprintcallable)
2. [**Blueprint Implementable Methods**](DialogueController.md#2-blueprint-implementable-methods)
   * [**Open Display**](DialogueController.md#open-display-blueprintimplementable)
   * [**Close Display**](DialogueController.md#close-display-blueprintimplementable)
   * [**Display Speech**](DialogueController.md#display-speech-blueprintimplementable)
   * [**Display Options**](DialogueController.md#display-options-blueprintimplementable)
   * [**Can Open Display**](DialogueController.md#can-open-display-blueprintimplementable-pure)
   * [**Handle Missing Speaker**](DialogueController.md#handle-missing-speaker-blueprintimplementable)
3. [**Data Attributes**](DialogueController.md#3-data-attributes)
   * [**Current Dialogue**](DialogueController.md#current-dialogue-blueprintreadonly)
   * [**Widget ZOrder**](DialogueController.md#widget-zorder)
   * [**Allow Game Input In Dialogue**](DialogueController.md#allow-game-input-in-dialogue)
   * [**Default Input Mode**](DialogueController.md#default-input-mode)

## 1. Blueprint Callable Methods
The following methods can be called but not overridden via blueprint. 
<br>

### Select Option (BlueprintCallable, Virtual)
```cpp
/**
* Notifies the dialogue that the user is attempting to select
* the option at the given index.  
* 
* @param InOptionIndex - int32, index of the selection. 
*/
virtual void SelectOption(int32 InOptionIndex) const;
```
<br>

### Get Speakers (BlueprintCallable, Virtual, Pure) 
```cpp
/**
* Retrieves the map of names to speaker components for the 
* current dialogue. Empty if the current dialogue is invalid.
* BlueprintCallable. 
* 
* @return TMap<FName, UDialogueSpeakerComponent*>, the map of speakers for
* the current dialogue.
*/
virtual TMap<FName, UDialogueSpeakerComponent*> GetSpeakers() const;
```
<br>

### Start Dialogue with Names (BlueprintCallable)
```cpp
/**
* Starts the provided dialogue with the provided speaker 
* components. Matches speakers to dialogue roles using
* the provided name-speaker pairings. 
* 
* @param InDialogue - UDialogue*, the dialogue to start. 
* @param InSpeakers - TMap<FName, UDialogueSpeakerComponent*>,
* Speaker Components mapped to their names in dialogue.
*/
void StartDialogueWithNames(UDialogue* InDialogue, TMap<FName, UDialogueSpeakerComponent*> InSpeakers);
```
<br>

### Start Dialogue (BlueprintCallable)
```cpp
/**
* Starts the provided dialogue with the provided speaker
* components.Matches the speakers to dialogue roles using their dialogue 
* names. Duplicate or unfilled names not allowed.  
* 
* @param InDialogue - UDialogue*, the dialogue to start.
* @param InSpeakers - TArray<UDialogueSpeakerComponent*>, Speaker 
* Components to use.
*/
void StartDialogue(UDialogue* InDialogue, TArray<UDialogueSpeakerComponent*> InSpeakers);
```
<br>

### End Dialogue (BlueprintCallable)
```cpp
/**
* Ends the current dialogue. BlueprintCallable. 
*/
void EndDialogue();
```
<br>

### Skip (BlueprintCallable)
```cpp
/**
* Tells the dialogue we want to skip the current speech, if 
* possible. BlueprintCallable. 
*/
void Skip() const;
```
<br>

### Clear Node Visits (BlueprintCallable)
```cpp
/**
* Tells the currentdialogue to clear all previous visits from its nodes, 
* so that the nodes register as unvisited. 
*/
void ClearNodeVisits();
```
<br>

### Set Speaker (BlueprintCallable)
```cpp
/**
* Adds the designated speaker to the target dialogue, using the provided
* name as a key. If no such name is present, or if the target dialogue 
* has not been set, does nothing. 
* 
* @param InName - FName, the target name. 
* @param InSpeaker - UDialogueSpeakerComponent*, the speaker component to 
* set.
*/
void SetSpeaker(FName InName, UDialogueSpeakerComponent* InSpeaker);
```
<br>

### Get Dialogue Records (BlueprintCallable, Pure)
```cpp
/**
* Exports a dialogue records struct containing the node visits for 
* all dialogues in the game. Useful for saving.
* 
* @return FDialogueMemory - record of all node visits in the game. 
*/
FDialogueRecords GetDialogueRecords() const;
```
<br>

### Clear Dialogue Records (BlueprintCallable)
```cpp
/**
* Clears node visitation info from all dialogues in the game. Might be 
* useful when saving and loading. I used it for testing. 
*/
void ClearDialogueRecords();
```
<br>

### Import Dialogue Records (BlueprintCallable)
```cpp
/**
* Imports a dialogue records struct, adding any recorded visits to the 
* appropriate dialogues. 
* 
* @param InRecords - const FDialogueRecords&, the records to load. 
*/
void ImportDialogueRecords(const FDialogueRecords& InRecords);
```
<br>

## 2. Blueprint Implementable Methods
The following methods are intended to be implemented by the user in blueprint when creating a custom dialogue controller. 
<br>

### Open Display (BlueprintImplementable)
```cpp
/**
* Opens the user-defined dialogue display.
*/
void OpenDisplay();
```
<br>

### Close Display ((BlueprintImplementable))
```cpp
/**
* Closes the user-defined dialogue display. 
*/
void CloseDisplay();
```
<br>

### Display Speech (BlueprintImplementable)
```cpp
/**
* Displays the specified speech in dialogue. 
* 
* @param InSpeechDetails - FSpeechDetails, struct defining 
* speech details 
* @param InSpeaker - UDialogueSpeakerComponent*, speaker
* component associated with the target speech. 
*/
void DisplaySpeech(FSpeechDetails InSpeechDetails, UDialogueSpeakerComponent* InSpeaker);
```
<br>

### Display Options (BlueprintImplementable)
```cpp
/**
* Displays a set of options for the user to select from 
* in dialogue. 
* 
* @param InOptions - const TArray<FSpeechDetails>&, the speech
* details to display as options. 
*/
void DisplayOptions(const TArray<FSpeechDetails>& InOptions);
```
<br>

### Can Open Display (BlueprintImplementable, Pure) 
```cpp
/**
* Checks if we can open the user-defined dialogue display. 
*/
bool CanOpenDisplay() const;
```
<br>

### Handle Missing Speaker (BlueprintImplementable)
```cpp
/**
* User-defined behavior for when a listed speaker component is
* not provided at dialogue start. 
* 
* @param MissingName - const FName&, the name of the missing
* speaker component. 
*/
void HandleMissingSpeaker(const FName& MissingName);
``` 
<br>

## 3. Data Attributes
The following are the data attributes associated with the class.
<br>

### Current Dialogue (BlueprintReadOnly)
* **Type:** UDialogue* 
* **Access:** Protected
* **Description:** The dialogue currently being played. 

### Widget ZOrder
* **Type:** int32
* **Access:** Public
* **Description:** The target ZOrder to spawn the dialogue widget at in the viewport. This should be above any widgets which might potentially block input from the dialogue widget.

### Allow Game Input in Dialogue 
* **Type:** bool
* **Access:** Public
* **Description:** Toggles whether normal game input is allowed while the dialogue is open. If set to false, normal game input is suppressed. If set to true, normal game input is allowed in parallel with UI. Under the hood this is just determining which input mode is used. 

### Default Input Mode
* **Type:** F_DLGCachedInputMode
* **Access:** Public
* **Description:** Struct used to determine input mode parameters for when the dialogue ends. Unfortunately the engine doesn't seem to have a means of retrieving these values; setting them here allows the user to fully customize what input mode the game reverts to when the dialogue closes. Members include:
    * **Cached Mode:** Enum value to set the desired mode. Can be Game Only (Default), Game and UI, or UI Only. 
    * **Flush Input:** Bool. Whether the input buffer should be flushed on exiting dialogue. This should only matter if game input is allowed, and rarely even then. 
    * **Hide Cursor During Capture:** Bool. Whether the cursor should be hidden during capture. Applied only if Cached Mode is set to Game and UI. 
    * **Mouse Lock Mode:** Enum value mirroring EMouseLockMode. EMouseLockMode appears hidden from Blueprints, making this workaround necessary even though it's somewhat ugly. This value allows you to determine the mouse lock behavior, if any on exiting dialogue. Not applied if Cached MOde is set to Game Only. 

