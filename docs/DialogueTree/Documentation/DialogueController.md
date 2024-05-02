---
layout: default
title: Dialogue Controller Documentation
permalink: /DialogueTree/Documentation/DialogueController
---
**Click [here](Contents.md) to return to table of contents.** 

# Dialogue Tree: Dialogue Controller 
**Extends: [AActor](https://docs.unrealengine.com/5.2/en-US/API/Runtime/Engine/GameFramework/AActor/)**

Actor that serves as a controller linking the various aspects of dialogue behavior: user input, dialogue widgets (or other display schemes), and the 
dialogue itself. Think of this as the primary interface between the player and dialogue. 

Some important considerations: 
- The controller is not placeable. Instead, a single controller will be automatically spawned in to follow the lifespan of your World. 
- Because the controller manages the "memory" of which nodes have been visited, those records also follow the lifespan of your world. 
- Custom controllers can be implemented by the user to achieve very different behavior in dialogue. To replace the default BP_BasicDialogueController with a custom implementation, set the DialogueControllerType in ProjectSettings>>Dialogue Tree. See [**Plugin Settings**](PluginSettings.md).
- The default controller has a number of configurable settings that can be set in ProjectSettings>>Dialogue Tree. 

## Contents
1. [**Blueprint Callable Methods**](DialogueController.md#1-blueprint-callable-methods)
   * [**Select Option**](DialogueController.md#select-option-blueprintcallable-virtual)
   * [**Get Speakers**](DialogueController.md#get-speakers-blueprintcallable-virtual-pure)
   * [**Start Dialogue With Names**](DialogueController.md#start-dialogue-with-names-blueprintcallable)
   * [**Start Dialogue**](DialogueController.md#start-dialogue-blueprintcallable)
   * [**Start Dialogue With Names At**](DialogueController.md#start-dialogue-with-names-at-blueprintcallable)
   * [**Start Dialogue At**](DialogueController.md#start-dialogue-at-blueprintcallable)
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
   * [**Controller Delegates**](DialogueController.md#controller-delegates-blueprintassignable)
4. [**Configurable Settings**](DialogueController.md#4-configurable-settings)


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
* @param bResume - bool - If true, the dialogue will resume from the marked
* resume node (if any). If false, the dialogue will start over.
*/
void StartDialogueWithNames(UDialogue* InDialogue, 
   TMap<FName, UDialogueSpeakerComponent*> InSpeakers, bool bResume);
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
* @param bResume - bool - If true, the dialogue will resume from the marked
* resume node (if any). If false, the dialogue will start over.
*/
void StartDialogue(UDialogue* InDialogue, TArray<UDialogueSpeakerComponent*> InSpeakers,
   bool bResume);
```
<br>

### Start Dialogue With Names At (BlueprintCallable)
```cpp
/**
* Starts the provided dialogue with the provided speaker
* components at the given dialogue node ID. Matches speakers to dialogue
* roles using the provided name-speaker pairings.
*
* @param InDialogue - UDialogue*, the dialogue to start.
* @param InSpeakers - TMap<FName, UDialogueSpeakerComponent*>,
* Speaker Components mapped to their names in dialogue.
*/
void StartDialogueWithNamesAt(UDialogue* InDialogue, FName NodeID,
	TMap<FName, UDialogueSpeakerComponent*> InSpeakers);
```
<br>

### Start Dialogue At (BlueprintCallable)
```cpp
/**
* Starts the provided dialogue with the provided speaker
* components at the given dialogue node ID. Matches the speakers to
* dialogue roles using their dialogue names. Duplicate or unfilled names
* not allowed.
*
* @param InDialogue - UDialogue*, the dialogue to start.
* @param InSpeakers - TArray<UDialogueSpeakerComponent*>, Speaker
* Components to use.
*/
void StartDialogueAt(UDialogue* InDialogue, FName NodeID,
   TArray<UDialogueSpeakerComponent*> InSpeakers);
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

**Note:** A common issue encountered here occurs when game input is set to not be allowed in the project settings. This blocks all input, which prevents Skip() getting called. You can bypass this restriction in one of two ways. Either allow game input while in dialogue, or implement an override of OnKeyDown() or OnMouseDown() in a custom Dialogue Widget. 


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
* Clears node visitation info for all dialogues in the game. 
*/
void ClearDialogueRecords();
```
<br>

### Import Dialogue Records (BlueprintCallable)
```cpp
/**
* Imports a dialogue records struct, adding any recorded visits to the 
* appropriate dialogue's record. 
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

### Controller Delegates (BlueprintAssignable)
The following are delegates that can be used to assign additional functionality to various phases in dialogue. These are included to provide another avenue for customizing/integrating dialogue into the world of your project. The delegates consist of:
   * **OnDialogueStarted:** called when the dialogue starts playing. 
   * **OnDialogueEnded:** called with the dialogue concludes.
   * **OnDialogueSpeechDisplayed:** takes an FSpeechDetails struct; called when a new speech plays. 

## 4. Configurable Settings
There are several settings that can be used to configure the behavior of the default BP_BasicDialogueController. These settings, as well as the controller type to use, can be set from ProjectSettings>>DialogueTree. For full details, please see the [**plugin settings**](PluginSettings.md) documentation. Settings include: 
   * **DialogueControllerType:** the type of controller to use if overriding the default. 
   * **Widget Type:** the type of display widget the default controller will use. 
   * **Widget ZOrder:** the ZOrder for the default controller to spawn the display widget into the viewport.
   * **Default Input Mode:** the input mode values to revert to when exiting dialogue. 
   * **Allow Game Input in Dialogue:** whether Game Input should be allowed when navigating dialogue. Please note that setting this option to false, will block ALL normal game input. As such, any key presses used in the UI will also need alternative routing. See notes on the Skip() function above. 
