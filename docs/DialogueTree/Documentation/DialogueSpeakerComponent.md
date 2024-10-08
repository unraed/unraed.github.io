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
   * [**Get Gameplay Tags**](DialogueSpeakerComponent.md#get-gameplay-tags-blueprintcallable-pure)
   * [**Start Owned Dialogue With Names**](DialogueSpeakerComponent.md#start-owned-dialogue-with-names-blueprintcallable)
   * [**Start Owned Dialogue**](DialogueSpeakerComponent.md#start-owned-dialogue-blueprintcallable)
   * [**Start Dialogue With Names**](DialogueSpeakerComponent.md#start-dialogue-with-names-blueprintcallable)
   * [**Start Dialogue**](DialogueSpeakerComponent.md#start-dialogue-blueprintcallable)
   * [**Start Owned Dialogue With Names At**](DialogueSpeakerComponent.md#start-owned-dialogue-with-names-at-blueprintcallable)
   * [**Start Owned Dialogue At**](DialogueSpeakerComponent.md#start-owned-dialogue-at-blueprintcallable)
   * [**Start Dialogue With Names At**](DialogueSpeakerComponent.md#start-dialogue-with-names-at-blueprintcallable)
   * [**Start Dialogue At**](DialogueSpeakerComponent.md#start-dialogue-at-blueprintcallable)
   * [**End Current Dialogue**](DialogueSpeakerComponent.md#end-current-dialogue-blueprintcallable)
   * [**Try Skip Speech**](DialogueSpeakerComponent.md#try-skip-speech-blueprintcallable)
2. [**Blueprint Implementable Methods**](DialogueSpeakerComponent.md#2-blueprint-implementable-methods)
   * [**Play Speech Audio Clip**](DialogueSpeakerComponent.md#play-speech-audio-clip-blueprintnativeevent)
3. [**Data Attributes**](DialogueSpeakerComponent.md#3-data-attributes)
   * [**Display Name**](DialogueSpeakerComponent.md#display-name-editanywhere-blueprintreadwrite)
   * [**Dialogue Name**](DialogueSpeakerComponent.md#dialogue-name-editanywhere-blueprintreadwrite)
   * [**Owned Dialogue**](DialogueSpeakerComponent.md#owned-dialogue-editanywhere-blueprintreadwrite)
   * [**Gameplay Tags**](DialogueSpeakerComponent.md#gameplay-tags-blueprintreadonly)
   * [**On Gameplay Tags Changed**](DialogueSpeakerComponent.md#on-gameplay-tags-changed-blueprintassignable)
   * [**On Speaker Speech Skipped**](DialogueSpeakerComponent.md#on-speech-skipped-blueprintassignable)

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

### Get Gameplay Tags (BlueprintCallable, Pure)
```cpp
/**
* Gets gameplay tag container for any ongoing speech. 
* 
* @return FGameplayTagContainer
*/
FGameplayTagContainer GetGameplayTags();
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
* @param bResume - bool, If true will resume dialogue from the marked resume
* node (if any). If false will start dialogue from the beginning. Defaults to 
* false. 
*/
void StartOwnedDialogueWithNames(TMap<FName, UDialogueSpeakerComponent*> InSpeakers, 
   bool bResume);
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
* @param bResume - bool, If true will resume dialogue from the marked resume
* node (if any). If false will start dialogue from the beginning. Defaults to 
* false. 
*/
void StartOwnedDialogue(TArray<UDialogueSpeakerComponent*> InSpeakers, bool bResume);
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
* @param bResume - bool, If true will resume dialogue from the marked resume
* node (if any). If false will start dialogue from the beginning. Defaults to 
* false. 
*/
void StartDialogueWithNames(UDialogue* InDialogue, 
   TMap<FName, UDialogueSpeakerComponent*> InSpeakers, bool bResume);
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
* @param bResume - bool, If true will resume dialogue from the marked resume
* node (if any). If false will start dialogue from the beginning. Defaults to 
* false. 
*/
void StartDialogue(UDialogue* InDialogue, TArray<UDialogueSpeakerComponent*> InSpeakers, 
   bool bResume);
```
<br>

### Start Owned Dialogue With Names At (BlueprintCallable)
```cpp
/**
* Starts the default dialogue for this speaker component at the given 
* NodeID location. Uses the provided name-speaker pairings for matching 
* with target dialogue.
*
* @param InNodeID - FName, the target node ID to start at. 
* @param InSpeakers - TMap<FName, UDialogueSpeakerComponent*>,
* the speaker components to pass to the dialogue.
*/
void StartOwnedDialogueWithNamesAt(FName InNodeID, 
   TMap<FName, UDialogueSpeakerComponent*> InSpeakers);
```
<br>

### Start Owned Dialogue At (BlueprintCallable)
```cpp
/**
* Starts the default dialogue for this speaker component at the given node 
* ID. Attempts to match the provided speaker's dialogue names to those 
* expected by the dialogue. Duplicate or unfilled names not allowed.
*
* @param InNodeID - FName, the target node to start at. 
* @param InSpeakers - TArray<UDialogueSpeakerComponent*>, the conversing
* speakers.
*/
void StartOwnedDialogueAt(FName InNodeID, TArray<UDialogueSpeakerComponent*> InSpeakers);
```
<br>

### Start Dialogue With Names At (BlueprintCallable)
```cpp
/**
* Starts the given dialogue at the given node ID. Uses the provided 
* name-speaker pairings for matching with target dialogue.
*
* @param InDialogue - UDialogue*, the dialogue to start.
* @param InNodeID - FName, the target node to start at. 
* @param InSpeakers - TMap<FName, UDialogueSpeakerComponent*>,
* the speaker components to pass to the dialogue.
*/
void StartDialogueWithNamesAt(UDialogue* InDialogue, FName InNodeID,
	TMap<FName, UDialogueSpeakerComponent*> InSpeakers);
```
<br>

### Start Dialogue At (BlueprintCallable)
```cpp
/**
* Starts the given dialogue at the given node ID. Uses the provided 
* speakers' dialogue names for matching with target dialogue. Duplicate 
* or unfilled dialogue names not allowed.
*
* @param InNodeID - FName, the target node to start at. 
* @param InDialogue - UDialogue*, the dialogue to start.
* @param InSpeakers - TArray<UDialogueSpeakerComponent*> the conversing
* speakers.
*/
void StartDialogueAt(UDialogue* InDialogue, FName InNodeID,
	TArray<UDialogueSpeakerComponent*> InSpeakers);
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
**Note:** A common issue encountered here occurs when game input is set to not be allowed in the project settings. This blocks all input, which prevents TrySkipSpeech() getting called. You can bypass this restriction in one of two ways. Either allow game input while in dialogue, or implement an override of OnKeyDown() or OnMouseDown() in a custom Dialogue Widget. 

## 2. Blueprint Implementable Methods

The following methods can have their behavior implemented or altered in blueprints. 

### Play Speech Audio Clip (BlueprintNativeEvent)
```cpp
/**
* Plays the given audio clip. Exposed to blueprint to be
* user-overridable. 
* 
* @param InAudio - USoundBase*, the audio clip. 
*/
void PlaySpeechAudioClip(USoundBase* InAudio);
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

### Gameplay Tags (BlueprintReadOnly) 
* **Type:** FGameplayTagContainer
* **Access:** Protected
* **Description:** Tags associated with the current speech in dialogue. Used for animation, etc. 
Updated for every new speech. Makes use of Unreal's GameplayTag system. 
* **Note:** The built in GameplayTag system is excellent and very flexible. Unfortunately, it's not as widely publicized as it deserves, so it's possible that some users will not know about it. In general I tried to keep to systems that the average Unreal user will know, but in this case I decided that GameplayTags offer enough extra flexibility to be worth the risk that some users might not immediately understand what they're looking at. If you're not already familiar with these they're well worth the short time it takes to learn them. 
<br>

### On Gameplay Tags Changed (BlueprintAssignable) 
* **Type:** FOnGameplayTagsChanged
* **Access:** Public
* **Description:** Delegate used to let others know when gameplay Tags change. Takes an event/function whose parameter is an FGameplayTagContainer representing the new tags for the speaker's current speech.
<br>

### On Speech Skipped (BlueprintAssignable) 
* **Type:** FSpeakerSpeechSignature
* **Access:** Public
* **Description:** Delegate used to let others know when this speaker's speech was skipped. 
<br>

