---
layout: default
title: Dialogue Documentation
permalink: /DialogueTree/Documentation/Dialogue
---
**Click [here](Contents.md) to return to table of contents.** 

# Dialogue Tree: Dialogue Asset
**Extends: [UObject](https://docs.unrealengine.com/5.1/en-US/API/Runtime/CoreUObject/UObject/UObject/)**

Dialogue asset that governs the flow of a single conversation.

## Contents 
1. [**Blueprint Callable Methods**](Dialogue.md#1-blueprint-callable-methods)
   * [**Set Speaker**](Dialogue.md#set-speaker-blueprintcallable)
   * [**Get Speaker**](Dialogue.md#get-speaker-blueprintcallable-pure)
   * [**Get All Speakers**](Dialogue.md#get-all-speakers-blueprintcallable-pure)
   * [**Clear Node Visits**](Dialogue.md#clear-node-visits-blueprintcallable)
   * [**Get Node Visits**](Dialogue.md#get-node-visits-blueprintcallable-blueprintpure)
   * [**Import Node Visits**](Dialogue.md#import-node-visits-blueprintcallable)

## 1. Blueprint Callable Methods 
The following methods can be called but not overridden from Blueprint. 


### Set Speaker (BlueprintCallable)

```cpp
/**
* Sets the component value associated with the given name 
* to the provided speaker component. BlueprintCallable. 
* 
* @param InName - FName, the dialogue's name for the speaker. 
* Can differ from the component's display name. 
* @param InSpeaker - UDialogueSpeakerComponent*, the component 
* associated with the speaker. 
*/
void SetSpeaker(FName InName, UDialogueSpeakerComponent* InSpeaker);
```
<br>

### Get Speaker (BlueprintCallable, Pure)

```cpp
/**
* Retrieves the speaker component associated with the given 
* name by the dialogue. BlueprintCallable. 
* 
* @param InName - FName, name associated with the desired 
* speaker
* @return UDialogueSpeakerComponent*, component associated with 
* the given speaker name. Nullptr if none found. 
*/
UDialogueSpeakerComponent* GetSpeaker(FName InName) const;
```
<br>

### Get All Speakers (BlueprintCallable, Pure)
```cpp
/**
* Retrieves the entire map of expected speaker names to their 
* speaker components. 
* 
* @return TMap<FName, UDialogueSpeakerComponent*>, the map of 
* speaker names to components. 
*/
TMap<FName, UDialogueSpeakerComponent*> GetAllSpeakers() const;
```
<br>

### Clear Node Visits (BlueprintCallable)
```cpp
/**
* Clears the "visited" status of all nodes in the graph. 
*/
void ClearVisitedNodes();
```
<br>

### Get Node Visits (BlueprintCallable, BlueprintPure)
```cpp
/**
* Extracts the dialogue's visited nodes as a struct. Useful for 
* saving. 
* 
* @return FDialogueNodeVisits - the visited nodes struct. 
*/
FDialogueNodeVisits GetVisitedNodes() const;
```
<br>

### Import Node Visits (BlueprintCallable) 
```cpp
/**
* Applies a record of visited nodes to the dialogue. Any non-matching 
* node IDs will not be applied. Will not "unvisit" nodes that have been
* separately visted by the dialogue. 
* 
* @param InNodeVisits - const FDialogueNodeVisits&, the visited nodes 
* struct.
*/
void ImportNodeVisits(const FDialogueNodeVisits& InNodeVisits);
```