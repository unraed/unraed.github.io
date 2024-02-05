---
layout: default
title: Dialogue On Behavior Flags Changed Documentation
permalink: /DialogueTree/Documentation/FOnBehaviorFlagsChanged
---
**Click [here](Contents.md) to return to table of contents.** 

# Dialogue Tree: FOnBehaviorFlagsChanged
**Extends: [Dynamic Multicast Delegate](https://docs.unrealengine.com/4.27/en-US/ProgrammingAndScripting/ProgrammingWithCPP/UnrealArchitecture/Delegates/Multicast/)**

Delegate used to let others know when behavior flags change.

## Contents
1. [**Delegate Parameters**](FOnBehaviorFlagsChanged.md#1-delegate-parameters)
   * [**In Flags**](FOnBehaviorFlagsChanged.md#in-flags)

## 1. Delegate Parameters 
The following paramters must be included on any function subscribing to the delegate. 
<br>

### In Flags 
* **Type:** FGameplayTagContainer
* **Description:** New tags associated with the speaker component's current speech. Can be empty.
* **Note:** As noted elsewhere, GameplayTags and GameplayTagContainers may not be familiar to all users. They are, however, extremely flexible, easy to learn, and useful in a broad range of circumstances. 
