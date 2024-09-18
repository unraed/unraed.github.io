---
layout: default
title: Dialogue On Gameplay Tags Changed Documentation
permalink: /DialogueTree/Documentation/FOnGameplayTagsChanged
---
**Click [here](Contents.md) to return to table of contents.** 

# Dialogue Tree: FOnGameplayTagsChanged
**Extends: [Dynamic Multicast Delegate](https://docs.unrealengine.com/4.27/en-US/ProgrammingAndScripting/ProgrammingWithCPP/UnrealArchitecture/Delegates/Multicast/)**

Delegate used to let others know when behavior flags change.

## Contents
1. [**Delegate Parameters**](FOnGameplayTagsChanged.md#1-delegate-parameters)
   * [**In Tags**](FOnGameplayTagsChanged.md#in-tags)

## 1. Delegate Parameters 
The following paramters must be included on any function subscribing to the delegate. 
<br>

### In Tags 
* **Type:** FGameplayTagContainer
* **Description:** New tags associated with the speaker component's current speech. Can be empty.
* **Note:** As noted elsewhere, GameplayTags and GameplayTagContainers may not be familiar to all users. They are, however, extremely flexible, easy to learn, and useful in a broad range of circumstances. 
