---
layout: default
title: Dialogue Speaker Component Documentation
permalink: /DialogueTree/Documentation/DialogueSpeakerComponent
---
**Click [here](Contents.md) to return to table of contents.** 

# Dialogue Tree: Dialogue Speaker Component
**Extends: [UAudioComponent](https://docs.unrealengine.com/5.2/en-US/API/Runtime/Engine/Components/UAudioComponent/)**

A component representing a “Speaker” or participant in a dialogue. Serves as a liaison between the dialogue and the game world, as well as playing any actual audio clips.

## Contents
1. [**Blueprint Callable Methods**](DialogueSpeakerComponent.md#1-blueprint-callable-methods)
   * [**Set Display Name**](DialogueSpeakerComponent.md#set-display-name-blueprintcallable)
   * [**Set Dialogue Name**](DialogueSpeakerComponent.md#set-dialogue-name-blueprintcallable)
   * [**Get Display Name**](DialogueSpeakerComponent.md#get-display-name-blueprintcallable-pure)
   * [**Get Dialogue Name**](DialogueSpeakerComponent.md#get-dialogue-name-blueprintcallable-pure)
   * [**Set Owned Dialogue**](DialogueSpeakerComponent.md#set-owned-dialogue-blueprintcallable)
   * [**Get Owned Dialogue**](DialogueSpeakerComponent.md#get-owned-dialogue-blueprintcallable-pure)
   * [**Get Behavior Flags**](DialogueSpeakerComponent.md#get-behavior-flags-blueprintcallable-pure)
   * [**Start Owned Dialogue With Names**](DialogueSpeakerComponent.md#start-owned-dialogue-with-names-blueprintcallable)
   * [**Start Owned Dialogue**](DialogueSpeakerComponent.md#start-owned-dialogue-blueprintcallable)
   * [**Start Dialogue With Names**](DialogueSpeakerComponent.md#start-dialogue-with-names-blueprintcallable)
   * [**Start Dialogue**](DialogueSpeakerComponent.md#start-dialogue-blueprintcallable)
   * [**End Current Dialogue**](DialogueSpeakerComponent.md#end-current-dialogue-blueprintcallable)
   * [**Try Skip Speech**](DialogueSpeakerComponent.md#try-skip-speech-blueprintcallable)
2. [**Blueprint Implementable Methods**](DialogueSpeakerComponent.md#2-blueprint-implementable-methods)
   * [**Get Dialogue Controller**](DialogueSpeakerComponent.md#get-dialogue-controller-blueprintimplementableevent)
3. [**Data Attributes**](DialogueSpeakerComponent.md#3-data-attributes)
   * [**Display Name**](DialogueSpeakerComponent.md#display-name-editanywhere-blueprintreadwrite)
   * [**Dialogue Name**](DialogueSpeakerComponent.md#dialogue-name-editanywhere-blueprintreadwrite)
   * [**Owned Dialogue**](DialogueSpeakerComponent.md#owned-dialogue-editanywhere-blueprintreadwrite)
   * [**Behavior Flags**](DialogueSpeakerComponent.md#behavior-flags-blueprintreadonly)
   * [**On Behavior Flags Changed**](DialogueSpeakerComponent.md#on-behavior-flags-changed-blueprintassignable)

## 1. Blueprint Callable Methods 
The following methods can be called but not overridden via blueprint.
<br>

### Set Display Name (BlueprintCallable)
```cpp
/**
* Sets the speaker's display name to the provided text.
* 
* @param InDisplayName - FText, the new display name. 
*/
void SetDisplayName(FText InDisplayName);
```
<br>

### Set Dialogue Name (BlueprintCallable)
```cpp
/**
* Sets the speaker's dialogue name (the name to use for matching it 
* automatically into a dialogue role). 
* 
* @param InDialogueName - FName, the new dialogue name. 
*/
void SetDialogueName(FName InDialogueName);
```
<br>

### Get Display Name (BlueprintCallable, Pure)
```cpp
/** 
* Retrieves the display name for the speaker.
*
* @return FText, the display name. 
*/
FText GetDisplayName() const;
```
<br>

### Get Dialogue Name (BlueprintCallable, Pure)
```cpp
/**
* Retrieves the dialogue name for the speaker. This is used for matching
* the speaker component to its role in a dialogue.
* 
* @return FName - the speaker's dialogue name. 
*/
FName GetDialogueName() const;
```
<br>

### Set Owned Dialogue (BlueprintCallable)
```cpp
/**
* Sets the speaker's owned dialogue to the provided dialogue asset. 
* 
* @param InDialogue - UDialogue*, the target dialogue. 
*/
void SetOwnedDialogue(UDialogue* InDialogue);
```
<br>

### Get Owned Dialogue (BlueprintCallable, Pure)
```cpp
/**
* Retrieves the speaker's owned dialogue. 
* 
* @return UDialogue*, the owned dialogue. 
*/
UDialogue* GetOwnedDialogue();
```
<br>

### Get Behavior Flags (BlueprintCallable, Pure)
```cpp
/**
* Gets gameplay tag container marking behavior flags for any ongoing speech. 
* 
* @return FGameplayTagContainer
*/
FGameplayTagContainer GetBehaviorFlags();
```
<br>


### Start Owned Dialogue With Names (BlueprintCallable)
```cpp
/**
* Starts the default dialogue for this speaker component. Uses the provided
* name-speaker pairings for matching with target dialogue. 
* 
* @param InSpeakers - TMap<FName, UDialogueSpeakerComponent*>,
* the speaker components to pass to the dialogue. 
*/
void StartOwnedDialogueWithNames(TMap<FName, UDialogueSpeakerComponent*> InSpeakers);\
```
<br>

### Start Owned Dialogue (BlueprintCallable)
```cpp
/**
* Starts the default dialogue for this speaker component. Attempts to 
* match the provided speaker's dialogue names to those expected
* by the dialogue. Duplicate or unfilled names not allowed. 
* 
* @param InSpeakers - TArray<UDialogueSpeakerComponent*>, the conversing 
* speakers. 
*/
void StartOwnedDialogue(TArray<UDialogueSpeakerComponent*> InSpeakers);
```
<br>

### Start Dialogue With Names (BlueprintCallable)
```cpp
/**
* Starts the given dialogue. Uses the provided name-speaker pairings for
* matching with target dialogue.
* 
* @param InDialogue - UDialogue*, the dialogue to start. 
* @param InSpeakers - TMap<FName, UDialogueSpeakerComponent*>,
* the speaker components to pass to the dialogue. 
*/
void StartDialogueWithNames(UDialogue* InDialogue, TMap<FName, UDialogueSpeakerComponent*> InSpeakers);
```
<br>

### Start Dialogue (BlueprintCallable)
```cpp
/**
* Starts the given dialogue. Uses the provided speakers' dialogue names 
* for matching with target dialogue. Duplicate or unfilled dialogue names
* not allowed.
* 
* @param InDialogue - UDialogue*, the dialogue to start. 
* @param InSpeakers - TArray<UDialogueSpeakerComponent*> the conversing
* speakers. 
*/
void StartDialogue(UDialogue* InDialogue, TArray<UDialogueSpeakerComponent*> InSpeakers);
```
<br>

### End Current Dialogue (BlueprintCallable)
```cpp
/**
* Ends the dialogue the speaker is currently participating in, if applicable. Does nothing 
* if the speaker is not engaged in dialogue. 
*/
void EndCurrentDialogue();
```
<br>

### Try Skip Speech (BlueprintCallable)
```cpp
/**
* Attempts to skip the current speech that is playing. Does nothing if the 
* speaker component is not engaged in dialogue. 
*/
void TrySkipSpeech();
```

## 2. Blueprint Implementable Methods 
The following methods are intended to be implemented by the user in blueprint when creating a custom speaker component.
<br>

### Get Dialogue Controller (BlueprintImplementableEvent)
```cpp
/**
* Retrieves the dialogue controller. BlueprintImplementable to suit 
* variable user setups for the controller. 
* 
* @return ADialogueController*, the controller found.
*/
ADialogueController* GetDialogueController();
```
<br>

## 3. Data Attributes 
Data attributes associated with the class. 
<br>

### Display Name (EditAnywhere, BlueprintReadWrite) 
* **Type:** FText
* **Access:** Protected
* **Description:** The name to display for this speaker in dialogue.
<br>

### Dialogue Name (EditAnywhere, BlueprintReadWrite) 
* **Type:** FName
* **Access:** Protected
* **Description:** The "key" name used to match the speaker to its dialogue role.
<br>

### Owned Dialogue (EditAnywhere, BlueprintReadWrite) 
* **Type:** UDialogue
* **Access:** Protected
* **Description:** The default dialogue to start when initiating dialogue.
<br>

### Behavior Flags (BlueprintReadOnly) 
* **Type:** FGameplayTagContainer
* **Access:** Protected
* **Description:** Flags associated with the current speech in dialogue. Used for animation, etc. 
Updated for every new speech. Makes use of Unreal's GameplayTag system. 
* **Note:** The built in GameplayTag system is excellent and very flexible. Unfortunately, it's not as widely publicized as it deserves, so it's possible that some users will not know about it. In general I tried to keep to systems that the average Unreal user will know, but in this case I decided that GameplayTags offer enough extra flexibility to be worth the risk that some users might not immediately understand what they're looking at. If you're not already familiar with these they're well worth the short time it takes to learn them. 
<br>

### On Behavior Flags Changed (BlueprintAssignable) 
* **Type:** FOnBehaviorFlagsChanged
* **Access:** Public
* **Description:** Delegate used to let others know when behavior flags change. Takes an event/function whose parameter is an FGameplayTagContainer representing the new "behavior flags" for the speaker's current speech.
<br>

